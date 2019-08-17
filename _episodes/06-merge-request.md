---
title: "Making a merge request"
teaching: 10
exercises: 15
objectives:
- "Make a friend"
- "Make a merge request to your friends repo"
- "Accept and merge request"
questions:
- "How do I fix someone else's code?"
keypoints:
- "You can fix someone else's code without direct edit rights to their repository"

hidden: false
---

> ## This episode assumes
>
> - You can run your code in a docker container.
{: .prereq}

There are a number of ways to share code with your collaborators and
git. Earlier we learned that you can add your collaborators public
repositories as remotes and merge their changes directly into your
code.

ATLAS follows a slightly more web-gui--focused workflow which you
_might_ have seen if you've ever contributed to a project on
github. The general idea is to:

- "Fork" your friend's repository directly using the gitlab GUI
- Make your local changes and push them to your fork
- Make a "merge request" to ask your friend to review / accept your
  changes.

**Note:** You can interact with git from your native laptop
  environment or within the images. From now on we'll _assume_ you are
  in the image.

## Forking your "friend's" repo

Assuming everyone has marked their repository public you should be
able to navigate to friend's github repository via your browser. You
can "fork" if their code by clicking the "fork" button on the upper
right (next to the big blue clone button we used before).

Once forking has finished, you can "clone" your fork as you did
before.
