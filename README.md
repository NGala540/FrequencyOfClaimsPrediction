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
**Chosen model:** in progress

**Explenation:** in progress

**Metrics:** in progress

**Other models:** in progress

## Potential improvements
