---
title: "Adding ATLAS code"
teaching: 10
exercises: 15
objectives:
- "Delete and re-clone your gitlab project"
- "Add the rest of your ATLAS code"
- "Push the code to gitlab"
questions:
- "How do I add to an existing project?"
keypoints:
- "Once you've pushed to gitlab, your code is backed up!"

hidden: false
---

> ## This episode assumes
>
> - You've uploaded a readme to gitlab
{: .prereq}

## Delete your local repository (!)

First, **make sure your repository on gitlab is there!**

Now let's do something super careless: go to the directory above your repository and run

~~~
rm -rf my-repository
~~~
{: .source}

Poof: gone just like that! This is a contrived case but this _will_ happen to you at some point in the future.

## Bring your local repository back

Good thing we just pused to gitlab. Let's clone the repository again:

~~~
git clone 
~~~
