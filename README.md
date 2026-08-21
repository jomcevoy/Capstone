# Capstone

**Section 1: Project Overview**

**◼. Black Box Optimisation**

This repository houses the Black-Box Optimisation (BBO) Capstone Project. The purpose of this project is to develop, benchmark, and deploy sample-efficient optimisation frameworks designed for complex, real-world systems.In many advanced engineering and scientific applications, the underlying system behaves as a "black box": we can observe its outputs for given inputs, but we do not possess an analytical mathematical formula to describe its inner workings. Furthermore, these systems lack gradient information, are highly non-linear, contain noisy outputs, and are incredibly resource-intensive or expensive to evaluate. This project provides a systematic, algorithmic alternative to inefficient manual tuning and brute-force searching.

**⟁ . Goal of the Capstone Project**

The primary objective of this project is to locate the global optimum (maximum or minimum) of an expensive black-box function using the absolute minimum number of system evaluations. To achieve this, the project focuses on designing an automated pipeline that balances exploration (gathering data in uncharted regions of the parameter space to reduce uncertainty) and exploitation (honing in on known high-performing regions to locate the peak). The ultimate benchmark of success is achieving a state-of-the-art objective score while drastically minimizing the computational or financial overhead.

**Real World Applications** - in the real world, engineers rarely work with clean, differentiable functions and BBO is a mechanism that bridges advanced statistical theory with high-impact industry applications such as..

Hyperparameter tuning in NL Models
Drug discovery
Recommendation systems
Reinforcement Learning (AI agents, robotics).
 

**⟳ Principle of Black Box Optimisation**

Instead of guessing randomly or evaluating a rigid, wasteful grid of points, BBO implements an iterative feedback loop driven by data-driven probability. The system relies on two core components.

A surrogate model that constructs a probabilistic approximation of the true objective function, capturing both its predicted value and the uncertainty around that prediction.
An acquisition function that uses the surrogate model’s predictions and uncertainty metrics to calculate a "utility score" across the entire search space, pinpointing where the next system evaluation should take place.
 

**⟐ . Capstone project supports my current or future career**

For a Commercial Finance Director, a Black-Box Optimisation (BBO) framework is the ultimate decision-support engine, and will become a powerful tool as businesses become more complex and competitive.

In corporate finance, you constantly face "black-box" problems: complex business environments where you know the inputs (price changes, marketing spend, inventory levels) and you can measure the outputs (revenue, EBITDA, customer churn), but the exact mathematical relationship between them is unknown, chaotic, and heavily exposed to market noise.

 

**Section 2: Inputs and Outputs**

**⟤.⟥ State the model’s interface**

The pipeline connects to the black-box engine using a input-output application . For each of the eight projects, the machine learning system has an initial sample set of inputs and outputs and application provides the subsequent inputs provided and outputs are feedback through personalised emails.

**⟢. What are the inputs and outputs**

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

Function 1:
0.000021365074638137203

Function 2:
-0.04250067518679212

Function 3:
-0.17955537260329268

Function 4:
0.5481902259003815

Function 5:
2998.5110568875957

Function 6:
-1.2679820129946602

Function 7:
1.3627627244158926

Function 8:
8.7983052999894



Section 3 - Challenge objectives

⊚ Capstone Callenge

This capstone challenge mimics a Bayesian optimisation-style competition, in which the objective is to find the maximum of eight unknown functions, also known as black-box functions. There is no insight into the equations or visuals of these functions up front – just some initial data and the ability to make smart guesses.

Each function simulates a real-world task such as radiation detection, robot control or drug discovery, where evaluations are expensive or limited. The goal is to find the inputs that give the highest possible output for each function. Every function has been constructed as a maximisation problem (if the real life problem was a minimisation problem then the features have been applied as negatives.)

The challenge lasts 13 weeks; this reflects the constraints where evaluations are expensive and data may be limited,

 

Section 4 - Technical approach

⫸ Core Strategy

The core strategy treats the challenge as a sequential decision-making problem under uncertainty, using Bayesian Optimisation as an efficient way to find the global optimum (maximum or minimum) of an expensive-to-evaluate, black-box function. 

The Initial Strategies (Queries 1-3)

Prior to submitting any user queries a detailed review of the initial sample data and outputs were analysed to understand the relative importance of features and to where possible review visually the initial output values.

There is more of an emphasis on Exploration in the initial queries; for UCB queries this means increasing the multiplier (kappa) of the standard deviation to give more weight to areas of higher variance, and for EI queries increasing the margin of performance threshold xi. 

Based on the analysis each function has specific characteristics that need to be considered.

Function 1 (Radiation) : utilising a matern kernel which is better at dealing with spiky functions

Function 2 (Log-Likelihood) : input values clustered along a diagonal corridor; look to probe the boundaries of the input spaces to test for clipping or edge constraints.

Function 3 (Drug) : possesses a single feature of high importance, with the objective score increasing along this single dimension.

Function 4 (Dynamic) : surprising positive output on the first query, contrasting sharply with previous negative baselines. Need to try to investigate the dynamic nature of the function. 

Function 5 (Chemical) & Function 6 (Cake) : both these functions have two dominant features of importance. Initially focus exploration on those planes.

Function 7 (Hypertune) and Function 8 (BBO) : have significant sparsity and random exploration may yield little results. Focus will be on finding specific ML methods for this level of sparsity.

 Reply Reply to Comment
