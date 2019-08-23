---
title: Setup
questions:
- "What do I need to start?"

---

## Where everything lives

The code for this is stored in gitlab, under
[`deep-sets-example`][dse].

[dse]: https://gitlab.cern.ch/deep-sets-example


## Getting the image you need

I've created a less annoying docker image, but we still require some
local directories to be mounted. Clone
[the `analysisbase-launcher`][launcher] recursively.

The README has instructions. All your data and other work that you
want to use both inside and outside the image should go in the
`/work/` directory.

[launcher]: https://gitlab.cern.ch/deep-sets-example/analysisbase-docker

### Python training image

For most of what we're doing I'd recommend using pip and working on
your local machine, but if you have issues setting that up you can
also use the Atlas Machine Learning Forum's images. You can get a good
starting point by running:

~~~
docker pull atlasml/ml-base:py-3.7.2
~~~
{: .bash}


## Getting the files you need

Unfortunately I couldn't figure out how to do something interesting
with the example file we had, so you'll have to download the one
[from my public area on EOS][dpub].

[dpub]: http://dguest-ci.web.cern.ch/dguest-public/ftag/tutorial/mc16_13TeV.426351.Pythia8EvtGen_A14NNPDF23LO_Ghh_03_3000.deriv.DAOD_FTAG5.e7358_s3126_r10201_p3870/
