# Model Card - Capstone Mutli-Functional Bayesian Optimisation Model with Gaussian Process Surrogate (CMF-BO-GP)
A model card is documentation for ML models. It provides key information about a model’s purpose, design, performance, limitations and ethical considerations. 
## Model Overview
Briefly describe what the model does and who created it

**Model Name :** Mutli-Functional Bayesian Optimisation Model with Gaussian Process Surrogate (MF-BO-GP)
with each model labelled CAP_FUNx

**Version :** Currently 8 versions; 1.0 through to 8.0. 

**Developer(s) :** Imperial College / Emeritus Programme

## Intended Use
What is the model designed do and where should it be used?

**Primary task :** Optimisation of multi-dimensional functions through Bayesian Optimisation

**Target Users :** Fellow students, data scientists and machine learning practitioners

**Recommended Use cases :** Solving black box maximisation problem. Finding the input combination that maximises the output, 
using a limited set of queries and an initial data set

**Not Intended for :** Large scale optimisation problems

## Training Data

**Data Sources :** Initial data provided via .npy files
initial_inouts.npy, which contains the input combination tried so far
initial_outputs.npy, which contains the corresponding ouputs

Also provided with a description of each function and it's real-world analogy

Subsequent inputs are derived from the optimisation process. These are entered into the university portal,
with the corresponding outputs provided back within 24-48 hours.
The initial and Subsequent inputs and output are combined and the optimisation are rerun and refined.

**Size of data set :**
| Function | Data Points | Dimensions | Initial Scale Ratio | Final Scale Ratio |
|---|---|---|---|---|
| Function 1 | 10 | 2D Array | 10:2 ~ 5 | 23:2 ~ 11.5 |
| Function 2 | 10 | 2D Array | 10:2 ~ 5 | 23:2 ~ 11.5 |
| Function 3 | 15 | 3D Array | 15:3 ~ 5 | 28:3 ~ 9.333 |
| Function 4 | 30 | 4D Array | 30:4 ~ 7.5| 43:4 ~ 10.75 |
| Function 5 | 20 | 4D Array | 20:4 ~ 5 | 33:4 ~ 8.25 |
| Function 6 | 20 | 5D Array | 20:5 ~ 4 | 33:5 ~ 6.6 |
| Function 7 | 30 | 6D Array | 30:6 ~ 5 | 43:6 ~ 7.167 |
| Function 8 | 40 | 8D Array | 40:8 ~ 5 | 53:8 ~ 6.625 |

New data added each week (for 13 weeks)

**Pre-processing Steps :** Preprocessing plays an important role in the process to help focus the model on the right areas to search.
Length scale bound utilised to allow certain dimensions to explore while focus important dimensions on smaller incremental shifts.
Further focus applied by actually setting localised bounds to keep model within the optimising space,

**Model Methodology :** Across the iterative rounds the approach develops from an Exploration focus to an Exploitation focus.
Initial Queries -  utilising gaussian process surrogates with high exploration parameters to map out more of the unknown space in the functions.
Consolidation Queries - utilising the dimensional knowledge from the correlation scores and balancing the need for exploration and exploitation.
Optimisation Queries - restricting the searchable space using localised bounds, and reducing the exploration parameters, and matching the acquisition function and kernel to the specific function.

## Evaluation Metrics

**Metrics Used :** the primary measure of success is current maximum output for each output.
The secondary measure (being tracked for the final optimisations) of performance was the change from the previous maximum and how that compared to the model prediction

**Performance Results :**
| Function | Base Score | Best Score | Query of Best |
|---|---|---|---|
| Function 1 | 0.000000000000 | 1.9508262577166 | Query 6 |
| Function 2 | 0.6112052157614 | 0.6204482195028 | Query 9 |
| Function 3 | -0.0348353133501| -0.0155718899148 | Query 7 |
| Function 4 | -4.0255422819082 | 0.5481902259004 | Query 1 |
| Function 5 | 1,088.8596181962700 | 8,662.4825000000000 | Query 6 |
| Function 6 | -0.7142649478202 |-0.1626039117877  | Query 4 |
| Function 7 | 1.3649683044992 | 2.6317852796995 | Query 9 |
| Function 8 | 9.5984820025663 | 9.9341808061485 | Query 8 |


## Ethical Considerations

**Potential biases or risks :**
The optimisation path is heavily biased by the choice of the 10 to 40 initial points provided in the .npy files.
If the initial dataset fails to capture a representative range of the function's landscape, 
the models may permanently exclude entire sub-regions of the search space, potentially leading to suboptimal or narrow conclusions.

**Mitigation Strategies :**
To offset the impact of potentially biased initial data points the first phase of the process intentionally sets
the model into high exploration mode through dynamic beta scheduling and utilising local optimisers such as (L-BFGS-B)
which initialise from 50 to 1090 random starts.

**Privacy concerns :** no privacy concerns due to the synthetic nature of the data

## Model Life cycle

**Date of last update :** October 2026 (Milestone 9)

**Version Control :** Current models CAP_FUN1.0 through to CAP_FUN8.0. 

**Monitoring Plan :** Convergence behaviours is mapped weekly through performance graphs.

