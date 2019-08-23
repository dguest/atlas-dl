---
title: "More Ideas"
---

There are a lot of things we should try!

For example:

 - The NN might have an easier time learning `true_pt /
   pt_reconstructed`, can you feed in the pt ratios and try to compute
   it as well?
 - We didn't normalize the inputs at all. NNs train slightly more
   easily if you feed them gaussian inputs. There are a few ways to
   accomplish this.
     + You could use pt ratios rather than raw pt, i.e. subjet pt /
       large jet pt, or (for the target) truth pt / reconstructed pt
     + You can use functions like log or just linear scaling


And then, there are many things we did _wrong_!

 - You should use a training, validation, and testing set, but for
   that we'd need a bit more time and data.
 - You never implemented this in a real analysis! Booo. There's more
 information in [mlbnn][mlbnn]

[mlbnn]: https://github.com/dguest/mlbnn
