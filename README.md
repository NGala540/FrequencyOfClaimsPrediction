# Frequency of claims prediction

## Problem
This project aims to develop a predictive model for claim frequency using historical insurance data. I will analyze key factors influencing claim frequency by leveraging data science techniques, such as policyholder demographics, vehicle characteristics, and historical claim patterns. The ultimate goal is to provide insurers with actionable insights to optimize pricing strategies and improve risk management.

## Introduction

### claim frequency
Understanding and predicting claim frequency is crucial for risk assessment, pricing, and decision-making in the insurance industry. Unlike the probability of a single claim occurrence, claim frequency measures how often claims are made over a period. It is defined as the number of claims divided by the total years of insurance coverage, also known as exposure. For policies active for less than a year, exposure is proportionally adjusted.

### bonus – malus system
In insurance, a bonus–malus system (BMS) is a system that adjusts the premium paid by a customer according to their individual claim history. A bonus is usually a discount in the premium which is given on the renewal of the policy if no claim is made in the previous year. Malus is an increase in the premium if there is a claim in the previous year. The fundamental principle of BMS is that the higher the claim frequency of a policyholder, the higher the insurance costs that on average are charged to the policyholder. This principle is also valid in an insurance arrangement consisting of a high maximum deductible which is common to all policyholders.

## Data Explanation
Data source: R-Package CASDatasets

- IDpol - The policy ID
- ClaimNb - Number of claims during the exposure period
- Exposure - The exposure period
- Area - The area code
- VehPower - The power of the car
- VehAge - The vehicle age, in years
- DrivAge - The driver age, in years (in France, people can drive a car at 18)
- BonusMalus - Bonus/malus, between 50 and 350 (<100 means bonus, >100 means malus in France). 
- VehBrand - The car brand (coded categories)
- VehGas - The car gas, Diesel or regular
- Density - The density of inhabitants (number of inhabitants per km2) in the city the driver of the car lives in
- Region - The policy regions in France (based on a standard French classification)


## Results
**Chosen model:** 

ZeroInflatedPoisson Regression Results                    

Dep. Variable:          ClaimFrequency   
No. Observations:               542401
Model:             ZeroInflatedPoisson   
Df Residuals:                   542380
Method:                            MLE   
Df Model:                           20
Date:                 Fri, 14 Mar 2025   
Pseudo R-squ.:                 0.01541
Time:                         12:07:42   
Log-Likelihood:            -1.3359e+05
converged:                        True   
LL-Null:                   -1.3568e+05
Covariance Type:             nonrobust   
LLR p-value:                     0.000

