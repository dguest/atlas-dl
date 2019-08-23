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

## What are we trying to do?

The idea here is to regress on the true higgs pt based on some
information that we're storing in the jets. Whether this makes any
sense is something to talk about with physicists, but we just want to demonstrate the workflow here.

## Get the training / plotting repo

The repository is called [`higgs-regression-training`][hrt]. Clone it.

[hrt]: https://gitlab.cern.ch/deep-sets-example/higgs-regression-training

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
