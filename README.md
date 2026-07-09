# Insurance Pricing using Generalized Linear Models (GLMs)
## Motor Insurance Pricing using the Norauto Dataset

## Overview

This project demonstrates an end-to-end actuarial pricing workflow using the norauto motor insurance dataset from the CASdatasets package.

The objective is to estimate the expected claim cost for each policyholder by modelling:

Claim Frequency
Claim Severity
Pure Premium
Gross Premium

The project follows a traditional General Insurance pricing framework by comparing multiple statistical models, selecting the most appropriate models using objective performance measures, and interpreting results from an actuarial perspective.

$$
Pure Premium = Frequency * Severity
$$

$$
Gross Premium = \frac{Pure Premim}{1 - Variable Expense Ratio - Profit Margin}
$$
