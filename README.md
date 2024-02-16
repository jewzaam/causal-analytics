# causal-analytics



### General Naming Convention

- v variables - are the treatments. They can be binary or continuous. In the case of continuous abs(beta) defines thier magnitude;

- y - is the outcome variable. The generating equation is, y = normal(0, stddev_outcome_noise) + t @ beta [where @ is a numpy matrix multiplication allowing for beta be a vector]

- W variables - Common Causes. Commonly cause both the treatment and the outcome and are iid. if continuous, they are Norm(mu = Unif(-1,1), sigma = 1)

- Z variables - Instrument variables. Each one affects all treatments. i.e. if there is one instrument and two treatments then z0->v0, z0->v1

- X variables - effect modifiers. If continuous, they are Norm(mu = Unif(-1,1), sigma = 1) [x -> y]

- FD variables - Front door variables, v0->FD0->y

### Data generation module

Refer: https://www.pywhy.org/dowhy/v0.11.1/dowhy.html#module-dowhy.datasets

#### Function
dowhy.datasets.linear_dataset(beta, num_common_causes, num_samples, num_instruments=0, num_effect_modifiers=0, num_treatments=None, num_frontdoor_variables=0, treatment_is_binary=True, treatment_is_category=False, outcome_is_binary=False, stochastic_discretization=True, num_discrete_common_causes=0, num_discrete_instruments=0, num_discrete_effect_modifiers=0, stddev_treatment_noise=1, stddev_outcome_noise=0.01, one_hot_encode=False)[source]
Generate a synthetic dataset with a known effect size.

This function generates a pandas dataFrame with num_samples records. The variables follow a naming convention where the first letter indicates its role in the causality graph and then a sequence number.

##### Parameters

- beta (int or list/ndarray of length num_treatments of type int) – coefficient of the treatment(s) (‘v?’) in the generating equation of the outcome (‘y’).

- num_common_causes (int) – Number of variables affecting both the treatment and the outcome [w -> v; w -> y]

- num_samples (int) – Number of records to generate

- num_instruments (int) – Number of instrumental variables [z -> v], defaults to 0

- num_effect_modifiers (int) – Number of effect modifiers, variables affecting only the outcome [x -> y], defaults to 0

- num_treatments – Number of treatment variables [v]. By default inferred from the beta argument. When provided, beta is recycled to match num_treatments.



##### Returns:
Dictionary with pandas dataFrame and few other metadata variables.
- ”df”: pd.dataFrame with num_samples records. The variables follow a naming convention were the first letter indicates its role in the causality graph and then a sequence number.

- v variables - are the treatments. They can be binary or continuous. In the case of continuous abs(beta) defines thier magnitude;

- y - is the outcome variable. The generating equation is, y = normal(0, stddev_outcome_noise) + t @ beta [where @ is a numpy matrix multiplication allowing for beta be a vector]

- W variables - commonly cause both the treatment and the outcome and are iid. if continuous, they are Norm(mu = Unif(-1,1), sigma = 1)

- Z variables - Instrument variables. Each one affects all treatments. i.e. if there is one instrument and two treatments then z0->v0, z0->v1

- X variables - effect modifiers. If continuous, they are Norm(mu = Unif(-1,1), sigma = 1)

- FD variables - Front door variables, v0->FD0->y

- ”treatment_name”: str/list(str) “outcome_name”: str “common_causes_names”: str/list(str) “instrument_names”: str/list(str) “effect_modifier_names”: str/list(str) “frontdoor_variables_names”: str/list(str) “dot_graph”: dot_graph, “gml_graph”: gml_graph, “ate”: float, the true ate in the dataset

### Causal Nomenclature

These names are understood:
- common causes
- instrument variables
- effect modifier
- front door variables
- treatment
- outcome

But, we need to understand a little more of causal lingo which is understood well by the causal community :
- Confounders
- Back door
- Modifier
- Colliders 

