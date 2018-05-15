+++
type = "blog"
title = "How learning Python has changed my life"
description = "My slow but steady transition from a sysadmin to a better sysadmin or a DevOps"
date = "2018-05-14"
tags = ["learning", "python"]
categories = ["learning", "python"]
share = true
comments = true
keywords = "learning python"
+++
Hello there,

Today I would like to share my [Python](https://www.python.org/) learning journey with you. Before I even begin, I would like to make it clear that I in no way am a master of Python programming language. I have just been able to scratch the surface of an extremely vast topic. It's just the beginning and I have a long long long way to go. But there is a reason why I wanted to share this learning journey with everyone.

Year 2002 was when I touched a computer for the first time and then got my very own computer in 2003. I would end up using it mostly for computer gaming and writing some programs using Turbo C. This didn't change till end of 2007. That's when I got my first job as System Administrator / Technical Support Representative. My team started mentoring me and learning new things almost everyday was so exciting that I forgot about computer gaming almost entirely. That's where my actual programming journey got it's push.

For my first work, I had to do a lot of manual work. This is when I decided I would start automating things. And that's when I was introduced to [BASH](https://www.gnu.org/software/bash/). It was love at first sight to be honest. I started writing several scripts. Taking backups, cleaning older logs, server/application installation and configuration and so many other things. You name it, I did it. As time went by, I eventually got so comfortable with BASH that in my last job I wrote an entire app using BASH, Apache and CGI. It wasn't a fancy web app, rather just a simple web based tool for managing Samba shares and user quota. And this was early 2015.

Till this point, I never felt the need to learn anything else. BASH and Ansible worked for me. All these while, a subset of my friends/colleagues kept telling me to learn one proper programming language to make my life easier. And I kept telling them that what I do on a day to day basis, no one can beat BASH. Then came a JIRA ticket where I was assigned a task to ensure that all Jenkins jobs are configured to run either without labels or if job has used a label, then it should be from a list of known labels. This helps immensely in those cases where you would want to import Jenkins jobs from one environment to others.

This is what I wrote:
<script src="https://gist.github.com/abhinav1107/6ea9d7a3f288d6c8e65f6333023602f4.js"></script>

It was supposed to be a [Sensu](https://sensu.io/) check. And as of this writing, running script is almost same. This JIRA ticket made me realise that you should always pick the right tool for the job, not the tool that you are most comfortable with all the time.

Picking Python as my first full fledged programming language was a no brainer. One of the biggest plus points for me was that the syntax made sense out of the box. I didn't have to struggle through online documentation of finding what is what. I know a lot of you might not or will not agree. But this is what I feel was the biggest reason for me. here is what I wrote as my first script in Python:

<script src="https://gist.github.com/abhinav1107/471df18abf140dc816902a249be419cf.js"></script>

I was literally on the Moon after this script executed successfully for the first time. But this was still not enough. I would end up writing a lot of scripts. Most of these scripts had overlapping work or use cases. Writing something once is good, writing something twice is still ok, but writing same thing again and again is not ok. This is where [OOP](https://en.wikipedia.org/wiki/Object-oriented_programming) comes in. I had tried understanding OOP before, but miserably failed at it. Every time I asked someone how did they got better at writing Classes, they gave the same answer. Keep practicing. And this never convinced me. To me it was like a continuous loop problem. To be able to understand OOP, you need to write Classes and to be able to write Classes, you need to understand OOP.

This struggle with Classes continued, in the meanwhile I wrote some Sensu Scripts in Python which worked really well. While working with one of the Sensu Checks, I ended up asking a [Stackoverflow Question](https://goo.gl/qhxs6p). The more work I did in Python, my confidence grew more. At this point, I started reading other's work in Python. This is where things started becoming interesting. Every new Class helped me understand what it meant and what the programmer was trying to achieve. And thus my OOP journey began. As of now, I can write simple reusable Classes and create packages. The idea is to be more comfortable with Python as a programming language.

In last few days, this ability to at least understand the code (irrespective of the programming language it's written in) has given me a different kind of self confidence. I try and see things differently now. The code doesn't scare me anymore. The kind of work that I do on a day-to-day basis, this procedural approach is never going to go away, but I am loving the OOP way.

The lesson from all this is nothing is easy and nothing is hard in this world. It's about how dedicated you are to achieve things. Don't lose faith in your self just because you have had some early set backs. Keep doing things. Start small and gradually build up the knowledge.

Until next time.

- [ ] fix grammar and spelling mistakes