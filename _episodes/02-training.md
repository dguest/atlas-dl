---
title: "M'learn some higgs regression"
teaching: 10
exercises: 10
objectives:
- "Train a NN for higgs regression"
questions:
- "How do I train NNs"
keypoints:
- "This part should be pretty easy"

hidden: false
---

> ## Setting up your environment
>
> I like to run these simple tests on my laptop natively, but if for
> whatever reason you can't do that, you can run all this within an
> image.
>
> We'd recommend you run
>
> ~~~
> docker pull atlasml/ml-base:py-3.7.2
> ~~~
> {: .bash}
>
> to get an image to start with
{: .prereq}


## What are we trying to do?

The idea here is to regress on the true higgs pt based on some
information that we're storing in the jets. Whether this makes any
sense is something to talk about with physicists, but we just want to demonstrate the workflow here.

## Get the training / plotting repo

The repository is called [`higgs-regression-training`][hrt]. Clone it
in the `/work` directory.

[hrt]: https://gitlab.cern.ch/deep-sets-example/higgs-regression-training

> ## Launching into another image
>
> If you need a docker image to run python 3, Keras, etc, you can get it
> by going to the `work` directory and running.
>
> ~~~
> docker run --rm -it -v ${PWD}:/home/atlas/data atlasml/ml-base:py-3.7.2
> ~~~
> {: .bash}
{: .callout}

### Making a plot

Try running `draw_regression.py -h` This should prompt you for some
arguments like the H5 file you just produced. Once you've fed in the
right augments it should produce a plot in `plots/` by default. What
we want to do is make this line more diagonal.

## Running the training

Now try running `train_nn.py -h`. If you figure out the right
arguments and feed them to the training script, you should see a lot
of status bars that mean the NN is training. Great! The model will be
saved in `model`.

After you run the training, you should see a few files in a `model`
directory. Run `tree model`:

~~~
model/
├── architecture.json
├── model.png
└── weights.h5
~~~
{: .output}

There are a few files:

 - The `architecture.json` shows the general structure of the model, but
   this is Keras's own special language
 - The elements of the dense layers are stored in the `weights.h5`
 - The more "human readable" format is in `model.png`

Take a look at `model.png` and try to make sense of it.
