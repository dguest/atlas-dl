---
title: "Creating a local repositry"
teaching: 10
exercises: 15
objectives:
- "Remind you how to create a _very basic_ repository"
- "Add your credentials to CERN's Gitlab"
- "Push your simple readme"
questions:
- "How do I create a simple repository?"
keypoints:
- "_Always_ add a `README.md` file to your repositry"


hidden: false
---

In this episode we hope to demonstrate that "publishing" anything via
CERN gitlab is extremely easy.

## Initalizing a repository

We'll be working with this repository for the remainder of this
workshop, so before doing anything let's make sure you're putting your
code somewhere where you won't loose it!

> ## Code in images
>
> Be _very_ careful where you put your code while developing within
> containers! Nothing in the image is saved when you exit, so make sure you
> develop within the directories you've mounted on your laptop.
{: .callout}

I would recommend creating a subdirectory like `bootcamp`. Personally
I keep my ATLAS projects under a directory called `~/work` but you can
adjust this as you see fit.

~~~
mkdir ~/work/bootcamp
cd ~/work/bootcamp
~~~
{: .source}

Now let's create a git repository

~~~
git init
~~~
{: .source}

You should see something like

~~~
Initialized empty Git repository in ...
~~~
{: .output}

where `...` is your working directory. If you try to commit something
now git will complain that there is nothing to commit. Git has good
intentions here: in general commiting nothing at all is a mistake.

## Adding a file

So let's add a file. Use your favorite text editor to create a file
called `README.md`. What you put here is up to you but _it will be the
first thing everyone sees when they look for your code_ so make it
count!

For now we'll describe what you're doing here. Add something like this

~~~
ATLAS Software Bootcamp
-----------------------

This is my bootcamp project.
There are many others like it but this one is mine.
Without my project, I am useless. Without me, my project is useless.

I will code clearly and simply.
I will document enough that my collegues may follow my work,
but not so excessively as to frighten them with walls of text.

All code will eventually need to die. I will write my code knowing this.
I will make my code modular.
I will introduce few dependencies.
When my project dies the pieces will be recycled by my collegues.
If I code poorly, they will curse me.
If I code well, they will prase me.
~~~
{: .language-markdown}

and save the file. Let's ask git what is sees now:

~~~
git status
~~~
{: .source}

~~~
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	README.md

nothing added to commit but untracked files present (use "git add" to track)
~~~
{: .output}

Great, git sees the file but it's just floating around for now, we're not properly keeping it under version control. OK, let's add it to the index:

~~~
git add README.md
~~~
{: .source}

and check that it's been properly added

~~~
git status
~~~
{: .source}

~~~
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   README.md
~~~
{: .output}

> ## Turning Red to Green
>
> Git can color its text to make it easier on your brain. If you don't
> see untracked files in red and the `new file` as green, you can run
> ~~~
> git config --global something.i.have.to.check.when.i.have.internet on
> ~~~
> {: .source}
{: .callout}

Great, now our reedme is ready to commit.

~~~
git commit -m "Add README file"
~~~
{: .source}

In general git will force you to create a commit message. You should
[try to write _good_ commit messages](TODO:link-to-git-commit-tips),
since this helps everyone understand what you were doing. In this case
it's pretty self-explanitory, but in many real world examples a commit
might just change one line deep inside your code. A commit message is
a very good way to explain _why_ you decided to make this change.

Also note that a good commit message might run for several paragraphs
to explain the full context of the commit. If you need something more
verbose, you can use the contents of a text file with
`git commit -F file.txt`.

This all might be review, but next the real fun begins: we'll push
this repository to gitlab.
