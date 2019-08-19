---
title: "Adding Code"
teaching: 10
exercises: 10
objectives:
- "Add the rest of your ATLAS code"
- "Compile and test it within the ATLAS environment"
- "Push the code to gitlab"
questions:
- "How do I add to an existing project?"
keypoints:
- "Your credentials can be used within an image"
- "Always compile and test code before pushing"

hidden: false
---

> ## This episode assumes
>
> - You've uploaded a readme to gitlab
> - You did the pre-workshop material
> - You downloaded the test file. Note you can download it with
>   ~~~
>   wget https://cernbox.cern.ch/index.php/s/YXbCrQkwnZuc3yU/download
>   ~~~
>   {: .bash}
{: .prereq}

## Add ATLAS code to your repository

Now we'll add the example we gave as pre-course material to your
versioned code. Copy the `AnalysisPayload.cxx` and `CMakeLists.txt`
files from that material into your repository.

Then run

~~~
git status
~~~
{: .bash}

which should print something like

~~~
On branch master
Your branch is up to date with 'origin/master'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	AnalysisPayload.cxx
	CMakeLists.txt

nothing added to commit but untracked files present (use "git add" to track)
~~~
{: .output}

Let's add these and commit them:

~~~
git add .
git commit -m "Add payload and CMakeLists"
~~~
{: .bash}

If you run `git status` now, git should indicate that you're one
commit ahead of master.

> ## Should I add my data files?
>
> NO!! No no no! You should not add your DAOD files, or root files, to your repositories.  This is a
> big no no in ATLAS and goes under the name of adding "binaries" because they are data files
> that are only machine readable.  Due to the way that things get versioned, this can cause repositories
> to explode and during Run1 of the LHC/ATLAS, this caused for the entire ATLAS version control system (at
> that time is was [SVN-Subversion](https://subversion.apache.org/)) to crash.  **People crashed the mainframe because they did this**.
> Not to mention that it just quickly makes a repository large and bloated and very cumbersome (large) to clone.
>
> <br>
>
> Now, unfortunately some people still do this.  We will pick on the luminosity group in this instance [gonzales/mblumi](https://gitlab.cern.ch/gonzales/mblumi).
> If you find a colleague is doing this, please try to educate them. #greatergood
>
{: .callout}

## Set up the ATLAS environment

Remember that we created some keys in the `~/.ssh` directory a while
back? We're going to need to use these to push code updates to gitlab while in the
docker container where we run ATLAS code.

First copy the keys into the `Bootcamp` directory, make _sure_ you do
this from the `Bootcamp` directory and **not** from the
`bootcamp-example` code, which is going to be versioned (i.e. it would suck to accidentally push all the contents of your .ssh directory to gitlab). Also copy
your git configuration file, so that your commits include your name
and email.

~~~
cp -r ~/.ssh ssh-credentials
cp ~/.gitconfig gitconfig
~~~
{: .bash}

Then we'll have to launch a docker image:

~~~
docker run --rm -it -w /home/atlas/Bootcamp -v \
    $PWD:/home/atlas/Bootcamp atlas/analysisbase:21.2.75 \
    bash -c 'cp -r ssh-credentials ~/.ssh; cp gitconfig ~/.gitconfig ; bash'
~~~
{: .bash}

We'll come back to this in a few days, but let's unpack what we just
did there, since it was a _very_ long command. `docker run`, runs a
container, but we supplied a few named arguments:

 - `--rm`: tells docker to delete the container when you exit
 - `-it`: two arguments, run **i**nteractive with attached **t**erminal
 - `-w`: sets the directory you'll be in when the container starts
 - `-v`: mounts your current directory within the image so you can
   access files on your laptop

There were also a few positional arguments (those without a `-*`
flag).

The first points to a container: in this case we're using an ATLAS
release which includes all the libraries we'll need for analysis work.

The second argument tells the container what to run in the
container. This one is more complicated than what you might have seen
before because we have to copy our credentials into a place in the
image where git will find them[^1].

[^1]: Later on we'll learn how to build our own containers based on
    the official atlas ones. There you'll learn to run scripts
    automatically when the container starts.

> ## Exercise: Script the `docker run` command
>
> You might have to call this quite a few times throughout the remainder of the week, so it would be advisable to write a shell script
> so that it's reduced to running `./run-docker.sh`
>
> However, we'll learn a lot more about what these commands are doing later this
> week.  So if you are a bit unsure of this, then don't worry, for now let's just worry about "getting it to work".
> But if Thursday comes and you are still unsure, then keep asking until you are sure.
{: .challenge}

## Compile this code

It's good practice to do a few things _before_ you push code to your public repository:[^2]

 1. make sure it compiles
 2. make sure it runs

You want to do this so that if a colleague of yours clones your repository, they are not left with a frustrating situation
of debugging your code that was checked in hastily after "just making that one small change" that actually broke
things and caused a segfault later on.  Don't be "that colleague".
<!-- If you're not already in an `AnalysisBase` image, move into the -->
<!-- directory that _contains_ `dan-example` and run -->
Next `cd` to `/home/atlas/Bootcamp`. You should see `dan-example`
here.

[^2]: Running these tests for every commit can get tedious, later this
    week we'll learn to do this in an automated way which will help prevent you from being "that colleague".


As we learned in the pre-workshop material, you should build code from a
directory which is _on the same level_ as your code repository. Create the build directory and build your code.

~~~
mkdir build
cd build
source ~/release_setup.sh
cmake ../dan-example
make
~~~
{: .bash}

Now, _if_ everything worked you should see an executable called
`AnalysisPayload`.

Try running it just to make sure it works.

> ## What if something doesn't work?
>
> If something is broken _you should fix it_! If you have to fix anything
> you can commit your changes with `git commit -am "fix bug"` which is a bit of short hand
> and has mashed together the `-a` argument (which effectively performs a `git add -u`)
> and the `git commit` command with a commit message.  Don't forget to make
> the commit message verbose, "fix bug" itself is not so verbose given that you
> will probably be fixing many bugs during your time in the experiment.
>
{: .callout}

## Push the code

Assuming everything compiles and you can run the resulting executable,
you can push your new code to your repository.

~~~
git push origin master
~~~
{: .bash}

#### Notes

