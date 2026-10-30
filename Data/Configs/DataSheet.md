# Datasheet - Imperial Capstone Project

## Motivation
**Use :** eight synthetic black-box functions to be optimised. Each one is designed to mimic real-world complexity, with features such as non-linearity and multiple local maxima.

**Purpose :** this is an iterative, real-world-style optimisation task. Each week each student receives one new data point per function based on query submission. The dataset will grow over time (13 new outputs for each function), helping improve modelling and query strategy.

**Created / Supported :** Imperial University 


## Composition

**Dataset Content :** each black box function provides an initial sample of input co-ordinates and relative to the dimensions of the function. These co-ordinates are between 0.000000 and 1.00000 and are stored as hyphen-separated variables rounded to six decimal places. For each set of input co-ordinates the functions produce an output score.
Initial sample provided in eight input files - ‘initial_inputs.npy’ of shape (N,d) and eight output files - ‘initial_outputs.npy’ of shape (N).

| Function    | Dimensions | Descriptions of sample applications|
|----|---|---|
| Function 1 | 2D array | Detects likely contamination sources in a two-dimensional area, such as a radiation field, where only proximity yields a non-zero reading. |
| Function 2 | 2D array | Imagine a black box, or a mystery ML model, that takes two numbers as input and returns a log-likelihood score. Goal is to maximise that score, but each output is noisy, and depending on start position,might get stuck in a local optimum. | 
| Function 3 | 3D array | Working on a drug discovery project, testing combinations of three compounds to create a new medicine. |
| Function 4 | 4D array | Address the challenge of optimally placing products across warehouses for a business with high online sales, where accurate calculations are costly and only feasible biweekly. To speed up decision-making, an ML model approximates these results within hours. The model has four hyperparameters to tune, and its output reflects the difference from the expensive baseline. Because the system is dynamic and full of local optima, it requires careful tuning and robust validation to find reliable, near-optimal solutions.|
| Function 5 | 4D array | Tasked with optimising a four-variable black-box function that represents the yield of a chemical process in a factory. The function is typically unimodal, with a single peak where yield is maximised.|
| Function 6 | 5D array | Optimising a cake recipe using a black-box function with five ingredient inputs, for example flour, sugar, eggs, butter and milk. Each recipe is evaluated with a combined score based on flavour, consistency, calories, waste and cost, where each factor contributes negative points as judged by an expert taster. This means the total score is negative by design. |
| Function 7 | 6D array | Tasked with optimising an ML model by tuning six hyperparameters, for example learning rate, regularisation strength or number of hidden layers. The function being maximised is the model’s performance score (such as accuracy or F1), but since the relationship between inputs and output isn’t known, it’s treated as a black-box function.|
| Function 8 | 8D array | Optimising an eight-dimensional black-box function, where each of the eight input parameters affects the output, but the internal mechanics are unknown. | 


Objective is to find the parameter combination that maximises the function’s output, such as performance, efficiency or validation accuracy. Because the function is high-dimensional and likely complex, global optimisation is hard, so identifying strong local maxima is often a practical strategy.
For example, imagine tuning an ML model with eight hyperparameters: learning rate, batch size, number of layers, dropout rate, regularisation strength, activation function (numerically encoded), optimiser type (encoded) and initial weight range. 

## Collection Process

**Importing the Data into Machine Learning models**
Initial samples are loaded into the ML models from the individual function directories


inputs = np.load('/home/mcevoyj777/_CAPSTONE/FUNCx/initial_inputs.npy')
output = np.load('/home/mcevoyj777/_CAPSTONE/FUNCx/initial_outputs.npy')

Subsequent inputs and outputs are added manually to ML model each week as extra_inputs arrays and extra_outputs arrays and then combined. (If the process was needed in production this part could be automated)

inputs = np.vstack([inputs, extra_inputs])
output = np.append(output, extra_output)

**Generation of next query inputs - Query Generation Strategy**
Initial Phase - to form a better understanding of  the initial data the correlations, mutual information and the total importance score of each of  inputs to the outputs was calculated. (This was repeated every week as new data was added)

**Correlation with Output:**
Input_X    0.132327
Input_Y    0.277218
Input_Z   -0.437098
Input_X Mutual Information Score: 0.0000
Input_Y Mutual Information Score: 0.0000
Input_Z Mutual Information Score: 0.1862
Input_X Total Importance (with interactions): 0.0807
Input_Y Total Importance (with interactions): 0.2076
Input_Z Total Importance (with interactions): 0.7117

**Initial Queries -**  utilising gaussian process surrogates with high exploration parameters to map out more of the unknown space in the functions.
**Consolidation Queries -** utilising the dimensional knowledge from the correlation scores and balancing the need for exploration and exploitation.
**Optimisation Queries -** restricting the searchable space using localised bounds, and reducing the exploration parameters, and matching the acquisition function and kernel to the specific function.


## Preprocessing/Cleaning/Labelling

Preprocessing plays an important role in the process to help focus the model on the right areas to search.
Length scale bound utilised to allow certain dimensions to explore while focus important dimensions on smaller incremental shifts.
Further focus applied by actually setting localised bounds to keep model within the optimising space,

## Dataset Uses
**Intended Uses -** dataset is strictly intended to support the development of optimising machine learning models, which face some of the some issues as real world problems. Providing a fixed query budget forces an accelerated strategic adaption process makes this particular useful in a competitive environment,

**Unintended Uses -** not appropriate for training standard models as the sample sizes are too sparse and the inputs bound within a unit area.


## Distribution & Maintenance
The initial data is provided by the university, and this may be different for each cohort of students. 
Weekly queries are entered via a university portal https://imperial-capstone-r3.emeritus.org/dashboard

Query inputs and outputs are stored within the function ML models.
