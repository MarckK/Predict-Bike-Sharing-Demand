# Report: Predict Bike Sharing Demand with AutoGluon Solution
#### Kara de la Marck

## Initial Training
### What did you realize when you tried to submit your predictions? What changes were needed to the output of the predictor to submit your results?
Kaggle only accepts predictions that are greater than 0. I needed to inspect the predictions to see if there were any negative values. I did this in a number of ways, the final check was to run a count of negative values in the predictions. Any negative values I set to zero and ran a count again. Then, I assigned the predictions to the submission dataframe and submittted to Kaggle.

### What was the top ranked model that performed?
The `top-ranked model` was the `(add features) model` named `WeightedEnsemble_L3`, with a **validation RMSE score** of **33.9800** and the best **Kaggle score** of **0.46258 (on test dataset)**. This model was developed by training on data obtained using exploratory data analysis (EDA) and feature engineering without the use of a hyperparameter optimization routine. 

## Exploratory data analysis and feature creation
### What did the exploratory analysis find and how did you add additional features?
**first EDA find**
The first exploratory analysis find conerned the `datetime` column with `object` dtype, which I changed into `datetime` dtype. Then I added more features by splitting separate column of `year`, `month`, `day`, and `hour` and from datetime column. 

**second EDA find**
Plotting the histogram of the training data during EDA gave insights into the distributions of each feature in the data. Plotting the data showed readily that there are two main types of data: *caegorical* and *continuous* data. Among the categorical data, the `season` and `weather` features are more informative while `holiday` and `workingday` are in a binary distribution. Therefore, I converted informative `season` and `weather` data into `categorical` type from `int64`.

### How much better did your model preform after adding additional features and why do you think that is?
- The addition of additional features improved model performance greatly in comparison to the initial/raw model (without EDA and/or feature engineering) performance.
- The model performance improved after converting certain categorical variables with `integer` data types into their true `categorical` datatypes. 
- Moreover, splitting the `datetime` feature into multiple independent features such as `year`, `month`, `day` and `hour`, further improved the model performance because these predictor variables `aid the model assess seasonality or historical patterns in the data` more effectively.
- Overall, the Kaggle score of `root_mean_square_error` (RMSE) decreased to a better result of `0.46258` from `1.80660`. 

## Hyper parameter tuning
### How much better did your model preform after trying different hyper parameters?
Trying with some model algorithms such as `lightGBM` and `NeuralNets` and its related hyperparameters moderately affected the model performance. Although hyperparameter tuned models delivered competitive performances in comparison to the model with EDA and added features, the latter performed better on the Kaggle (test) dataset.

### If you were given more time with this dataset, where do you think you would spend more time?
Given more time to work with this dataset, I would spend more time experimenting with hyperparameter tuning with AutoGluon. The current trials show that the performance of hyperparameter optimized models can be sub-optimal because the hyperparameters are tuned with a fixed set of values given by the user, which then limits the options AutoGluon can explore. It is important to be quite knowledgeable about the hyperparameters when setting them manually and/or to have a lot of time for experimentation. 

I would like to investigate additional potential outcomes when AutoGluon is run for an extended period with a high quality preset and enhanced hyperparameter tuning.

### Create a table with the models you ran, the hyperparameters modified, and the kaggle score.

|model|hpo1|hpo2|hpo3|score|
|--|--|--|--|--|
|initial|prescribed_values|prescribed_values|"presets: 'best_quality' (auto_stack=True)"|1.80660|
|add_features|prescribed_values|prescribed_values|"presets: 'best_quality' (auto_stack=True)"|0.46258|
|hpo|Tree-Based Models: (GBM, XT, XGB & RF)|KNN|"presets: 'best_quality'|0.47702|

### Create a line plot showing the top model score for the three (or more) training runs during the project.

![model_train_score.png](model_train_score.png)

### Create a line plot showing the top kaggle score for the three (or more) prediction submissions during the project.

![model_test_score.png](model_test_score.png)

## Summary
The top-ranked model was the (add features) model named WeightedEnsemble_L3, with the best Kaggle score of 0.46258 (on the test dataset). This top-ranked AutoGluon-based model achieved significantly improved results by utilizing data obtained after exploratory data analysis (EDA) and feature engineering without hyperparameter optimization. Leveraging automatic hyperparameter tuning, model selection/ensembling and architecture search enables AutoGluon to explore and exploit the best  options. 
