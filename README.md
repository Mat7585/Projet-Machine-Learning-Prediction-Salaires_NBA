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
3/ Data cleaning: removed non-informative/redundant columns, standardized data types, and converted key fields (height, weight, draft pick) into model-ready numeric features. Prepared categorical variables for encoding and exported a cleaned dataset for modeling.
4/ Imputation of missing values using appropriate replacement strategies, and removal of columns with excessive missingness.
5/ Outlier detection and capping when necessary to limit the impact of extreme values.
6/ Encoded categorical features into numerical representations (e.g., one-hot encoding) for model compatibility.

...

### Data transformation stage
...

### Supervised Machine Learning stage
...

### Results
...

##Conclusion & improvements
...
