# [Tensorflow Probability in R](https://github.com/ropensci/unconf18/issues/21)

> state: **open** opened by: **michaelquinn32** on: **4/11/2018**

Earlier today, Google announced TensorFlow Probability: a probabilistic programming toolbox for machine learning. The full text of the announcement is available on [Medium](https://medium.com/tensorflow/introducing-tensorflow-probability-dca4c304e245)

See the article for full details, but at a high level.

- TF Probability provides an incredibly flexible language for specifying models imperatively
- You work with distributions as first class objects
- When it comes time to fit your model, TFP has a host of tools (like MCMC and variational inference) to get the job done

This [notebook](https://github.com/tensorflow/probability/blob/master/tensorflow_probability/examples/jupyter_notebooks/Linear_Mixed_Effects_Models.ipynb) provides an end-to-end walkthrough on fitting a linear mixed effects model using the InstEval data from lme4. 

For this project, unconf participants should come up with a design for how TF Probability will work in R, referring to RStudio&#x27;s work on [keras](https://tensorflow.rstudio.com/keras/) and [tfestimators](https://tensorflow.rstudio.com/tfestimators/). Participants will be able to write some of these wrappers, and should hope to complete some example notebooks before the end of the event. It would be great if we could do an R version of the notebook linked above, and maybe others too.

R already has other probabilistic programming languages, in Stan, and there are other R projects that try to build up a probabilistic programming language for TensorFlow (Greta). But this will be the primary Google-supported project in this area, with a lot of new features coming soon.

### Comments

---
> from: [**goldingn**](https://github.com/ropensci/unconf18/issues/21#issuecomment-381301516) on: **4/14/2018**

Yeah, it&#x27;s awesome that the folks at Google are pulling all of these bits together!

By the way, &#x60;greta&#x60; already uses parts of &#x60;probability&#x60; (the distributions), and will be providing greta-like interfaces to the inference methods going forward (and we&#x27;ll be trying to keep up with the new developments). These and some other variational inference and stochastic gradient MCMC methods should start appearing in the development version of &#x60;greta&#x60; over the next couple of months.

&#x60;greta&#x60; provides a higher-level interface than the modules in &#x60;probability&#x60; though; so it&#x27;s necessarily more limited and I think making it easy for people to use &#x60;probability&#x60; directly in R is a great idea! We could even make the resulting package a dependency of &#x60;greta&#x60;&#x27;s.

Though I can&#x27;t quite envisage how a more R-like &#x60;probability&#x60; interface would fit in between &#x60;greta&#x60; and the interface to &#x60;probability&#x60; provided by the [R &#x60;tensorflow&#x60; API](https://tensorflow.rstudio.com/tensorflow/articles/using_tensorflow_api.html), since the interface to &#x60;probability&#x60; is lower-level than keras or estimators. What sort of functionality do you have in mind?
---
> from: [**michaelquinn32**](https://github.com/ropensci/unconf18/issues/21#issuecomment-381804788) on: **4/16/2018**

First of all, hi Nick!

Sorry, I didn&#x27;t realize you were attending the unconf, but I&#x27;m really excited to meet and work with you. TBH, I got permission to come to the unconf because I was planning to attend the event to do something &quot;Tensorflow related,&quot; but working on Greta definitely falls under that umbrella! If that&#x27;s the big &#x60;TFP&#x60;  project, I&#x27;d be really happy.

Full disclosure, I&#x27;m not a &#x60;TFP&#x60; developer, my work at Google is on something else entirely, but I do contribute to the R infrastructure used by everyone. With that caveat out of the way, I see &#x60;greta&#x60; fitting into the [&#x60;TFP&#x60; stack](https://cdn-images-1.medium.com/max/1400/0*19BJhsJ-2DzQ7fFH.) the same way that &#x60;edward2&#x60; does, as a language for building models. I had assumed that we&#x27;d be wrapping &#x60;edward2&#x60; when working in &#x60;TFP&#x60; during the unconf, but there is no reason to stick to that plan.

Anyway, it&#x27;s really great to meet you! And I&#x27;m really looking forward to collaborating.
---
> from: [**goldingn**](https://github.com/ropensci/unconf18/issues/21#issuecomment-381827054) on: **4/16/2018**

Hi Michael :)

Oh great. Well I&#x27;d be very happy to collaborate on anything tensorflowy!

There are tons of things to be done on greta, so happy to go down that route. But also very happy to work on another TFP project.

A couple of things that spring to mind: easily dispatching parallel MCMC chains to separate Cloud ML jobs (Id love this for greta, hence my interest in parallel progress bars); using greta&#x27;s R -&gt; TF syntax mapping to enable speedups/parallelisation/GPU support when evaluating arbitrary R functions; a sort of TF estimators-like containerisation of greta/TFP models, so that they can be easily wrapped up to have train() and predict() methods, and possibly support online learning with an update_training() method or something.


---
> from: [**mmulvahill**](https://github.com/ropensci/unconf18/issues/21#issuecomment-389039053) on: **5/15/2018**

Hi @michaelquinn32 &amp; @goldingn! 

I&#x27;m new to Greta &amp; TensorFlow, but they&#x27;re both on my list of tools to learn.  I&#x27;d be interested in working on a TFP/greta project if I could be helpful.   

On a related note, where does &#x60;TFP&#x60;/&#x60;greta&#x60; stand on varying dimension methods like reversible jump and birth-death MCMC?   My impression is most probabilistic languages/tools tend not to feature varying dimension methods like reversible jump and birth-death since they add significant complexity to MCMC.  I&#x27;ve been working on a collection of birth-death MCMC models for reproductive endocrinology research for a while -- recently have been refactoring them from C to C++/R -- so I have a keen interest in whether &#x60;TFP&#x60; supports birth-death ;)
---
> from: [**goldingn**](https://github.com/ropensci/unconf18/issues/21#issuecomment-389041020) on: **5/15/2018**

@mmulvahill that&#x27;s great! Sounds like a team is coming together :)

We should try to distill this down into a tangible project (or a few, in separate issues) so folks can decide what to do next week.

I suspect the short answer to your Q is that they can&#x27;t do that because the tensorflow graph is static, not dynamic. That said there&#x27;s almost always a way of hacking in that behaviour, and there are extensions like [fold](https://github.com/tensorflow/fold), which would work. greta&#x27;s current API is even more static than Tensorflow (since all array dimensions are fixed), but that could potentially be generalised in the future. This would be a great thing to discuss at the unconf!
---
> from: [**goldingn**](https://github.com/ropensci/unconf18/issues/21#issuecomment-389041138) on: **5/15/2018**

Any particular angles on tfp/greta that look like they would be interesting and feasible to make progress on in a couple of days?
---
> from: [**goldingn**](https://github.com/ropensci/unconf18/issues/21#issuecomment-389041490) on: **5/15/2018**

P.S. the greta [dev branch](https://github.com/greta-dev/greta/commits/dev) (which will become greta 0.3) now depends on TFP, and directly uses TFP&#x27;s samplers
---
> from: [**michaelquinn32**](https://github.com/ropensci/unconf18/issues/21#issuecomment-389380919) on: **5/15/2018**

I like the progress on the dev branch Nick!

Thus far, my work with TFP has been trying to implement (derivatives of) provided materials. I really enjoyed playing with this:
https://github.com/tensorflow/probability/blob/master/tensorflow_probability/examples/jupyter_notebooks/Linear_Mixed_Effects_Models.ipynb

It&#x27;s a relatively simple model, but has a really interesting approach to inference: using an EM algorithm that both applies a sample and an optimizer.

Implementing that would be a big job for those couple of days and a lot of fun to work on. Hacking on the sampler would (hopefully) add some nice abstractions for customizing inference. I saw hmc was in the dev branch already (AWESOME!!!), but there are like a million samplers popping up in TFP these days.
https://github.com/tensorflow/probability/tree/master/tensorflow_probability/python/mcmc

Stepping further back, having some sort of abstraction for how inference happens could eventually lead greta to supporting VI too. I don&#x27;t think we should implement it yet (considering this is way out of my depth and VI looks a bit like black magic to me*), but it would be nice to be able to make that step once there are a few more implementations out there in the wild.

* But I did get VI to work in edward1 once, FWIW. The examples here were pretty straightforward: http://edwardlib.org/getting-started



---
> from: [**goldingn**](https://github.com/ropensci/unconf18/issues/21#issuecomment-389787411) on: **5/17/2018**

Yeah, that&#x27;s a great demo of what TFP can do!

We actually have some prototype VI code (for Stein VGD) that&#x27;ll be added to greta soon; though probably after next month&#x27;s release of 0.3. We&#x27;ll also be adding minibatching and other nice things that @martiningram has been working on.

The dev branch changes have rejigged greta to have an (internal) inference class from which samplers and optimisers inherit, so the various VI approaches will be added as a third inference option. That generalisation of the inference structure also means its easy to add the other TFP samplers (and TF optimisers). I&#x27;m planning to hook up the MH and MALA samplers in the next release. I might even do that on the plane over to Seattle this weekend :)

So developing and adding new inference methods would definitely be feasible.
---
> from: [**michaelquinn32**](https://github.com/ropensci/unconf18/issues/21#issuecomment-390079624) on: **5/17/2018**

Separately, I noticed that Greta doesn&#x27;t yet support tfp transformed distributions and bijectors:

* https://www.tensorflow.org/api_docs/python/tf/contrib/distributions/TransformedDistribution
* https://www.tensorflow.org/api_docs/python/tf/distributions/bijectors/Bijector

Bijectors are an abstraction for transforming distributions. For example, in tfp you create the log normal distribution by transforming the normal distribution.

&#x60;&#x60;&#x60;
import tensorflow_probability as tfp
tfd &#x3D; tfp.distributions
tfb &#x3D; tfp.distributions.bijectors

log_normal &#x3D; tfd.TransformedDistribution(
  distribution&#x3D;tfd.Normal(loc&#x3D;0., scale&#x3D;1.),

  # The bijector encaspulates several different transformations together
  bijector&#x3D;tfb.Exp(),
  name&#x3D;&quot;LogNormalTransformedDistribution&quot;)
&#x60;&#x60;&#x60;

You can do some crazy stuff with bijectors. See this notebook, for example:
https://github.com/tensorflow/probability/blob/master/tensorflow_probability/examples/jupyter_notebooks/Gaussian_Copula.ipynb

A full implementation might take time, but it wouldn&#x27;t hurt to get started on this during the unconf.
---
> from: [**goldingn**](https://github.com/ropensci/unconf18/issues/21#issuecomment-390088932) on: **5/18/2018**

I think bijectors is at a lower level than the greta user API. greta deliberately doesn&#x27;t let users mess around with distributions and densities directly, since (even if bijection was handled) that relies on users understanding things like log jacobian transformations, (which most users won&#x27;t) and can easily lead to incorrectly specified models.

Of course having lower-level APIs is useful (and you can always do the low-level TFP stuff in R by importing TFP with reticulate), it&#x27;s just out of scope for greta.


