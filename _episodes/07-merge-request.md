---
title: "Making a merge request"
teaching: 10
exercises: 15
objectives:
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
> - You've forked and modified someone else's repository
> - Your changes are on a branch called `change-cuts`
{: .prereq}

This episode explains the standard ATLAS procedure for pushing changes
to code back to the original authors. Once you are comfortable with this procedure,
you will be in a position to start contributing to the ATLAS Athena code base
using the same procedure, described [here](https://atlassoftwaredocs.web.cern.ch/gittutorial/).
If you've contributed to open source projects on github the procedure should be familiar, with a few
"gitlab" specific differences.

> ## Friendtime activity!
>
> This episode works in two parts:
>  - First you'll make a merge request to your friend's repository
>  - Next you'll review your friend's merge request and merge it into your
>    repository
>
> You and your friend can work in parallel on both parts, no need to wait
> one person to finish.
>
{: .testimonial}

# Pushing your changes to your fork

First let's make sure your remote repositories are set up properly:

~~~
git remote -v
~~~
{: .bash}

should print something like

~~~
origin	ssh://git@gitlab.cern.ch:7999/dguest/sam-example.git (fetch)
origin	ssh://git@gitlab.cern.ch:7999/dguest/sam-example.git (push)
~~~
{: .output}

From the part after the second to rightmost slash you can tell that:
- This is _your_ fork (`dguest/`)
- This is from your friend's example code (`sam-example`)

> ## Exercise: add another remote
>
> Try to add another remote that points to your _friend's_ repository.
>
> > ## Hint
> > you should be able to navigate to it from the "project" section
> > of the your fork on gitlab, click the little house on the upper left.
> > From there you should see the parent repo that you forked from.
> {: .solution}
{: .challenge}

Now push your code to your fork.
~~~
git push origin change-cuts
~~~
{: .bash}

git should tell you that it pushed a branch and print a URL that you
can visit to make a merge request into the parent fork. This is a
convenient shortcut but for demonstration purposes we'll set
everything up manually.

# Making a merge request

The URL for your fork will always be something like

~~~
https://gitlab.cern.ch/YOUR_USER_NAME/REPOSITORY_NAME
~~~

where `YOUR_USER_NAME` is your CERN login and `REPOSITORY_NAME` is
whatever your friend called their repository.

 - Go to this url and click the "merge requests" button on the left
 side
 - Click the big green button that says "new merge request"
 - This will bring up a "New Merge Request" dialog
    + From the "source branch" block on the left, select the
      "change-cuts" branch
    + From the "target branch" block on the right, select
      `friend-username/repo-name`, and `master`
 - click the green "compare branches and continue"

This should bring up a "New Merge Request" dialog.

> ## Merge Request Fields
>
> - Title: should be descriptive but short (around 50 characters)
> - Description: as a general rule you should try to give the reasons
>   reasons for the changes you made, i.e. if you changed the jet pt
>   cut to 50 GeV, explain _why_ you did this; just saying _that_ you
>   changed the jet pt cut is redundant since that's clear from the
>   commit.
>
>   It's also good practice to "mention" people who might be interested
>   by using `@username`, i.e. `@meehan`. Gitlab will automatically
>   notify them.
>
> - Most of the other boxes you don't need to touch
>     - "Delete source branch wen merge request" can be useful to keep your
>       repository clean.
{: .checklist}

When you are done, click "submit merge request".


## Reviewing The Merge Request

Now that you've both submitted a merge request, it's time to play
reviewer. If you were tagged with a `@username` in the merge request
you might have even received an email pointing to the request.

Take a look at what your friend wants to change. We encourage you to
explore the options for feedback that this interface offers: right now
you're in the same room but when your collaborators are remote this is
_much_ more convenient than sending an email.

> ## Exercise: Use Fancy Gitlab Merge Request Features
>
> Gitlab offers quite a few features for merge requests. Try to do the
> following:
>  1. Review the "changes" by clicking "changes" tab in the middle of
>     the page
>  2. Make a comment on some line: if you put your mouse over a line
>     on the left side of the changes list, you should be given the
>     option to comment.
>  3. Respond to your friend's comment. Note that you can also add
>     more commits to your local branch and push them if your friend
>     isn't happy with your proposed changes.
>  4. Resolve the discussion. Note that merging your changes is
>     impossible if conversations are unresolved.
>  5. When you are happy with the change your friend proposes, go back
>     to the "discussion" tab and make a comment to document
>     this. Then click the "merge" button.

Your gitlab remote repository should now be updated with your friend's
addition. To get these changes into your `master` branch, you'll have
to copy your local repository, and _then_ merge them. First copy them
with `fetch`.

~~~
git fetch origin
~~~
{: .bash}

Now merge

~~~
git merge origin/master
~~~
{: .bash}


