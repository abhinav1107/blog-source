+++
type = "blog"
title = "Python Serialization with Dill"
description = "Converting data structure or objects state in python into a format that can be stored/transmitted and recreated later"
date = "2018-07-08"
tags = ["learning", "python", "pickle", "dill"]
categories = ["learning", "python", "pickle"]
share = true
comments = true
keywords = "python serialization marshalling pickle dill"
+++

Last week I got to know about a concept called Serialization through a friend of mine. Till that point I wasn't even aware something like this existed. I really liked the concept instantly. So to better understand this concept, I thought I will pen it down somewhere. This is my attempt to write what I have understood about `pickling`.

"Pickling" is a process where a Python object is taken and converted into byte stream. Once pickling happens, this pickled data can be taken and then un-pickled somewhere. And once un-pickled, this new object can be used as it was like in previous place.

In Python this is done using [pickle](https://docs.python.org/2/library/pickle.html) module. But I am going to demonstrate this using another module called [dill](http://dill.readthedocs.io/en/latest/). `dill` is more of less same as pickle, just that it in addition to pickling Python objects, it also provides ability to save the state of an interpreter session in a single command.

Everywhere I read about pickling, they all warned about more of less the same things. Here they are:

* `pickle` module is not secure against erroneous or maliciously constructed data. So never un-pickle data received from untrusted or unauthenticated source.
* The pickle protocol is specific to Python. We can not transfer the information to other languages.
* Not all python data structure can be serialized by pickle.
* No compatibility guaranteed between different version of python as well.
* If version is not specified, the pickle picks the latest protocol version in which pickling is done in binary format

Enough with the talk, lets see it in action. I am taking Elasticsearch connection object as an example here, because that's what I was working with when I was trying to figure out pickle.

I am a big fan of [Vagrant](https://www.vagrantup.com/) and [Docker](https://www.docker.com/) for local work. Here I am using 5 Docker containers for my overall test. 2 containers for Elasticsearch, 1 for Redis and 2 normal Python nodes as clients from where I can perform pickling process in one and un-pickling in another.

Here is how the docker compose and corresponding `Dockerfile` looks like:

<script src="https://gist.github.com/abhinav1107/25f326c4fb59dfdff95d12cb226d15f5.js"></script>

Copying this two files in a directory and running `docker-compose up -d` should ideally give you 5 running containers:

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/109446163@N05/42557972284/in/dateposted-public/" title="pickling-1-es-run"><img src="https://farm2.staticflickr.com/1821/42557972284_512f8a885e_z.jpg" width="800" alt="pickling-1-es-run"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

Now that we have something to work with, lets connect to one test container and pickle an object. In my case, I have called this container `pclient1`, so I will connect to this one. The following picture shows the commands that I ran:

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/109446163@N05/29406709548/in/dateposted-public/" title="Screen Shot 2018-07-08 at 7.14.53 PM"><img src="https://farm1.staticflickr.com/834/29406709548_3ec8100220_z.jpg" width="800" alt="Screen Shot 2018-07-08 at 7.14.53 PM"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

Basically, what happened here is, I created an object, pickled it using `dill.dumps` and stored that data in Redis. Now I will connect to other container `pclient2`, get the value from Redis using the key obtained previously and un-pickle it using `dill.loads`:

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/109446163@N05/43276908461/in/dateposted-public/" title="Screen Shot 2018-07-08 at 7.39.13 PM"><img src="https://farm2.staticflickr.com/1821/43276908461_f4eed708dd_z.jpg" width="800" alt="Screen Shot 2018-07-08 at 7.39.13 PM"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

Once I recreated the object using `dill.loads`, I can use it just like the way I used it in `pclient1`. And all these without even needing to import `elasticsearch` module in another instance.

We are using this style in one of our in-house REST API written using [Falcon](https://falconframework.org/), where there are multiple instances behind a load balancer. All we need to do now is initiate an object, pickle it, store that data in Redis and pass the client that key. Irrespective of which backend instance the client will go in subsequent requests, we can use the same connection object.

><i><u>Some Word Of Caution</u>: This entire model is in its super early stages at my work. We are still concept proofing this. So, this entire structure can change in future. but I have solid hopes on this (concept wise), unless we/I missed something really basic here. In which case, I will update this article as and when required. For now, I am really excited to have implemented it. And thought about sharing my learning experience with the world. If you are reading this and planning to implement something like this, ensure you are aware of what you are getting into.</i>

Until next time. Happy pickling :)
