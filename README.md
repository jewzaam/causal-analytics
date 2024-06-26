# causal-analytics

This repository is inspired by thoughts in here:

1. [Causal inference in statistics: An overview](https://ftp.cs.ucla.edu/pub/stat_ser/r350.pdf)
1. [An Introduction to Causal Inference - PMC](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2836213/)
1. [The Book of Why: The New Science of Cause and Effect – Pearl and Mackenzie](http://bayes.cs.ucla.edu/WHY/why-ch1.pdf)

And concrete implementation of [doWHy](https://github.com/py-why/dowhy)

The goal is to make problem debugging in any domain simpler than what it is today.

### Naming Convention followed in Causal literature

- v variables - are the treatments. They can be binary or continuous. In the case of continuous abs(beta) defines thier magnitude;

- y - is the outcome variable. The generating equation is, y = normal(0, stddev_outcome_noise) + t @ beta [where @ is a numpy matrix multiplication allowing for beta be a vector]

- W variables - Common Causes. Commonly cause both the treatment and the outcome and are iid. if continuous, they are Norm(mu = Unif(-1,1), sigma = 1)

- Z variables - Instrument variables. Each one affects all treatments. i.e. if there is one instrument and two treatments then z0->v0, z0->v1

- X variables - effect modifiers. If continuous, they are Norm(mu = Unif(-1,1), sigma = 1) [x -> y]

- FD variables - Front door variables, v0->FD0->y

### Causal Nomenclature describing effects of variables

These names are understood:
- common causes
- instrument variables
- effect modifier
- front door variables
- treatment
- outcome

But, we need to understand a little more how some of them affect the causal pathway. To desribe that, causal community groups them by :
- Confounders
- Back door
- Modifier
- Colliders 

