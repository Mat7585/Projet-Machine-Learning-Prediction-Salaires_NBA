# NBA Salary Prediction (1985–2018)

## Objective
The initial goal of this project was to predict NBA player salaries season by season using player performance and contextual information from previous seasons.
However, during the data exploration phase, I realized that the dataset contains a mix of season-level variables and career-level variables. Using career-level information to predict a specific season would introduce temporal leakage, as the model would have access to future information.
To avoid this issue, I reframed the problem and instead predicted the total salary over a player's entire career, using only variables that are consistent with this level of aggregation.

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

7/ Applied one-hot encoding to categorical features for the Linear Regression model. This preprocessing was not necessary for XGBoost, as it can handle categorical features natively when enable_categorical=True is used.


...



### Supervised Machine Learning Stage

I trained and compared two regression models: Linear Regression and XGBoost.

### Data Transformation Stage

I first built a baseline Linear Regression model without any transformation.

Exploratory Data Analysis showed that the target variable (salary) is highly right-skewed:
<img width="1046" height="880" alt="image" src="https://github.com/user-attachments/assets/43c4300e-62e1-4d6d-97ce-9f0da182c3c1" />

To address this, I tested a log transformation of the target variable. I also applied StandardScaler to the features because several variables have very different scales.

These transformations were tested on the Linear Regression model, but they did not lead to a significant improvement in performance.

For XGBoost, I kept the log-transformed target variable, while feature scaling was not applied, as it is generally not required for tree-based models.

### Results
<img width="797" height="90" alt="image" src="https://github.com/user-attachments/assets/2055fe62-bccf-4782-bc08-838ef904da4d" />

##Conclusion & improvements
There are some large errors due to very high salaries.
