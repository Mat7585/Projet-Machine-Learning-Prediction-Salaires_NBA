# NBA Salary Prediction (1985–2018)

## Objective
Predict NBA player salaries for a given season using player performance and context from previous seasons.
From data extraction and cleaning to salary prediction.

## Dataset
- Source: Kaggle — NBA Player Salaries (1985–2018) : https://www.kaggle.com/datasets/ulrikthygepedersen/nba-player-salaries/data?select=salaries_1985to2018.csv
- Main files: `salaries_1985to2018.csv` &  `players.csv`

## Approach
### Data preparation
1/ import datasets and explore  

2/ merge the two datasets `salaries_1985to2018.csv` &  `players.csv`  

3/ The dataset mixes season-level variables (1 row = 1 season) and career-level variables. Using these career variables for a season-level prediction would create temporal leakage (the model “sees” future information). Therefore, the solution is to predict the salary over the entire career. So, only keep the variables that are specific to the entire career and aggregate them when necessary.  

4/ Data cleaning: removed non-informative/redundant columns, standardized data types, and converted key fields (height, weight, draft pick) into model-ready numeric features. Prepared categorical variables for encoding and exported a cleaned dataset for modeling.  

5/ Imputation of missing values using appropriate replacement strategies, and removal of columns with excessive missingness.  

6/ Outlier detection and capping when necessary to limit the impact of extreme values.  

7/ Encoded categorical features into numerical representations (e.g., one-hot encoding) for model compatibility.  


...



### Supervised Machine Learning stage
I will test two machine learning models: linear regression and XGBoost.  

### Data transformation stage
I tested a log transformation on the target variable (Y) and applied StandardScaler, but it did not significantly improve the results.  

### Results
<img width="797" height="90" alt="image" src="https://github.com/user-attachments/assets/2055fe62-bccf-4782-bc08-838ef904da4d" />

##Conclusion & improvements
...
