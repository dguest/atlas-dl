---
title: "Dump an H5 File"
teaching: 10
exercises: 10
objectives:
- "Get a data file you can use"
questions:
- "How do I get data to Keras"
keypoints:
- "We always reformat our data before M'Learnin"

hidden: false
---

## Get your credentials etc

The script in the `analysisbase-launcher` expects that your key is in
`~/.ssh/id_rsa`. If you don't want to use this you can run
`make-key.sh` and copy the output into your gitlab SSH keys.


## Building the dumper

You can load up the image by running `./run-docker.sh` script. This
should (hopefully) drop you into a working image. I've added most of
the annoying setup stuff to the `.bashrc` so you should be ready to
clone and build.

Clone and build the dumper with

~~~
ssh://git@gitlab.cern.ch:7999/deep-sets-example/higgs-regression-dumper.git
~~~
{: .bash}

Then make a build directory and build it.


## Producing an output file

You'll have to run something like

~~~
./AnalysisPayload ../data/DAOD_FTAG5.p3870.pool.root
~~~
{: .bash}

Your path may be something else.

This will produce an output file called `jets.h5`. Let's take a look
at it:

~~~
h5ls -v jet.h5
~~~
{: .bash}

This prints a lot of information:

~~~
Opened "jets.h5" with sec2 driver.
jets                     Dataset {18757/Inf}
    Location:  1:1552
    Links:     1
    Chunks:    {2048} 24576 bytes
    Storage:   225084 logical bytes, 201354 allocated bytes, 111.79% utilization
    Filter-0:  deflate-1 OPT {7}
    Type:      struct {
                   "GhostHBosonsPt"   +0    native float
                   "GhostBHadronsFinalPt" +4    native float
                   "pt"               +8    native float
               } 12 bytes
subjets                  Dataset {18757/Inf, 5/5}
    Location:  1:800
    Links:     1
    Chunks:    {2048, 5} 122880 bytes
    Storage:   1125420 logical bytes, 517620 allocated bytes, 217.42% utilization
    Filter-0:  deflate-1 OPT {7}
    Type:      struct {
                   "pt"               +0    native float
                   "rnnip_pb"         +4    native float
                   "JetFitter_mass"   +8    native float
               } 12 bytes
~~~
{: .output}

We'll be trying to learn `GhostHBosonPt` from the other
variables. Note that `subjets` is a 2d array, we're saving all the
subjets in each large-R higgs jet.
