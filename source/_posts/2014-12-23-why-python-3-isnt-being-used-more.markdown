---
layout: post
title: "Why Python 3 Isn't Being Used More"
date: 2014-12-23 16:48:48 -0800
comments: true
categories:
---

Disclaimer: None of this is to bash on python itself, but moreso the
ecosystem and problems that exist with it.

Earlier this week, I decided to start working on a new personal project. As I've
grown as a developer, the steps I take to begin something new have dramatically
changed. In the beginning, I would fire up gedit and start editing files. I
didn't know what version control was and I was happy just editing files and
saving them. Of course once I discovered git, I couldn't possibly understand how
I had managed before version control. Similarly, once I started using python's
`virtualenv` I couldn't imagine going without it when I started to work on a
project. And then I found my way to Vagrant and just virtualizing entire
boxes.

So, when I decided to start a new django project this week, I said to myself,
"Hey. I should write it all in python 3." Where I work right now, we're still
stuck on python 2, mostly due to a few dependencies and that we just haven't had
the time to change code to python 3. But this is a personal project, and if I
never ran into another Unicode error, I would be soooo happy! If I want
to play around with python 3, I can, dammit. And thus began the beginning of
my troubles....

My first steps were to put together some configuration stuff to provision a
vagrant box. Always wanting to be cutting-edge, I decided I would would start
with ubuntu 14.04 (trusty tahr) and provision it with Ansible. I've mostly only
toyed with other orchestration tools, but been very happy with Ansible. It
happens to be written in Python 2, but hey, that's not an issue. I'm fine with
using python for system stuff. That's what virtual environments are for.
Besides forgetting to install `python-dev` and `python-psycopg2` for python 2
(for Ansible) I wasn't having too many issues.

Until I tried to have Ansible install my python 3 requirements.txt file for my
django project. Since `pip` is still an alias to python 2's `pip` and not `pip3`
in ubuntu 14.04, I needed to use a different command. No big deal, Ansible's
`pip` module has it documented that you can pass a parameter, `executable` which
is to specify a different executable (in this case `pip3`). And then, of course,
I want my dependencies to be in a virtual environment, so again there is a
parameter to specify the directory and the command for your virtual environment.
Upon reading about python 3, I had learned that virtual environments had been
added to the standard library and the module was called `pyvenv`. Cool! Except
for one thing... It's broken in ubuntu 14.04. See [this](http://askubuntu.com/questions/488529/pyvenv-3-4-error-returned-non-zero-exit-status-1)
ask ubuntu question for a bit more context. And the solution, passing
`--without-pip` to `pyvenv` isn't really an option for me since Ansible doesn't
allow passing args to the virtual environment command that is called by it's
pip module.

Now this may sound kind of trivial, and working around it isn't incredibly
difficult. But my point is that it took hours, instead of minutes to just get my
dev environment setup for a new project. I recognize that the fault lies in
several places, and probably least of all, with Python 3 itself. But it doesn't
matter if it's Python's fault or not. If the ecosystem to work with it involves
a bunch of things that don't 'just work', it will be difficult to get people to
use it. I want to use Python 3. When will the ecosystem get to a place where it
is just as easy for me to use as it still is for Python 2?
