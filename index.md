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
{: .prereq}

Introduction
------------

In ATLAS we use uses Gitlab---basically an open-source replica of Github---to host our code.
Superficially the two have some confusing differences: the website layout won't match; gitlab is .com hosted by Microsoft, wheras ATLAS's Gitlab is a cern-hosted instance of an open-source project; Github encourages "pull requests" while in Gitlab you must make "merge requests".
Fortunately, beyond this veneer the core concepts are nearly identical.

The aim of this module is to:
 - explain the core diffences, and
 - expand on some concepts that are essential to anyone working in ATLAS

> ## The skills we'll focus on:
>
> 1.  The basic setup for CERN Gitlab
> 2.  Creating a new reposiotry
> 3.  Forking an existing repository
> 4.  Adding and working with multiple "remote" forks from your local repository
> 5.  Creating merge requests
> 6.  Submodules, the Athena repository, and how to contribute to both
{: .checklist}

{% include links.md %}
