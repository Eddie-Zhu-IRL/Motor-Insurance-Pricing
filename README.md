# Insurance Pricing using Generalized Linear Models (GLMs)
## Motor Insurance Pricing using the Norauto Dataset

## Overview

This project demonstrates an end-to-end actuarial pricing workflow using the norauto motor insurance dataset from the CASdatasets package.

The objective is to estimate the expected claim cost for each policyholder by modelling:

- Frequency
- Severity
- Pure Premium
- Gross Premium

The project follows a traditional General Insurance pricing framework by comparing multiple statistical models, selecting the most appropriate models using objective performance measures, and interpreting results from an actuarial perspective.

## Business Problem
Motor insurers must determine premiums that adequately reflect each policyholder's expected future claims while covering operating expenses and generating a target level of profit.

This project demonstrates how Generalized Linear Models (GLMs) can be used to estimate expected claim costs and convert them into insurance premiums. Gross premiums are estimated by incorporating expense loadings and target profit margins into the expected claim costs.

### Pricing Framework
- Pure Premium represents the expected cost of claims for an individual policyholder.
- 
$$
Pure Premium = Frequency * Severity
$$
- Gross Premium is the premium that insurance companies must recover operating expenses and earn an appropriate profit.

$$
Gross Premium = \frac{Pure Premim}{1 - Variable Expense Ratio - Profit Margin}
$$

## Dataset

The Norauto dataset, available through the CASdatasets R package([CASDatasets](https://dutangc.github.io/CASdatasets/index.html)), contains 183,999 observations of automobile insurance policies losses over a one-year period.

| Variable | Description |
|----------|-------------|
| Male | 1 if the policyholder is a male, 0 otherwise |
| Young | 1 if the policyholder age is below 26 years, 0 otherwise |
| DistLimit | The distance limit as stated in the insurance contract: "8000 km", "12000 km", "16000 km", "20000 km", "25000-30000 km", "no limit". |
| GeoRegion | Density of the geographical region (from heaviest to lightest): "High+", "High-", "Medium+", "Medium-", "Low+", "Low-". |
| Expo | Exposure as a fraction of year. |
| NbClaim | claim number |
| ClaimAmount | 0 or the average claim amount if NbClaim > 0. |

## Feature Engineering & Explanatory Data Analysis: Male, Young, DistLimit, GeoRegion
### 1. Feature Engineering: Relevel Factor Variables
DistLimit and GeoRegion are factored with their levels listed below. To improve interpretation and visualisation, both variables were converted into ordered categorical factors based on the descriptions provided by the dataset authors.
This ordering allows trends in claim frequency and severity to be interpreted more intuitively.

![pre](/Figures/pre_relevel.png)

After relevelling, variable DistLimit are in order "8000 km", "12000 km", "16000 km", "20000 km", "25000-30000 km", "no limit". Varibale GeoRegion are in order of "High+", "High-", "Medium+", "Medium-", "Low+", "Low-", which is ordered from heaviest to lightest.

![post](/Figures/post_relevel.png)

### 2. Data Summary
Exploratory analysis was performed to understand relationships between policyholder characteristics and insurance risk.
Summary statistics and visualisations were produced for:
- Male
- Young
- DistLimit
- GeoRegion

![summary](Figure/eda_summary.png)

### 3. Visuals of Frequency
Plots of frequency for each variable are as follows,

**Male**

![male](Figures/freq_male.png)

**Young**

![Young](Figures/freq_young.png)

**DistLimit**

![DistLimit](Figures/freq_distlimit.png)

**GeoRegion**

![GeoResion](Figures/freq_georegion.png)

## Train data & Test Data
Before frequency and severity modelling, relevelled data is split into train and test datasets, with 80% for train data, and 20% for test data.
Dimension for train and test datasets are,

![train_test](Figures/train_test.png)

## Frequency Modelling

Claim frequency was modelled using two Generalized Linear Models:

- Poisson Regression
- Negative Binomial Regression

Model performance was compared using:

- Akaike Information Criterion (AIC)
- Dispersion Statistic

The Poisson model produced the lower AIC while maintaining a dispersion statistic close to one, indicating that it provided the most appropriate fit for the training data.

![aic_dispersion](Figures/freq_perf.png)

## Severity Modelling
Claim severity was modelled using

- Gamma GLM
- Lognormal GLM

Predictive performance was evaluated on the test dataset using Mean Squared Error (MSE).

The Gamma model achieved the lowest MSE and was therefore selected for premium estimation.

![mse](Figures/sev_perf.png)

## Pure Premium


