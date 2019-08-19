---
title: Setup
questions:
- "What do I need to start?"

---
> ## Prerequisites
>
> Most of the prerequisites should have been covered if you did the
> pre-workshop material.
>
> At a bare minimum:
> - You should have git working on your laptop
> - You should have docker working
> - We assume that you already have a CERN account
{: .prereq}

To ensure that your gitlab account is active, go to
[gitlab.cern.ch](gitlab.cern.ch).

You should find your very own gitlab homepage!

If you're having issues, **please notify your instructor immediately**
since you won't be able to follow this lesson without access to CERN's
Gitlab.

## Set up your working directory structure

We want to start everything in a _relatively_ clean directory, which has:
- The pre-workshop material
- The input data file in a path like
  ~~~
  data/DAOD_EXOT27.17882744._000026.pool.root.1
  ~~~

You can check your working directory with `tree .`. I get something like

~~~
.
├── data
│   └── DAOD_EXOT27.17882744._000026.pool.root.1
└── pre-workshop
    ├── AnalysisPayload.cxx
    ├── CMakeLists.txt
    └── README.md
~~~
{: .output}
