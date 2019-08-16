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

## Set up the ATLAS environment

Remember that we created some keys in the `~/.ssh` directory a while
back? We're going to need to use these to edit code while in the
docker container where we run ATLAS code.

First copy the keys into the `Bootcamp` directory, make _sure_ you do
this from the `Bootcamp` directory and **not** from the
`bootcamp-example` code, which is going to be versioned.

~~~
cp -r ~/.ssh ssh-credentials
~~~
{: .bash}

Then we'll have to launch a docker image:

~~~
docker run --rm -it -w /home/atlas/Bootcamp -v $PWD:/home/atlas/Bootcamp atlas/analysisbase:21.2.85-centos7 bash -c 'cp -r ssh-credentials ~/.ssh ; bash'
~~~
{: .bash}

Let's unpack what we just did there, since it was a _very_ long command. `docker run`, runs a container, but we supplied a few named arguments:
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
image where git will find them.


## Compile this code

It's good practice to do a few things _before_ you push code to your public repository:

 1. make sure it compiles
 2. make sure it runs

If you're not already in an `AnalysisBase` image, move into the
directory that _contains_ `dan-example` and run


next `cd` to `/home/atlas/Bootcamp`. You should see `dan-example`
here.

As we learned in the pre-course material, you should build code from a
directory which is _on the same level_ as your code repository. Create the build directory and build your code.

~~~
mkdir build
cd build
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
> you can commit your changes with `git commit -am "fix bug"`
{: .callout}

## Push the code

Assuming everything compiles and you can run the resulting executable,
you can push your new code to your repository.

~~~
git push origin master
~~~
