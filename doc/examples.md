# Examples

For all examples, do load `babette`:

```
library(babette)
```

All examples read the alignment from a FASTA file (usually `my_fasta.fas`) 
and create a BEAST2 input file called `my_beast.xml`.

## Example #1: all default

Using all default settings, only specify a DNA alignment.

![Example #1: all default](pics/all_default.png)

```
posterior <- run_beast2(
  "test_output_0.fas"
)
```

All other parameters are set to their defaults, as in BEAUti.

## Example #2: fixed crown age

Using all default settings, only specify a DNA alignment.

```
[No screenshot, as this cannot be done in BEAUti yet]
```

```
posterior <- run_beast2(
  "my_fasta.fas",
  posterior_crown_age = 15
)
```

`fasta_to_phylo` creates a random phylogeny from
a FASTA file of a certain crown age. 

## Example #3: JC69 site model

![Example #3: JC69 site model](pics/jc69_2_4.png)

```
posterior <- run_beast2(
  "my_alignment.fas",
  site_models = create_jc69_site_model()
)
```

## Example #4: Relaxed clock log normal

![Example #4: Relaxed clock log normal](pics/relaxed_clock_log_normal_2_4.png)

```{r example_4}
posterior <- run_beast2(
  "my_alignment.fas",
  clock_models = create_rln_clock_model()
)
```

## Example #5: Birth-Death tree prior

![Example #5: Birth-Death tree prior](pics/birth_death_2_4.png)

```{r example_5}
posterior <- run_beast2(
  "my_alignment.fas",
  tree_priors = create_bd_tree_prior() 
)
```

## Example #6: Yule tree prior with a normally distributed birth rate

![Example #6: Yule tree prior with a normally distributed birth rate](pics/birth_rate_normal_2_4.png)

```{r example_6}
posterior <- run_beast2(
  "my_alignment.fas",
  tree_priors = create_yule_tree_prior(
    birth_rate_distr = create_normal_distr()
  ) 
)
```

Thanks to Yacine Ben Chehida for this use case

## Example #7: HKY site model with a non-zero proportion of invariants

![Example #7: HKY site model with a non-zero proportion of invariants](pics/hky_prop_invariant_0_5_2_4.png)

```{r example_7}
posterior <- run_beast2(
  "my_alignment.fas",
  site_models = create_hky_site_model(
    gamma_site_model = create_gamma_site_model(prop_invariant = 0.5)
  )
)
```

Thanks to Yacine Ben Chehida for this use case

## Example #8: Strict clock with a known clock rate

![Example #8: Strict clock with a known clock rate](pics/strict_clock_rate_0_5_2_4.png)

```{r example_8}
posterior <- run_beast2(
  "my_alignment.fas",
  clock_models = create_strict_clock_model(
    clock_rate_param = create_clock_rate_param(value = 0.5)) 
)
```

Thanks to Paul van Els and Yacine Ben Chehida for this use case.

## Example #9: Two alignments

![Example 9: Two alignments](pics/anthus_2_4.png)

```{r example_9}
posterior <- run_beast2(
  c("anthus_aco.fas", "anthus_nd2.fas")
)
```

Thanks to Paul van Els for this use case and supplying these FASTA files.

## Example #10: Two alignments, different site models

![Example 10: Two alignments, different site models](pics/aco_hky_nd2_tn93.png)

```{r example_10}
babette::posterior <- run_beast2(
  c("anthus_aco.fas", "anthus_nd2.fas"),
  site_models = list(
    create_hky_site_model(), 
    create_tn93_site_model()
  )
)
```

Since `v1.12` this it is supported to have two alignments with different site models, clock models and tree priors.

Thanks to Paul van Els for this use case.

## Example #11: Two alignments, shared clock model

[Example 11: shared clock model](aco_nd2_same_clock_model.png)

```{r example_10}
babette::posterior <- run_beast2(
  c("anthus_aco.fas", "anthus_nd2.fas"),
  clock_models = list(
    create_strict_clock_model(id = "anthus_aco"), 
    create_strict_clock_model(id = "anthus_aco")
  )
)
```

From `v1.13`, it will be supported to have two alignments with shared site models, clock models and tree priors.

Thanks to Yacine Ben Chehida for this use case.
