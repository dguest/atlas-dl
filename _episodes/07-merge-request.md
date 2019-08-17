---
title: "Making a merge request"
teaching: 10
exercises: 15
objectives:
- "Make a merge request to your friends repo"
- "Accept and merge request"
questions:
- "How do I fix someone else's code?"
keypoints:
- "You can fix someone else's code without direct edit rights to their repository"

hidden: false
---

> ## This episode assumes
>
> - You can run your code in a docker container.
> - You've forked and modified someone else's repository
{: .prereq}

This episode explains the standard ATLAS procedure for pushing changes
to code back to the original authors. If you've contributed to open
source projects on github the procedure should be familiar, with a few
"gitlab" specific differences.

# Pushing your changes to your fork

First let's make sure your remotes are set up properly:

~~~
git remote -v
~~~
{: .bash}

should print something like

~~~
origin	ssh://git@gitlab.cern.ch:7999/dguest/sam-example.git (fetch)
origin	ssh://git@gitlab.cern.ch:7999/dguest/sam-example.git (push)
~~~
{: .output}

Note that this is _my_ fork of _Sam's_ example code.
