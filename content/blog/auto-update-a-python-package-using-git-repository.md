+++
type = "blog"
title = "Auto update a Python package using Git repository"
description = 'A "hackish" way to automatically / self update a custom python package hosted using git repo'
date = "2018-05-20"
tags = ["python", "package", "self-update"]
categories = ["python", "python package"]
share = true
comments = true
keywords = "python packaging self-update"
+++

We, at work, are exclusively Ansible oriented. Most of our day-to-day work happens using Ansible. But there is a big problem when it comes to using Ansible. I really can't call it a problem though. It's just the way Ansible works. Ansible uses a push based model, meaning if you want some changes reflected on target machines, you have to push those changes using a controller machine. There is something called [ansible-pull](http://docs.ansible.com/ansible/latest/cli/ansible-pull.html) which uses pull based model, but we (more specifically I) haven't used it yet, so I am not going to talk about it. Now, coming back to the problem. Everyday we write a lot of python scripts/module/packages that we use in our automation. But the problem is every time those Python codes are updated, we have to push those changes to all machines in our infra. This is where a Puppet like model helps, but that model has it's own shortcomings. So, I decided to come up with a way to get these Python code updated every time there are changes.

TL;DR At my current work, I wanted to make my life easier by coming up with a way where every time I or anyone else updates Python code/scripts/modules, that should get reflected in places where they are getting used.

To be able to achieve this, first thing I needed was to have a git repo which we can control exclusively. No one could commit directly to it's master branch. So, I created a separate Git repo with all Python code related files and locked it for direct master commits. Achieving this is very easy. Google it if you want to find out how to do that.

Then I created a [`__init__.py`](https://docs.python.org/3/tutorial/modules.html#packages) file under that repo. As described in reference link, the `__init__.py` is a special file and I would really encourage you to go ahead and read it if you want to understand how Python uses packages and modules. The code for `__init__.py` is this:
<script src="https://gist.github.com/abhinav1107/48938cc53bfb293a32846aaaa55230ab.js"></script>

Let's demonstrate this with an example. Let's assume your Python package looks something like what's hosted at my [demo_supp](https://github.com/abhinav1107/demo_supp) (that's the best name I could come up with, so never mind)

And here is the screen shot of the same in action
<a data-flickr-embed="true"  href="https://www.flickr.com/photos/109446163@N05/41519714354/in/album-72157695319518191/" title="gitdemo1"><img src="https://farm1.staticflickr.com/973/41519714354_5a605f5a03_c.jpg" width="800" height="310" alt="gitdemo1"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

As shown in the screenshot, here is the code used for my test script:

```python
#!/usr/bin/env python

import sys
sys.path.insert(0, '/tmp')
from demo_supp.base_class1 import MyBaseClass1, MyBaseClass2

my_obj1 = MyBaseClass1()
my_obj2 = MyBaseClass2()

print(my_obj1.get_base_string())
my_obj2.base_class2_function1()
```

My demo_supp repo was checked out at `/tmp` directory. That's why I am appending that directory to PYTHONPATH so that Python will look for packages in that directory. Now notice how the first time when script ran, it prints

```text
I am in updated demo function1
Do something cool here with MyVariable
I am in updated demo function2
I am the init string in base class 1
do something cooler here with MyVariable
```

Then I go ahead and made some changed to git repo using Github's UI. In 2nd run, even though nothing else was done, the test script outputs this

```text
I am in updated demo function1
UPDATED: Do something cool here with MyVariable
I am in updated demo function2
I am the init string in base class 1
UPDATED: do something cooler here with MyVariable
```

It automatically updated the repo before printing that output. So, there you have it. Doesn't matter where your code is, as long as it has git command line utility and ability to connect to remote git repo, the local package files will be automatically updated every time there is changes in them. That's it for now. I hope someone find this useful. :)

Some Notes:<br/>
- This code is under testing phase as of this writing. If something breaks, I will be updating it.<br/>
- If you intend to use it, use it at your own risk please. Ensure it suits your requirements.<br/>

Happy coding!