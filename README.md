**Authors:** Aylin & Marika
**Date:** 28.10.2026
**Context:** Theoretical Ecology and Evolution Practical 

# Resistance vs. lysogeny: bacterial defense against temperate phages under phage therapy

## About this project
Stochastic, discrete-time simulation of a bacterial population exposed to temperate phages. Bacteria can survive in two ways:
- Resistance: slow but permanent (rare mutation, growth cost)
- Lysogeny: fast but risky. A phage integrates a wild-type cell which becomes a lysogen (= a bacterium that carries the dormant genome of a temperate phage). The prophage can later be induced and kill the cell.
We use this model to test phage therapy: can additional phages be used to eliminate the bacterial population, and does it work equally well against resistant bacteria and lysogens?

The model extends the basic evolutionary rescue model based on Orr & Unckless (2008) introduced in the Theoretical Ecology and Evolution Practical (Bank 2026).

## Project structure
```
project/
├── README.md                  this file
└── THEE_bacteria_phage.Rmd    main notebook (model, simulations, plots)
```

| Piece | What it does |
|---|---|
| `simulate_one_gen()` | Simulates one generation: infection/induction losses, Poisson offspring with logistic growth, multinomial split of wild-type offspring into resistant / lysogenic / wild type, phage update |
| `simulate_pop()` | Repeats `simulate_one_gen()` until extinction or `t_max` and returns population sizes per generation |
| Plot chunk | Plots wild type, resistant, lysogens, phages and total population (ggplot2) |
| Analysis chunk | Runs many replicates over a parameter range and summarizes the outcome |

## Requirements 
- R and RStudio
- R packages: "ggplot2", "tidyr", "dplyr", "tibble"

```r
install.packages(c("ggplot2", "tidyr", "dplyr", "tibble"))
```

## How to run
1. Open "THEE_bacteria_phage.Rmd" in RStudio.
2. Run the chunks from top to bottom, or click "Knit" for an HTML report.
3. Change the parameters in the "population trajectory" chunk to explore other scenarios. The analysis chunk runs many replicates and can be slow.

## Variables and Parameters
| Name | Type | Description | Allowed range | Value |
|:-----|:-----|:------------|:--------------|:------|
| $N_{wt}$ | State variable | Current size of the wild-type bacteria population | integer ≥ 0 | changes over time |
| $N_r$ | State variable | Current size of the resistant bacteria population | integer ≥ 0 | changes over time |
| $N_l$ | State variable | Current size of the lysogenic bacteria population | integer ≥ 0 | changes over time |
| $N_P$ | State variable | Current size of the phage population | ≥ 0 | changes over time |
| `N_init_wt` | Initial condition | Initial size of the wild-type population | positive integer | 100 |
| `N_init_r` | Initial condition | Initial size of the resistant mutant population | integer ≥ 0 | 0 |
| `N_init_l` | Initial condition | Initial size of the lysogenic population | integer ≥ 0 | 0 |
| `N_init_P` | Initial condition | Initial size of the phage population | positive integer | 1 |
| `growth_rate` | Model parameter | Average number of offspring per bacterium (wt, r and l) per generation | ≥ 0 | 1.5 |
| `lysogen_prob` | Model parameter | Probability that a wt bacterium becomes lysogenic | 0 to 1 | 0.002 |
| `mut_rate` | Model parameter | Probability that an offspring of a wt bacterium mutates to resistant | 0 to 1 | 0.002 |
| `infection_prob` | Model parameter | Probability that a wt bacterium is infected by a phage per generation | 0 to 1 | 0.01 |
| `K` | Model parameter | Carrying capacity of the total bacteria population (wt + r + l) | positive integer | 2000 |
| `P_decline` | Model parameter | Fraction of phages decaying every generation (entered as a negative number) | ≤ 0 | -0.5 |
| `P_prod` | Model parameter | Number of new phages produced per infection or induction | ≥ 0 | 1.5 |
| `t_max` | Simulation setting | Number of generations after which the simulation stops (not a model parameter). The simulation also stops automatically if the bacterial population goes extinct | integer > 0 | 2000 |
| `induction_prob` | Varied parameter | Probability (per generation) that a lysogenic bacterium is killed by its own dormant phage | 0 to 1 | varied in the analysis |
| `cost_r` | Varied parameter | Fraction of offspring that resistant bacteria lose compared to wt (fitness cost of resistance) | 0 to 1 | varied in the analysis |



## References
Alexander HK et al. (2014) Evolutionary rescue: linking theory for conservation and medicine. *Evolutionary Applications* 7: 1161-79. DOI:https://doi.org/10.1111/eva.12221

Bank C (2026) Course material: basic evolutionary rescue notebook

Karamlou S et al. (2025) Bacterial resistance to phage therapy: Mechanisms and strategies to overcome it. *Current Molecular Pharmacology* 18: 108-122. DOI:https://doi.org/10.1016/j.cmp.2025.11.003

Orr HA, Unckless RL (2008) TPopulation Extinction and the Genetics of Adaptation. *The American Naturalist* 172(2). DOI:https://doi.org/10.1086/589460
























