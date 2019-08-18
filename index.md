---
layout: lesson
title: Introduction
root: .  # Is the only page that doesn't follow the pattern /:path/index.html
permalink: index.html  # Is the only page that doesn't follow the pattern /:path/index.html
---

{% include gh_variables.html %}

> ## Prerequisites
>
> This assumes that you'll have some basic background with git, for example:
>
> 1. How to get a local repository, in two ways
>     * using `git init`
>     * by cloning from github
>
> 2. How to `branch`, `add` changes, `commit` them, and `push`
> 3. The basics of creating a merge request
>
> You should also have fully worked through the [pre-workshop material](https://adjackp.github.io/pre-workshopMaterial/). Having
> failed to complete this will make it very challenging and you will eventually have to go back and do this.  So take a few hours to
> be sure you have fully worked through that now.
>
{: .prereq}

Introduction
------------

In ATLAS we use use [Gitlab](https://about.gitlab.com/)---basically an open-source replica of Github---to host our code.
Superficially the two have some confusing differences:

- The website layouts won't match and you may need to click differently to get the same buttons.
- Gitlab is .com and owned/hosted by Microsoft, whereas ATLAS's Gitlab is a cern-hosted instance of an open-source project ([https://gitlab.cern.ch/](https://gitlab.cern.ch/))
- Github encourages "pull requests" while in Gitlab you must make "merge requests"

Fortunately, beyond this veneer the core concepts are nearly identical so everything you learned from the [Software Carpentry lesson](http://swcarpentry.github.io/git-novice/) applies.
The aim of this module is to expand on some concepts you learned in the morning and highlight a few of what we consider to
be essential skills to anyone working in ATLAS.

> ## The skills we'll focus on:
>
> 1.  The basic setup for CERN Gitlab
> 2.  Creating a new repository for your AnalysisPayload from the [pre-workshop material](https://adjackp.github.io/pre-workshopMaterial/)
> 3.  Forking an existing repository so you can use it "like its your own"
> 4.  Adding and working with multiple "remote" forks from your local repository
> 5.  Creating merge requests to modify code in a way to ensure that it gets reviewed
> 6.  Including code from other repositories with yours through the use of submodules
> 7.  The Athena repository, and how to contribute to it.
{: .checklist}

{% include links.md %}
