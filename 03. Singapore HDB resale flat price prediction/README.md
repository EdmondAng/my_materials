# Project Title: Prediction of HDB Resale Flat Prices

## Problem Statement

ABC Estate Management asked for a predictive model with $R^{2}$ > 0.8 to be developed to help its estate agents to more accurately value Housing Development Board (HDB) resale flat prices. The developed model will help the company to reduce manual efforts and human errors, in turn reducing the number of violations of the national Code of Ethics by the company.

## Methodology

1. Create baseline training and test data:
    * Using the training and test data found at [Kaggle](https://www.kaggle.com/competitions/dsi-sg-project-2-regression-challenge-hdb-price/overview), clean and curate a suitable set of baseline features for HDB resale flat prices
2. Create a baseline model:
    * Fit and evaluate a baseline linear regression model on the curated dataset
3. Create an improved model:
    * Further curate the number of features by filtering for more significantly correlated features to the resale price, using Pearson correlation coefficients
    * Cross-validate 4 different models (linear regression, lasso cross-validation, ridge cross-validation, elastic net cross-validation) on the curated datasets
4. Predict using the best model:
    * Based on the cross-validation scores, pick the best model and size of dataset. Thereafter, fit and evaluate model RMSE performance on Kaggle.

## Conclusion

The objective was achieved: a RidgeCV model of $R^{2}$ score of 0.9 was developed for ABC Estate Agency. A minimal data cleaning framework was also proposed to maintain the best model result.

1. Findings:
    * The RidgeCV model used on full hdb_train_df gave the best model result
    
2. Areas for future improvement:
    * The dataset can be improved by adding several other factors that are intuitively impactful to HDB resale flat prices, such as:
        * Demand and supply data (e.g. number of unsold HDB resale flats (representing supply), number of HDB resale transactions per time period (representing demand))
        * Cooling measures (e.g. duration of wait-out period for private homeowners before purchasing HDB resale flats, loan-to-value limit for HDB loans etc.)
        
## Input and Output Datasets

Due to the upload size limit of Github, the datasets are uploaded separately and can be accessed via Google Drive [here](https://drive.google.com/drive/folders/1bC2_wfMBnoyfjtmfqtWhFZZ0KouIJDs-?usp=share_link).