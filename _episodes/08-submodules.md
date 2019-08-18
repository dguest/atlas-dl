---
title: "Submodules"
teaching: 10
exercises: 15
objectives:
- "Add a submodule"
- "Update a submodule"
- "Consume a submodule"
- "Break a subdirectory into anohter submodule"
questions:
- "How do I use another repository in my project"
keypoints:
- "Submodules allow you to share common code between projects"
- "Sometimes simply consuming a submodule is a better option"

hidden: false
---

## Why use submodules?

The most important part of writing good software is to avoid writing
any software. In most cases, someone else has already done what you
want: you might as well take advantage. One way to take advantage of
other people's code is using **submodules**. This is a feature in git
that allows it to keep track of another repository _within_ your
repository.

In this case, we'll use a jet selector tool that someone else
wrote. The tool we want is called [JetSelectionHelper][jsh]. We'll add
this tool as a submodule and then adapt our code to use it.

## Adding a submodule

Go to the [JetSelectionHelper][jsh] github page and copy the URL for
cloning with ssh. Then run this command from the top level of your
source directory.

~~~
git submodule add ssh://git@gitlab.cern.ch:7999/usatlas-computing-bootcamp/JetSelectionHelper.git
~~~
{: .bash}

You should get some printouts from git but no errors. You should also see a new directory when you run `ls -l`, something like:

~~~
total 16
-rw-r--r-- 1 atlas atlas 2706 Aug 17 13:41 AnalysisPayload.cxx
-rw-r--r-- 1 atlas atlas  411 Aug 16 01:50 CMakeLists.txt
drwxr-xr-x 6 atlas atlas  204 Aug 18 21:39 JetSelectionHelper
-rw-r--r-- 1 atlas atlas  640 Aug 16 01:17 README.md
~~~
{: .output}

also take a look inside `JetSelectionHelper`, it's another repository
just like this one.

Now let's ask git what it sees by running `git status`

~~~
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#	new file:   .gitmodules
#	new file:   JetSelectionHelper
#
~~~
{: .output}

So the above command actually added _two_ files, the directory we saw
before and a `.gitmodules` file. What is that? Let's take a look:

~~~
cat .gitmodules
~~~
{: .bash}

should print something like

~~~
[submodule "JetSelectionHelper"]
	path = JetSelectionHelper
	url = ssh://git@gitlab.cern.ch:7999/usatlas-computing-bootcamp/JetSelectionHelper.git
~~~
{: .output}

Now commit these changes. Make sure to explain why you're adding this
submodule in the commit message. Finally, just to make sure nothing
broke, go back to the `build` directory and call `make`. You should
see that nothing gets recompiled.

## Building the submodule

You'll need to add small amount of magic to your `CMakeLists.txt` file
to make sure CMake builds this submodule. Go into this file and add the following lines in the end:

~~~
add_subdirectory(JetSelectionHelper)
target_link_libraries(AnalysisPayload PRIVATE JetSelectionHelper)
~~~
{: .language-cmake}

Don't worry, we'll explain all the details tomorrow. This should be
enough to tell the build system that we want to include this as part
of the project.

Recompile the package to see what happens: CMake should rerun and
build the extra package too.

## Using the submodule

Now we have to implement the package within our code. Open up
`AnalysisPayload.cxx` and add the following line at the top

~~~
// Add a submodule for JetSelectionHelper
#include "JetSelectionHelper/JetSelectionHelper.h"
~~~
{: .source}

Now let's implement a selection with this tool. First we'll need to
create an instance of the tool somewhere. Add something like this
_before_ you enter the event loop:

~~~
// add jet selection helper
JetSelectionHelper jet_selector;
~~~
{: .source}

Finally, let's use the this to apply the kinematic selection as well,
go to the spot where you applied the kinematic selection and replace
the selection with

~~~
if (jet_selector.isJetGood(jet)) {
  ...
}
~~~
{: .source}

Now try to rebuild the package.

[jsh]: https://gitlab.cern.ch/usatlas-computing-bootcamp/JetSelectionHelper
