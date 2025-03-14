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
**Chosen model:** Zero Inflated Poisson Model

**Explenation:** based on 

**Metrics:** MSE = 

**Other models:** in progress

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
|5.0|	0.33|	4.0|	12.0|	52.0|	50.0|	824.0|	D|	B1|	Regular|	R91|	15.151515|0.054610|
|4.0|	0.27|	5.0|	9.0|	23.0|	90.0|	6924.0|	E|	B3|	Diesel|	R11|	14.814815|0.100919|
|5.0|	0.41|	4.0|	12.0|	52.0|	50.0|	824.0|	D|	B1|	Regular|	R91|	12.195122|0.054610|
|3.0|	0.27|	5.0|	7.0|	40.0|	51.0|	403.0|	C|	B2|	Diesel|	R91|	11.111111|0.056296|
|3.0|	0.30|	4.0|	1.0|	71.0|	50.0|	42.0|	A|	B12|	Regular|	R52|	10.000000|0.082729|
|3.0|	0.32|	4.0|	10.0|	24.0|	90.0|	1955.0|	D|	B1|	Regular|	R94|	9.375000|0.113255|
|3.0|	0.36|	4.0|	2.0|	57.0|	50.0|	1217.0|	D|	B4|	Regular|	R82|	8.333333|0.077179|
|3.0|	0.36|	6.0|	12.0|	56.0|	101.0|	9307.0|	E|	B1|	Diesel|	R82|	8.333333|0.121981|
|3.0|	0.36|	4.0|	7.0|	31.0|	68.0|	1974.0|	D|	B2|	Diesel|	R54|	8.333333|0.081385|

#### Lowest claims frequency
|ClaimNb|	Exposure|	VehPower|	VehAge|	DrivAge|	BonusMalus|	Density|	Area|	VehBrand|	VehGas|	Region|	ClaimFrequency| Ptredicted ClaimFrequency|
|-------|---------|---------|-------|--------|------------|--------|------|---------|-------|-------|---------------|--------------------------|
|0.0|	0.005464|	6.0|	15.0|	50.0|	50.0|	29.0|	A|	B2|	Diesel|	R24|	0.0|0.051645|
|0.0|	0.670000|	6.0|	15.0|	50.0|	50.0|	29.0|	A|	B2|	Diesel|	R24|	0.0|0.051645|
|0.0|	0.890000|	6.0|	8.0|	30.0|	68.0|	48.0|	A|	B1|	Diesel|	R53|	0.0|0.072744|
|0.0|	0.100000|	6.0|	8.0|	30.0|	57.0|	48.0|	A|	B1|	Diesel|	R53|	0.0|0.062307|
|0.0|	0.200000|	7.0|	4.0|	44.0|	50.0|	56.0|	B|	B14|	Diesel|	R24|	0.0|0.064355|
|0.0|	0.170000|	6.0|	10.0|	49.0|	95.0|	26.0|	A|	B3|	Diesel|	R24|	0.0|0.099524|
|0.0|	1.000000|	6.0|	4.0|	33.0|	50.0|	16.0|	A|	B1|	Diesel|	R24|	0.0|0.059074|
|0.0|	1.000000|	7.0|	8.0|	31.0|	50.0|	17.0|	A|	B5|	Diesel|	R24|	0.0|0.057957|
|0.0|	1.000000|	7.0|	12.0|	46.0|	50.0|	126.0|	C|	B5|	Diesel|	R24|	0.0|0.060066|
|0.0|	1.000000|	6.0|	11.0|	55.0|	50.0|	67.0|	B|	B1|	Diesel|	R24|	0.0|0.058400|


### The variable that most differentiates the predicted claim frequency for the GLM class model
For the GLM model, the variable differentiating the predicted claim frequency the most is ... with the coefficient of ... and marginal effect for mean values of ...