| Feature                             | Coef   | Std Err | Z        | P>|z|  |  0.025,  0.975 |
|--------------------------------------|--------|---------|----------|--------|----------------|
| inflate_const                        | 2.4961 | 0.021   | 116.178  | 0.000  | 2.454  ,  2.538  |
| inflate_num__VehAge                  | 0.2089 | 0.008   | 26.960   | 0.000  | 0.194  ,  0.224  |
| inflate_num__DrivAge                 | -0.2526 | 0.007   | -34.723  | 0.000  | -0.267  ,  -0.238  |
| inflate_num__TransformBonusMalus     | -0.2562 | 0.007   | -37.266  | 0.000  | -0.270  ,  -0.243  |
| inflate_num__TransformDensity        | -0.0421 | 0.010   | -4.054   | 0.000  | -0.062  ,  -0.022  |
| inflate_cat__Area_E                  | 0.0610 | 0.023   | 2.684    | 0.007  | 0.016  ,  0.105  |
| inflate_cat__Area_F                  | 0.1224 | 0.048   | 2.557    | 0.011  | 0.029  ,  0.216  |
| inflate_cat__VehBrand_B12            | 0.2924 | 0.018   | 16.106   | 0.000  | 0.257  ,  0.328  |
| inflate_cat__VehBrand_B5             | -0.1049 | 0.029   | -3.635   | 0.000  | -0.161  ,  -0.048  |
| inflate_cat__VehGas_Regular          | -0.1942 | 0.013   | -14.482  | 0.000  | -0.221  ,  -0.168  |
| inflate_cat__Region_R23              | 0.4735 | 0.072   | 6.581    | 0.000  | 0.333  ,  0.615  |
| inflate_cat__Region_R24              | -0.3662 | 0.024   | -15.238  | 0.000  | -0.413  ,  -0.319  |
| inflate_cat__Region_R25              | -0.2765 | 0.053   | -5.258   | 0.000  | -0.380  ,  -0.173  |
| inflate_cat__Region_R31              | 0.2631 | 0.040   | 6.640    | 0.000  | 0.185  ,  0.341  |
| inflate_cat__Region_R52              | -0.1444 | 0.033   | -4.361   | 0.000  | -0.209  ,  -0.080  |
| inflate_cat__Region_R53              | -0.4804 | 0.031   | -15.379  | 0.000  | -0.542  ,  -0.419  |
| inflate_cat__Region_R54              | -0.1663 | 0.044   | -3.807   | 0.000  | -0.252  ,  -0.081  |
| inflate_cat__Region_R72              | 0.1954 | 0.037   | 5.271    | 0.000  | 0.123  ,  0.268  |
| inflate_cat__Region_R73              | 0.1906 | 0.049   | 3.908    | 0.000  | 0.095  ,  0.286  |
| inflate_cat__Region_R82              | -0.1912 | 0.025   | -7.662   | 0.000  | -0.240  ,  -0.142  |
| inflate_cat__Region_R83              | 0.3597 | 0.088   | 4.105    | 0.000  | 0.188  ,  0.531  |
| inflate_cat__Region_R91              | 0.3777 | 0.037   | 10.329   | 0.000  | 0.306  ,  0.449  |
| inflate_cat__Region_R93              | 0.1596 | 0.026   | 6.115    | 0.000  | 0.108  ,  0.211  |
| inflate_cat__Region_R94              | 0.2946 | 0.082   | 3.573    | 0.000  | 0.133  ,  0.456  |
| const                                | -0.0749 | 0.018   | -4.128   | 0.000  | -0.110  ,  -0.039  |
| num__VehAge                          | 0.0324 | 0.007   | 4.415    | 0.000  | 0.018  ,  0.047  |
| num__DrivAge                         | -0.0759 | 0.007   | -11.211  | 0.000  | -0.089  ,  -0.063  |
| num__TransformBonusMalus             | 0.0761 | 0.006   | 12.588   | 0.000  | 0.064  ,  0.088  |
| cat__Area_D                          | 0.0520 | 0.015   | 3.360    | 0.001  | 0.022  ,  0.082  |
| cat__Area_E                          | 0.0751 | 0.017   | 4.480    | 0.000  | 0.042  ,  0.108  |
| cat__Area_F                          | 0.0922 | 0.037   | 2.490    | 0.013  | 0.020  ,  0.165  |
| cat__VehBrand_B12                    | 0.2593 | 0.017   | 15.144   | 0.000  | 0.226  ,  0.293  |
| cat__VehGas_Regular                  | -0.1055 | 0.012   | -8.504   | 0.000  | -0.130  ,  -0.081  |
| cat__Region_R24                      | -0.2292 | 0.020   | -11.358  | 0.000  | -0.269  ,  -0.190  |
| cat__Region_R25                      | -0.1722 | 0.049   | -3.534   | 0.000  | -0.268  ,  -0.077  |
| cat__Region_R26                      | -0.1175 | 0.052   | -2.267   | 0.023  | -0.219  ,  -0.016  |
| cat__Region_R41                      | -0.2001 | 0.050   | -4.036   | 0.000  | -0.297  ,  -0.103  |
| cat__Region_R52                      | -0.1531 | 0.030   | -5.179   | 0.000  | -0.211  ,  -0.095  |
| cat__Region_R53                      | -0.2912 | 0.028   | -10.571  | 0.000  | -0.345  ,  -0.237  |
| cat__Region_R54                      | -0.1739 | 0.040   | -4.361   | 0.000  | -0.252  ,  -0.096  |
| cat__Region_R73                      | -0.1012 | 0.045   | -2.258   | 0.024  | -0.189  ,  -0.013  |
| cat__Region_R82                      | -0.1069 | 0.021   | -4.997   | 0.000  | -0.149  ,  -0.065  |
| cat__Region_R91                      | 0.1021 | 0.033   | 3.139    | 0.002  | 0.038  ,  0.166  |
| cat__Region_R93                      | 0.0628 | 0.022   | 2.799    | 0.005  | 0.019  ,  0.107  |
| cat__Region_R94                      | 0.2894 | 0.069   | 4.182    | 0.000  | 0.154  ,  0.425  |

**Explenation:** 

The choice of model is driven by the characteristics of the data. A large proportion of zeros suggests that the data may come from two separate generating processes — one for non-claimers and another for potential claimers. The Zero-Inflated Poisson (ZIP) model helps separate these two groups, leading to improved prediction accuracy.

The number of claims is a positive integer. Thus, this target can be modelled by a Poisson distribution. It is then assumed to be the number of discrete events occurring with a constant rate in a given time interval. Here we model the frequency = claim number / exposure, which is still a (scaled) Poisson distribution.

Finally, the model selection was based on a Mean Squared Error (MSE), the Likelihood Ratio Test (LRT), and computational efficiency.

**Metrics:** 

MSE = 

**Other models:**

1. Zero-Inflated Negative Binomial (ZINB) model – While training, the model ran into an issue with a non-invertible Hessian matrix, which typically signals numerical instability. After digging into it, I found two possible reasons: overfitting (too many variables for the dataset size) and extreme dispersion, making it hard for the model to estimate variance. Since the variance-to-mean ratio (1.92) wasn’t excessively high, I decided to drop ZINB in favor of a standard Negative Binomial (NB) model. NB’s mean-variance relationship already allows it to handle some zero inflation without needing a separate zero-inflation component.
2. Negative Binomial (NB) model – To compare performance, I ran a Likelihood Ratio Test (LRT) against a Zero-Inflated Poisson (ZIP) model. Even though NB and ZIP aren’t technically nested, ZIP is the more complex model, and LRT still gives a reasonable comparison. The results showed ZIP had a better fit, so I went with that.
3. Random Forest (classification) + XGBoost (regression) combination – An initial test of this approach resulted in higher Mean Squared Error (MSE) compared to the ZIP model. While this hybrid model has the potential to outperform ZIP with further hyperparameter tuning and data preprocessing, the computational resources required stoped further exploration. As a result, this approach was deprecated.

