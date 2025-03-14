# Frequency of claims prediction

## Problem
This project aims to develop a predictive model for claim frequency using historical insurance data. I will analyze key factors influencing claim frequency by leveraging data science techniques, such as policyholder demographics, vehicle characteristics, and historical claim patterns. The ultimate goal is to provide insurers with actionable insights to optimize pricing strategies and improve risk management.

## Introduction

### claim frequency
Understanding and predicting claim frequency is crucial for risk assessment, pricing, and decision-making in the insurance industry. Unlike the probability of a single claim occurrence, claim frequency measures how often claims are made over a period. It is defined as the number of claims divided by the total years of insurance coverage, also known as exposure. For policies active for less than a year, exposure is proportionally adjusted.

### bonus – malus system
In insurance, a bonus–malus system (BMS) is a system that adjusts the premium paid by a customer according to their individual claim history. A bonus is usually a discount in the premium which is given on the renewal of the policy if no claim is made in the previous year. Malus is an increase in the premium if there is a claim in the previous year. The fundamental principle of BMS is that the higher the claim frequency of a policyholder, the higher the insurance costs that on average are charged to the policyholder. This principle is also valid in an insurance arrangement consisting of a high maximum deductible which is common to all policyholders.

## Data Explanation
Data source: R-Package CASDatasets: Frequency analysis of a French Motor Third Party Liability dataset - modified

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
- Density - The density of inhabitants (number of inhabitants per km2) in the city where the driver of the car lives in
- Region - The policy regions in France (based on a standard French classification)


## Results
**Chosen model:** 

Combination of two models:
- Random Forest for classification - RandomForestClassifier(class_weight='balanced', max_depth=20, n_estimators=200, random_state=42)
- XGBoost for regression - XGBRegressor(objective ='reg:squarederror', max_depth = 5, n_estimators = 50, seed = 42)

XGBoost predicts the frequency of a claim when Random Forest classifies observation as positive (client is a "claimer")

**Explanation:** 

The characteristics of the data drive the choice of model. Many zeros suggest that the data may come from two separate generating processes — one for non-claimers and another for potential claimers. Dividing the problem into classification and regression helps separate these two groups, leading to improved prediction accuracy.

The model selection was based on a structure of predicted values very similar to real claim frequency. Even though the Zero-Inflated Poisson model had a lower mean squared error, the model didn't manage to predict 0 properly. Furthermore, the ML model shows bigger potential for improvement.

**Metrics:** 

- Classification Accuracy: 0.85
- Classification Precision: 0.11
- Classification Recall: 0.27
- Classification F1: 0.15
- Classification AUC: 0.58
- Regression RMSE: 0.68
- Combination MSE: 0.35

**Other models:**

1. Zero-Inflated Poisson (ZIP) – The number of claims is a positive integer. Thus, this target can be modelled by a Poisson distribution. It is then assumed to be the number of discrete events occurring at a constant rate in a given time interval. Here, we model the frequency = claim number/exposure, which is still a (scaled) Poisson distribution. Furthermore the Zero-Inflated Poisson model helps separate two groups (claimers, non-claimers), leading to improved prediction accuracy. Even though a strong theory stands behind the model and MSE is better than the chosen model, ZIP didn't manage to predict zeros properly, and its claim frequency was generally lower than expected in a "claimers" group. Therefore, I decided that a combined ML model provides better business value. 
   
2. Zero-Inflated Negative Binomial (ZINB) model – While training, the model ran into an issue with a non-invertible Hessian matrix, which typically signals numerical instability. After digging into it, I found two possible reasons: overfitting (too many variables for the dataset size) and extreme dispersion, making it hard for the model to estimate variance. Since the variance-to-mean ratio (1.92) wasn’t excessively high, I decided to drop ZINB in favor of a standard Negative Binomial (NB) model. NB’s mean-variance relationship already allows it to handle some zero inflation without needing a separate zero-inflation component.
   
3. Negative Binomial (NB) model – To compare performance, I ran a Likelihood Ratio Test (LRT) against a Zero-Inflated Poisson (ZIP) model. Even though NB and ZIP aren’t technically nested, ZIP is the more complex model, and LRT still gives a reasonable comparison. The results showed that ZIP had a better fit.


## Potential improvements
- using imputation method instead deleting rows with missing values
- further feature engineering, exploring additional combinations of data
- create functions for data preprocessing and combine it into pipeline
- use stratified splitting method for train-test datasets
- use MLFlow package for results presentation
- use cloud-based service for model training
- testing other ML algorithms for classification/regression problem
- further hyperparameter tuning
- implementing other balance methods for exogenous variable

## Additional research
### Customer segments for which GLM and ML family model predictions differ the most
Top client segments where model predictions differ the most:
1. Clients in region R24
2. Clients aged 68-87
3. Clients aged 48-57
4. Clients with a vehicle power of 6

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
