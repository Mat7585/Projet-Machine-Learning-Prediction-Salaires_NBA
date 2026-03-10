# NBA Salary Prediction (1985–2018)

## Objective
This project predicts total NBA career salary using player-level career information from 1985 to 2018.
The main challenge **was avoiding temporal leakage, since the dataset mixes season-level and career-level variables**.
To solve this, I reframed the problem from season salary prediction to total career salary prediction.

## Dataset
- Source: Kaggle — NBA Player Salaries (1985–2018) : https://www.kaggle.com/datasets/ulrikthygepedersen/nba-player-salaries/data?select=salaries_1985to2018.csv
- Main files: `salaries_1985to2018.csv` &  `players.csv`
- Contains player salary history and player information
- Combines season-level and career-level variables

## Approach
### Data preparation
- Imported and explored both datasets
- Merged salaries_1985to2018.csv and players.csv
- Kept only career-level variables and aggregated features when needed
- Cleaned the data, imputed missing values, and removed columns with excessive missingness
- Detected and capped outliers to reduce the impact of extreme values
- Applied one-hot encoding for Linear Regression
- Kept native categorical handling for XGBoost when applicable



### Modeling

I trained and compared two regression models: Linear Regression and XGBoost.

### Data transformations

The target variable was highly right-skewed, so I applied a log transformation. StandardScaler did not improve the Linear Regression results, and feature scaling was not needed for XGBoost. Therefore, I kept only the log-transformed target.

The histogram below shows the strong right skew of the target variable:  
<img width="1046" height="880" alt="image" src="https://github.com/user-attachments/assets/43c4300e-62e1-4d6d-97ce-9f0da182c3c1" />


### Results
        Model	                    RMSE	        R²	    MAE	       Median AE
XGBoost + log(y)	                  4,411,183	    0.9873	2,038,471	 516,751
Linear Regression + log(y)	        21,410,359	  0.4739	8,901,897	 2,875,696

XGBoost + log(y) achieved substantially better performance than Linear Regression + log(y) across all evaluation metrics. It obtained a much lower RMSE, MAE, and Median Absolute Error, indicating **smaller prediction errors overall**, while its much higher R² shows that it explains a far **greater share of the variance in salary**.



## Conclusion & improvements
<img width="1111" height="881" alt="image" src="https://github.com/user-attachments/assets/dc988116-c4c7-4ed4-a773-569236f27c62" />    

Overall, the XGBoost model with log-transformed target variable achieved the best predictive performance. This is confirmed both by the evaluation metrics and by the prediction plot, where most points lie very close to the 45-degree reference line. This visual alignment indicates that the predicted salaries are generally very close to the actual salaries. Although **a few larger deviations remain for the highest salary values**, the model captures the overall relationship extremely well and provides reliable predictions. Therefore, XGBoost was retained as the final model for this project.
