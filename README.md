**Authors:** Aylin & Marika
**Date:** 28.10.2026
**Context:** Theoretical Ecology and Evolution Practical 

# Resistance vs. lysogeny: bacterial defense against temperate phages under phage therapy

## About this project
Stochastic, discrete-time simulation of a bacterial population exposed to temperate phages. Bacteria can survive in two ways:
- Resistance: slow but permanent (rare mutation, growth cost)
- Lysogeny: fast but risky. A wild-type cell is infected and becomes a lysogen (= a bacterium that carries the dormant genome of a temperate phage). The prophage can later be induced and kill the cell.
We use this model to test phage therapy: can additional phages be used to eliminate the bacterial population, and does it work equally well against resistant bacteria and lysogens?

The model extends the basic evolutionary rescue model (Orr & Unckless) introduced in the course.

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
2. Run the chuncks from top to bottom, or click "Knit" for an HTML report.
3. Change the parameters in the "population trajectory" chunck to explore other scenarios. The analysis chunck runs many replicates and can be slow.

## Parameters
| Parameter | Meaning |
|---|---|
| `growth_rate` | mean offspring per bacterium per generation |
| `infection_prob` | infection probability of wild type per phage |
| `induction_prob` | probability that a symbiont is killed by its own phage |
| `symbiosis_prob` | probability that a wild-type cell becomes symbiotic |
| `mut_rate` | probability of mutation to resistance |
| `cost_r` | growth cost of resistance (0 = none, 1 = maximal) |
| `K` | carrying capacity |
| `P_decline`, `P_prod` | phage decay and phages produced per infection/induction |
| `t_max` | maximum number of generations |

## References
- Orr & Unckless (2008), Population extinction and the genetics of adaptation.
- Course material: basic evolutionary rescue notebook (Claudia Bank).






















