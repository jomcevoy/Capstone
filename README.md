# Capstone

### Section 1: Project Overview

#### ◼. Black Box Optimisation

This repository houses the Black-Box Optimisation (BBO) Capstone Project. The purpose of this project is to develop, benchmark, and deploy sample-efficient optimisation frameworks designed for complex, real-world systems.In many advanced engineering and scientific applications, the underlying system behaves as a "black box": we can observe its outputs for given inputs, but we do not possess an analytical mathematical formula to describe its inner workings. Furthermore, these systems lack gradient information, are highly non-linear, contain noisy outputs, and are incredibly resource-intensive or expensive to evaluate. This project provides a systematic, algorithmic alternative to inefficient manual tuning and brute-force searching.

#### ⟁ . Goal of the Capstone Project

The primary objective of this project is to locate the global optimum (maximum or minimum) of an expensive black-box function using the absolute minimum number of system evaluations. To achieve this, the project focuses on designing an automated pipeline that balances exploration (gathering data in uncharted regions of the parameter space to reduce uncertainty) and exploitation (honing in on known high-performing regions to locate the peak). The ultimate benchmark of success is achieving a state-of-the-art objective score while drastically minimizing the computational or financial overhead.

#### Real World Applications - in the real world, engineers rarely work with clean, differentiable functions and BBO is a mechanism that bridges advanced statistical theory with high-impact industry applications such as..

Hyperparameter tuning in NL Models
Drug discovery
Recommendation systems
Reinforcement Learning (AI agents, robotics).
 

#### ⟳ Principle of Black Box Optimisation

Instead of guessing randomly or evaluating a rigid, wasteful grid of points, BBO implements an iterative feedback loop driven by data-driven probability. The system relies on two core components.

A surrogate model that constructs a probabilistic approximation of the true objective function, capturing both its predicted value and the uncertainty around that prediction.
An acquisition function that uses the surrogate model’s predictions and uncertainty metrics to calculate a "utility score" across the entire search space, pinpointing where the next system evaluation should take place.
 

#### ⟐ . Capstone project supports my current or future career

For a Commercial Finance Director, a Black-Box Optimisation (BBO) framework is the ultimate decision-support engine, and will become a powerful tool as businesses become more complex and competitive.

In corporate finance, you constantly face "black-box" problems: complex business environments where you know the inputs (price changes, marketing spend, inventory levels) and you can measure the outputs (revenue, EBITDA, customer churn), but the exact mathematical relationship between them is unknown, chaotic, and heavily exposed to market noise.

 

### Section 2: Inputs and Outputs

#### ⟤.⟥ State the model’s interface

The pipeline connects to the black-box engine using a input-output application . For each of the eight projects, the machine learning system has an initial sample set of inputs and outputs and application provides the subsequent inputs provided and outputs are feedback through personalised emails.

#### ⟢. What are the inputs and outputs

There are eight BBO functions that have between 2 and 8 features. 

The inputs to each function are continuous numeric values that lie within the range 0 to 1. After the initial sample inputs are provided the user based inputs are limited to 6 significant digits. Example provided below.

Functions
**Input Examples**
Function 1:0.616162-0.646465

Function 2:0.000000-0.400000

Function 3:0.813402-1.000000-0.850601

Function 4:0.435949-0.443948-0.243355-0.439113

Function 5:0.476092-0.995411-1.000000-1.000000

Function 6:0.892895-0.772634-0.937451-0.406290-0.360158

Function 7:0.000000-0.267792-0.069571-0.000000-0.227411-0.803541

Function 8:0.000000-0.399074-0.123214-0.112487-0.679719-0.634021-0.180101-0.801376

The outputs are generated based on the user inputs and are provided soon after  inputs are submitted. Example from a different week provided below.

**Output Examples**
| Function | Output |
| --- | --- |
| Function 1 | 0.000021365074638137203 |
| Function 2 | -0.04250067518679212 |
| Function 3 | -0.17955537260329268 |
| Function 4 | 0.5481902259003815 |
| Function 5 | 2998.5110568875957 |
| Function 6 | -1.2679820129946602 |
| Function 7 | 1.3627627244158926 | 
| Function 8 | 8.7983052999894 |



### Section 3 - Challenge objectives

#### ⊚ Capstone Challenge

This Black Box Optimisation (BBO) Capstone project (a course or project undertaken by a student as a culmination of work towards a diploma/certificate) is an effective way to develop and test students' practical understanding of the course material. The project mimics a Bayesian optimisation-style competition, in which we are trying to discover the maximum of eight unknown functions, also known as black-box functions. There are no equations or visuals of these functions up front – just some initial data and the ability to make smart guesses.