## Potential improvements
- using imputation method instead deleting rows with missing values
- further feature engineering, exploring additional combinations of data
- create functions for data preprocessing and combine it into pipeline
- use stratified spliting method for train-test datasets
- use MLFlow package for results presentation
- use cloud based service for model training
- testing other ML algorithms for classification / regression problem
- further hiperparameter tuning
- implementing other balance methods for exogenous variable

## Additional reaserch
### Customer segments for which GLM and ML family model predictions differ the most



### Customers with the highest and lowest risk and their predicted claim frequency for the GLM class model

#### Highest claims frequency
|ClaimNb | Exposure | VehPower | VehAge | DrivAge | BonusMalus | Density | Area | VehBrand | VehGas | Region | ClaimFrequency| Ptredicted ClaimFrequency|
|--------|----------|----------|--------|---------|------------|---------|------|----------|--------|--------|---------------|--------------------------|
|5.0|0.33|4.0|12.0|52.0|50.0|824.0|D|B1|Regular|R91|15.151515|0.054610|
|5.0|	0.33|	4.0|	12.0|	52.0|	50.0|	824.0|	D|	B1|	Regular|	R91|	15.151515|0.047506|
|4.0|	0.27|	5.0|	9.0|	23.0|	90.0|	6924.0|	E|	B3|	Diesel|	R11|	14.814815|0.047506|
|5.0|	0.41|	4.0|	12.0|	52.0|	50.0|	824.0|	D|	B1|	Regular|	R91|	12.195122|0.102723|
|3.0|	0.27|	5.0|	7.0|	40.0|	51.0|	403.0|	C|	B2|	Diesel|	R91|	11.111111|0.047506|
|3.0|	0.30|	4.0|	1.0|	71.0|	50.0|	42.0|	A|	B12|	Regular|	R52|	10.000000|0.042753|
|3.0|	0.32|	4.0|	10.0|	24.0|	90.0|	1955.0|	D|	B1|	Regular|	R94|	9.375000|0.089862|
|3.0|	0.36|	4.0|	2.0|	57.0|	50.0|	1217.0|	D|	B4|	Regular|	R82|	8.333333|0.111204|
|3.0|	0.36|	6.0|	12.0|	56.0|	101.0|	9307.0|	E|	B1|	Diesel|	R82|	8.333333|0.167211|
|3.0|	0.36|	4.0|	7.0|	31.0|	68.0|	1974.0|	D|	B2|	Diesel|	R54|	8.333333|0.079642|

#### Lowest claims frequency
|ClaimNb|	Exposure|	VehPower|	VehAge|	DrivAge|	BonusMalus|	Density|	Area|	VehBrand|	VehGas|	Region|	ClaimFrequency| Ptredicted ClaimFrequency|
|-------|---------|---------|-------|--------|------------|--------|------|---------|-------|-------|---------------|--------------------------|
|0.0|	0.005464|	6.0|	15.0|	50.0|	50.0|	29.0|	A|	B2|	Diesel|	R24|	0.0|0.050133|
|0.0|	0.670000|	6.0|	15.0|	50.0|	50.0|	29.0|	A|	B2|	Diesel|	R24|	0.0|0.050133|
|0.0|	0.890000|	6.0|	8.0|	30.0|	68.0|	48.0|	A|	B1|	Diesel|	R53|	0.0|0.079624|
|0.0|	0.100000|	6.0|	8.0|	30.0|	57.0|	48.0|	A|	B1|	Diesel|	R53|	0.0|0.062471|
|0.0|	0.200000|	7.0|	4.0|	44.0|	50.0|	56.0|	B|	B14|	Diesel|	R24|	0.0|0.065780|
|0.0|	0.170000|	6.0|	10.0|	49.0|	95.0|	26.0|	A|	B3|	Diesel|	R24|	0.0|0.136230|
|0.0|	1.000000|	6.0|	4.0|	33.0|	50.0|	16.0|	A|	B1|	Diesel|	R24|	0.0|0.056763|
|0.0|	1.000000|	7.0|	8.0|	31.0|	50.0|	17.0|	A|	B5|	Diesel|	R24|	0.0|0.054351|
|0.0|	1.000000|	7.0|	12.0|	46.0|	50.0|	126.0|	C|	B5|	Diesel|	R24|	0.0|0.059531|
|0.0|	1.000000|	6.0|	11.0|	55.0|	50.0|	67.0|	B|	B1|	Diesel|	R24|	0.0|0.060730|


### The variable that most differentiates the predicted claim frequency for the GLM class model
For the GLM model, the variable differentiating the predicted claim frequency the most is region with the coefficient depending on specific region, but highest in comparison to Region R11 for region 53 of -0.29 and -0.48 for modeling zero inflating process
