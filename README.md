This is a Kaggle competition for Kaggle starter. We're required to predict house prices based on 80 variables (in fact many of them are useless). A more detailed description can be found at: https://www.kaggle.com/c/house-prices-advanced-regression-techniques/data

In this project, I did some basic EDA and feature engineering before fitting model:
  1. Eliminate outliers for GrLivArea, which is the second most important variable in prediction.
  2. Deal with missing values: ignore the variable with too many missings, and fill the missings with median, mode, mean or 0, None, depending on situation.
  3. Check skewness and transform the ones with skewness > 0.75 with boxcox. The target variable, sale price, is transformed with log.
  4. Create new features such as house age, total number of bathrooms, etc. By result of heatmap (using Spearman Correlation), the new created variables are strongly associated with target variable.
  
To train the model, I first fit a xgboost model and see its feature importance. By result, many of the variables have 0 feature importance. Since the result is changing with the change of parameters, I simply select features with importance>0. Then I tried several models, including both tree models and linear models, using the selected variables. After that, I fit a stacking model using combinations of tried models with good performance. Based on the their score, I weighted the result from these models and tuned the weights. Evaluation metric is always RMSE, the same as organizor's evaluation.

The result is top 8% on leaderboard.

Future improvement will be focused on dealing with ordinal variables, such as rating, quality and condition.

One of an interesting thing I found during this project is EDA and feature engineering are much more helpful and important than model tuning, based on the rmse observed.

Some inspiration got from https://www.kaggle.com/itslek/blend-stack-lr-gb-0-10649-house-prices-v57/data?scriptVersionId=11189608
