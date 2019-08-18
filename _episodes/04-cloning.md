---
title: "Cloning"
teaching: 5
exercises: 5
objectives:
- "Delete and re-clone your gitlab project"
questions:
- "How do I clone an existing project"
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
rm -rf dan-example
~~~
{: .source}

Poof: gone just like that! This is a contrived case but this _will_ happen to you at some point in the future.

> ## Be careful with `rm -rf`!
>
> We gave `rm` two options:
>  - `-r`: recursive remove, this removes the directory by recursively
>    deleting every file and subdirectory under it. This is obviously very
>    dangerous so use it with caution.
>  - `-f`: this tells `rm` to delete files even though they aren't writable.
>    In most situations files are not writable for a reason. Again this is
>    very dangerous, use with caution.
>
> Together these options are a "nuclear" option to remove something, don't
> train your fingers to type this easily[^1]
{: .callout}

[^1]: If you're curious about other things that you should only ever
    use with extreme caution:

       - `sudo` elevates your privileges to allow you to delete files you
          normally can't
       - `rm -rf *` will remove everything in your current directory,
          recursively, without asking for confirmation to remove
          writable files.

    The ultimate nuclear option is thus `sudo rm -rf *`. Please don't
    ever use this.

## Bring your local repository back

Good thing we just pushed to gitlab. Let's clone the repository
again. Go to your ''`dan-example`'' repository on gitlab again, click
"clone" button again and copy the "clone with SSH" url. Then run

~~~
git clone <copied url>
~~~
{: .bash}

You should be back where you were before you deleted everything.

> ## Cloning with other protocols
>
> Here we assumed that you used the `ssh` method, but gitlab allows
> you to clone with `kerberos` or via `https` as well. All will work
> equally well, your choice should be based on what you consider most
> convenient.
{: .callout}

## Notes