Each function simulates a real-world task such as radiation detection, robot control or drug discovery, where evaluations are expensive or limited. The project provides an opportunity to apply the various ML tools from the course and intelligent search strategies in a realistic ML challenge. Perfect solutions were not expected, but rather encouraged to demonstrate a sound experimental process throughout the capstone project, and an introduction to supporting documentation (datasheets, modelcards) as well the wonders of git. The core algorithm used for this project was Bayesian Optimisation utilising a surrogate model. This has proved a powerful technique in its own right but is also clearly an important tool for the tuning of the multi-dimensional hyperparameters found in large language models (LLM), 

The overarching objective was - Solving black box maximisation problems. Finding the input combinations that maximises the output, using a limited set of queries and an initial training data set. Coming from a maths/finance background I default to trying to understand the data, and so for each function I calculated feature correlations (how each feature individually relates to the output score), mutual information (the extent to which features overlap information) and importance score (how much weight, influence, or predictive power a specific feature has within the function). From these results, in most cases I was able to represent each function in 2 key dimensions so that I could visualise them.


 

### Section 4 - Technical approach

#### ⫸ Core Strategy

The core strategy treats the challenge as a sequential decision-making problem under uncertainty, using Bayesian Optimisation as an efficient way to find the global optimum (maximum or minimum) of an expensive-to-evaluate, black-box function. 

The overall strategy was to break the exercise into three phases; Because we already possess the initial data sets, we can immediately construct a surrogate model (Gaussian Process) to create a probability distribution (mean and variance) over the possible functions, providing a prediction; and how confident it is about that prediction.

Phase 1 - Exploration (Queries 1-4) - in the exploration phase we encourage the algorithm to target critical blind spots—especially large unmapped gaps sitting right next to high-performing historical data points. Spending any more query budget on exploration, (particularly in the high dimensional functions) would likely be unproductive.

Phase 2 - Trade Offs  (Queries 5-10) - in the trade off phase we encourage the algorithm to use the dimensional statistics we continue to calculate along with its historic results through an acquisition function; to balance exploring areas where the variation is high with filling in the gaps with the highest scoring zones. In this phase the search space bounds (where it can search) and the search length scales  (how big its moves are) are actively tightened based on our ongoing dimensional statistics.

Phase 3 - Deep Exploitation  (Queries 11-13) - in the final phase we encourage the algorithm to ignore anything but the highest performing regions and to change input parameters by tiny increments to to pinpoint the exact peak of the underlying function.


There is more of an emphasis on Exploration in the initial queries; for UCB queries this means increasing the multiplier (kappa) of the standard deviation to give more weight to areas of higher variance, and for EI queries increasing the margin of performance threshold xi. 

Based on the analysis each function has specific characteristics that need to be considered.

Function 1 (Radiation) : utilising a matern kernel which is better at dealing with spiky functions

Function 2 (Log-Likelihood) : input values clustered along a diagonal corridor; look to probe the boundaries of the input spaces to test for clipping or edge constraints.

Function 3 (Drug) : possesses a single feature of high importance, with the objective score increasing along this single dimension.

Function 4 (Dynamic) : surprising positive output on the first query, contrasting sharply with previous negative baselines. Need to try to investigate the dynamic nature of the function. 

Function 5 (Chemical) & Function 6 (Cake) : both these functions have two dominant features of importance. Initially focus exploration on those planes.

Function 7 (Hypertune) and Function 8 (BBO) : have significant sparsity and random exploration may yield little results. Focus will be on finding specific ML methods for this level of sparsity.

 **Configuration Documents**
 * **Data Sheet**: [DataSheet](Data/Configs/DataSheet.md)
 * **Model Card**: [Model_Card](Data/Configs/Model_card.md)

  **Supporting Documents**
 * **Week 1**: [12](Data/Subs/12.md)
 * **Week 2**: [13](Data/Subs/13.md)
 * **Week 3**: [14](Data/Subs/14.md)
 * **Week 4**: [15](Data/Subs/15.md)
 * **Week 5**: [16](Data/Subs/16.md)
 * **Week 6**: [17](Data/Subs/17.md)
 * **Week 7**: [18](Data/Subs/18.md)
 * **Week 8**: [19](Data/Subs/19.md)
 * **Week 9**: [20](Data/Subs/20.md)
 * **Week 10**: [15](Data/Subs/21.md)
 * **Week 11**: [16](Data/Subs/22.md)
 * **Week 12**: [15](Data/Subs/23.md)
 * **Week 13**: [16](Data/Subs/24.md)
 * **Week 14a**: [Retrospective](Data/Subs/25.md)
 * **Week 14b**: [Successful Strategies](Data/Subs/25(2).md)
