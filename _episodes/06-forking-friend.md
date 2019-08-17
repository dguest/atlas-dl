---
title: "Modifying your friend's code"
teaching: 10
exercises: 15
objectives:
- "Make a friend"
- "Build and run your friend's code"
- "Add kinematic cuts"
questions:
- "How do I run someone else's code?"
keypoints:
- "You can (and usually will) start with someone else's code"

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
before. Do this from the `Bootcamp` directory:

~~~
git clone path/to/friends/repo
~~~
{: .bash}

you should now have two directories containing code: the one you
created and the one you just forked.

## Building (and running) your friend's code

Let's build your friend's code now. We'll start by deleting the
previous build directory: in principal this isn't necessary but having
many build directories around can get confusing. Then we'll make a new
one.

~~~
rm -r build
mkdir build
~~~
{: .bash}

Next we'll build their repository as we did before

~~~
cd build
cmake ../friends-repo
make
~~~
{: .bash}

Assuming everything went ok, you should be able to run their
`AnalysisPayload`.

> ## Backup Plan
>
> If your friend was adventurous and wrote something which you can't
> easily compile, they can also fork the [pre-workshop example][prework]
> which will allow you to _fork their fork_. The goal of this exercise is
> to make a merge request to _something_ which they own.
{: .callout}

[prework]: https://gitlab.cern.ch/usatlas-computing-bootcamp/v1-prework-finished-code/tree/master

## Adding Kinematic Cuts

We used a very loose selection in the initial examples. In a more
realistic analysis you'd only be selecting jets with a specific pt,
eta range etc. Since we're working collaboratively, we'll have you add
these cuts to your friend's repository.

### Duplicating histograms

Before we do that let's add another set of histograms so we can make
both selections at the same time. Go through `AnalysisPayload` and
create a second set of histograms where you've replaced `*_raw` with
`*_kin`, i.e.

~~~
  TH1D *h_njets_raw = new TH1D("h_njets_raw","",20,0,20);
~~~
{: .source}

should become

~~~
  TH1D *h_njets_raw = new TH1D("h_njets_raw","",20,0,20);
  TH1D *h_njets_kin = new TH1D("h_njets_kin","",20,0,20);
~~~
{: .source}

Recompile the code just to make sure there are no obvious issues.

### Adding a selection

Now let's add some selection requirements. Somewhere in your code you
might already be creating a `std::vector<xAOD::Jet>` and filling it
with all the jets in the event. Add a second container which will only
be filled with your selection. Then fill this with all the jets with
pt greater than 50 GeV.

Your code should end up _somthing like_ this:

~~~
    std::vector<xAOD::Jet> jets_kin;
    for(const xAOD::Jet* jet : *jets) {
      // perform kinematic selections and store in vector of "selected jets"
      if(jet->pt() > 50e3){
        jets_kin.push_back(*jet);
      }
    }
~~~
{: .source}

Now fill two histograms with this selection: one for `n_jets` and one
for the invariant mass of the leading two jets.

Finally, recompile and _try_ to run the code. Take a look at the
resulting histograms, are they what you'd expect?


## Committing on a branch

Conceptually branches in git are nothing more than a bookmark pointing
at the most recent in a line of commits. As such they are very
lightweight to create and you should use them liberally.

You should _always_ create a branch when you make a merge request.
Since you're requesting that a very specific set of changes be
reviewed and merged, you don't want any further development you add to
`master` to be pushed into the request.

If this seems a bit confusing that's fine, it should be more clear in
the near future.

For now, create a new branch and commit your changes:

~~~
cd friends-repo
git checkout -b change-cuts
git add AnalysisPayload.cxx
git commit -m "change cuts in AnalysisPayload" -m "more detailed explanation of your changes"
~~~
{: .bash}

In the next episode we'll learn to push this to your fork and make a
merge request.
