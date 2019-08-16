---
title: "Creating the remote repository"
teaching: 10
exercises: 15
objectives:
- "Upload your simple readme file"
questions:
- "How do I create a repository and share code?"
keypoints:
- "Initializing a new repository is very easy"
- "Share your code as appropriate"

hidden: false
---

> ## This episode assumes
>
> - You've uploaded your public key to gitlab and verified that it's working
{: .prereq}

In this episode we'll finally push _something_ to a public gitlab
repository.

## Creating an empty repository on gitlab

Go to [gitlab.cern.ch], click the little "plus" icon on the center
of the top bar, and select "new project".

This will bring you to a dialog to create the project. The important
fields are:
 - The "project name": in principal this can be anything, but to make
   things less confusing we'd recommend using the same name you used
   locally. In this example this is `dan-example`.
 - The "visibility level", there are three levels allowed:
    - Private: only you and people you "share" the project with are
      allowed to see it.
    - Internal: **everyone with a CERN account** can see the
      project. This will _not_ hide anything from e.g. CMS.
    - Public (**use this**): everyone with the URL can see the project

   Note that there is no option here to make projects
   "ATLAS-only". For anything that isn't _extermely_ sensitive
   (i.e. you discovered a new particle and explicetly say this in your
   project) public should be fine.
 - The "**Initialize repository with a README**" checkbox. Do **not**
   check this, we'll upload the readme from your local repository.

The "project description" might be useful, but in general this should be explained in the README.

Click the "Create Project" button on the bottom. You should be
presented with a page that gives the name of the project and says "The
repository for this project is empty".

Make sure you keep track of the URL for this page: this is where your
public code will live from now on.

## Pushing your local project

On the empty project page there are instructions to push an existing
project. Unfortunately CERN uses a much more complicated
authentication scheme than ssh by default, so these can be confusing.

Click the blue "clone" button on the upper right side of the page. It
will give you multiple options, click the "copy URL to clipboard"
button next to "Clone with SSH".

Now you need to go back to your terminal and tell your _local_
repository that a _remote_ repository lives at this URL.

~~~
git remote add origin ssh://git@gitlab.cern.ch:7999/rest/of/url.git
~~~
{: .source}

where the last string starting with `ssh://`... is the URL you just copied.

Now try pushing your local project!

~~~
git push -u origin master
~~~
{: .source}

Once this is done, refresh the browser in your gitlab page. You should
see your README now!

[gitlab]: https://gitlab.cern.ch
[new-project]: https://gitlab.cern.ch/projects/new
