# Predicting Soil Lead Levels from XRF Readings using Co-Regionalized Gaussian Processes
**A Cost-Effective Method for Detecting Hazardous Lead Levels in Soil**  

**Note**: This is just an overview of the project. For detailed analysis, methodologies, and insights, refer to the main [report](https://github.com/jaredwins99/xrf-soil-predictions/blob/main/Report.pdf).

---

## File Overview

- Data: hand-imputed into a coordinate-system from maps
- [Preprocessing & Exploratory Data Analysis](https://github.com/jaredwins99/xrf-soil-predictions/blob/main/Preprocessing%20%26%20Exploratory%20Data%20Analysis.ipynb): includes data formatting, descriptive statistics, and non-spatial statistical analysis
- [Main Gaussian Process Regression](https://github.com/jaredwins99/xrf-soil-predictions/blob/main/Main%20Gaussian%20Process%20Regression.ipynb): includes main Bayesian modeling, posterior inference, MCMC approximation, and results
- [Report](https://github.com/jaredwins99/xrf-soil-predictions/blob/main/Report.pdf)
- Squared Exponential Kernel GP Regression: repeat of Main Gaussian Process Regression, just with a different kernel
- Exponential Kernel GP Regression: repeat of Main Gaussian Process Regression, just with a different kernel

---

## Introduction
This project aims to assess the reliability of X-Ray Fluorescence (XRF) sampling in detecting elevated lead levels in the soil at a hazard site, a pressing concern for a Massachusetts environmental clean-up agency.

---

## Data, Exploratory Analysis, & Methods
The dataset consists of: approximately forty physical soil samples and around one hundred and fifty XRF samples, both in parts per million (PPM). 
Samples lie on an equidistant grid, and for statistical analysis, location data was encoded with a relative distance from an arbitrary center. 
Key findings from the exploratory analysis include spatial autocorrelation, correlation between XRF and soil samples, and a theoretically-justified log-transformation.

---

## Modeling
- Gaussian processes (GPs) captured the clustered distribution of lead in soil. 
- Modeling involved two kernels and five parameters, with each parameter coming from a prior distribution. 
- Within the model is XRF samples' hypothesized dependence on soil lead level samples’.

---

## Optimization & Inference
- The PyMC library was used to perform Bayesian inference. 
- The No-U-Turn Sampler (NUTS) was used to approximate the model’s intractable posterior. 
- To speed up convergence, hyperparameters were initialized to reasonable values.

---

## Evaluation
The model was evaluated using three prediction types:
1. Predicting XRF and soil sample values for held-out test data at locations with readings.
2. Predicting XRF and soil sample values for locations without readings.
3. Predicting soil sample values using XRF values (giving the model access to true XRF information) for held-out test data at locations with readings.

(In the report it is explained as two types of prediction, with one of the prediction types having two sub-categories.)

The Matern52 kernel provided the best results after comparisons with the exponential kernel and the exponentiated quadratic kernel. 

---

## Conclusion
- There is reasonably compelling evidence supporting the use of XRF sampling as a reliable method for predicting lead levels in the soil. 
- The project showcases the correlation between XRF samples and soil samples, the model's promising fit, and the benefits of accounting for geospatial location in statistical analysis.
- Future research could explore similar geospatial datasets to further validate XRF's utility, as well as validate the reliability of Gaussian process regressions in leveraging proxy measures to make robust predictions.

---

## Appendix
- **Table 1**: Provides more values and correlations.
- **Graph 1 & 2**: Display variance and other parameters.
- **Graph 3**: Reflects the predicted values.
- **Graph 4 & 5**: Visual representation of the difference in predictions for XRF vs. soil samples.
- **Graph 6 & 7**: Comparison of predictions using different kernels.

---


