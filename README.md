# Predictive Modeling & Feature Selection 
SFU Stat452 Fall2025 Project 
 
## Overview 
This repository contains the methodology and summary of a machine learning prediction task. The primary objective of this project was to develop a highly accurate predictive model for a continuous, bimodal response variable (Y) using a high-dimensional dataset of 19 numeric predictors (X1,..., X19).  The model's performance was evaluated strictly on the Mean Squared Prediction Error (MSPE) against an unseen test dataset. 
<img width="50%" alt="image" src="https://github.com/user-attachments/assets/943b2f39-a9c3-4923-98a8-25ddb22dc3da" />
 
## Academic Integrity Notice 
To maintain compliance with course policies regarding academic integrity, the source code and raw datasets in this repository are password-archived. 

## Methodology & Workflow 
This project utilized a 3-stage predictive modeling approach: 
1. Exploratory Data Analysis (EDA) & Preprocessing: Conducted distributional analysis (skewness, kurtosis) and applied strategic transformations (logarithmic, square root) to normalize right- and left-skewed predictors. Extreme outliers were clipped at the 1st and 99th percentiles to stabilize the model without discarding data.

  <img width="50%" alt="image" src="https://github.com/user-attachments/assets/6088f323-7404-4282-9b67-e9e6779ac039" />
   
2. Feature Selection: Evaluated the relationship between Y and individual predictors using LOESS smoothing curves. Combined visual analysis with Random Forest (Ranger) permutation importance scoring to isolate the 9 most significant predictors out of the original set, effectively reducing dimensionality and noise.

  <img width="50%" alt="image" src="https://github.com/user-attachments/assets/c92091e9-de6e-4d76-b43f-7fa89644c049" />

3. Hyperparameter Tuning & Validation: Optimized the Random Forest model using a binary search grid approach to evaluate different mtry and min.node.size parameters. Evaluated configurations using a 10-fold Cross-Validation repeated 3 times to ensure stability, minimize standard error, and prevent overfitting.

  <img width="30%" alt="image" src="https://github.com/user-attachments/assets/064740de-92a7-4eea-bf70-6b04b07c5ae6" />


## Final Model Configuration 
The final deployed model is a Random Forest Regressor optimized for complex, non-linear data distributions. 
- Algorithm: Random Forest (ranger package). 
- Trees: 1,000. 
- Features Used: Top 9 optimized variables. 
- Performance: Achieved an Out-of-Bag (OOB) prediction error of approximately 13.85 and an R-squared of 0.630 on the training set. 

<img width="70%" alt="image" src="https://github.com/user-attachments/assets/4cc457b4-523f-4fc2-bf80-c2b9e58d6793" />

<img width="50%" alt="image" src="https://github.com/user-attachments/assets/9b9dc545-02fe-4ce3-939c-bbca5abdddb9" />

## Alternative Approach: 2-Stage Segmentation Modeling
To address the bimodal nature of the response variable, I also experimented with a 2-stage mixture architecture. This involved splitting the data into Lower & Upper segments using a classification ranger, and then fitting independent regression models to each cluster. 

Why it wasn't the final model: A 13% classification error caused massive squared penalties, making the conservative single-stage Random Forest mathematically safer for minimizing the final MSPE. 

## Technology Stack
- Language: R 
- Key Libraries: tidyverse (dplyr, ggplot2, tidyr, purrr) for data manipulation and visualization, ranger for fast random forest implementation. 
