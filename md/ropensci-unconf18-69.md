# [Synthetic Dataset Generation](https://github.com/ropensci/unconf18/issues/69)

> state: **open** opened by: **laderast** on: **5/16/2018**

I know that @sckott has done the &#x60;charlatan&#x60; package, which does some basic generation of patient variables. When we teach learning with biomedical data, we often need to use synthetic datasets because we can&#x27;t use datasets with protected health information (PHI). Hence, I&#x27;ve had to generate patient datasets, but they need to have realistic dependencies, such as patients who don&#x27;t have hypertension are not being treated for hypertension.

I have been generating synthetic data with Bayesian networks, which allow you to encode dependencies and structural zeroes in the data by specifying the conditional probability tables (CPTs), which is how you control the degree of association between variables. I have found that tuning these CPTs is a bit of an art.

The strength of this approach is that you can encode the degree of association of variables with outcome.

Would generalizing this be of interest to people? 

### Comments

---
> from: [**laderast**](https://github.com/ropensci/unconf18/issues/69#issuecomment-389596574) on: **5/16/2018**

You can see the general approach here: https://laderast.github.io/cvdRiskData/
---
> from: [**maelle**](https://github.com/ropensci/unconf18/issues/69#issuecomment-389605545) on: **5/16/2018**

Could https://github.com/kkholst/lava help?
---
> from: [**laderast**](https://github.com/ropensci/unconf18/issues/69#issuecomment-389615549) on: **5/16/2018**

@maelle interesting...I don&#x27;t know much about structural equation modeling, but it seems like a nice approach, especially the graphing
---
> from: [**maelle**](https://github.com/ropensci/unconf18/issues/69#issuecomment-389629523) on: **5/16/2018**

I haven&#x27;t used it, but I heard a talk about it and remembered thinking I&#x27;d like to try it next time I needed to simulate a dataset for sample size calculation (in epidemiology). So not much experience with it 😁 
