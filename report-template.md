# Report: Predict Bike Sharing Demand with AutoGluon Solution
#### Chinedu Emmanuel Agwunobi

## Initial Training
### What did you realize when you tried to submit your predictions? What changes were needed to the output of the predictor to submit your results?

Five different experiments were performed as follows:

    Initial Raw Submission [Model: initial]
    Added Features Submission (EDA + Feature Engineering) [Model: add_features]
    Hyperparameter Optimization (HPO) - Initial Setting Submission
    Hyperparameter Optimization (HPO1) - Setting 1 Submission
    Hyperparameter Optimization (HPO2) - Setting 2 Submission 

Iniatially I experienced this error; "/bin/sh: 1: kaggle: not found unzip:  cannot find or open bike-sharing-demand.zip, bike-sharing-demand.zip.zip or bike-sharing-demand.zip.ZIP.", which also affected my submission until I was able to install kaggle using "pip install kaggle", then the error was resolved.

Then when trying to submit to kaggle, the predictions were rejected because some of the values were containing negative values.
Which were later converted to zero to resolve the issues with the submission

### What was the top ranked model that performed?

The top-ranked model was the HPO1 (predictions_new_hpo1) model named WeightedEnsemble_L2, with a validation RMSE score of 34.4510 and the best Kaggle score of 0.52512 (on test dataset). The model performed better after using some hyper parameter tuning.

## Exploratory data analysis and feature creation
### What did the exploratory analysis find and how did you add additional features?


* Feature datetime was parsed as a datetime feature to obtain hour information from timestamp
* Independent features season and weather were initially read as integer. Since these are categorical variables, they were transformed into category data type.
* The datetime needed to be split into more features and I chose to split it into year, month, day and hour which is what improve my model the most.
* After probing and considering the features, casual and registered, it was noticed that the RMSE scores improved significantly during cross-validation and these independent features were highly co-related to the target variable count. However, the features casual and registered are only present in the train dataset and absent in the test data; hence, these features were ignored/dropped during model training
* A histogram was plotted for data visualization in order to derive insights from the features.


### How much better did your model preform after adding additional features and why do you think that is?
The feature engineering improved the model by 60%, from 1.78607 to 0.69576 

## Hyper parameter tuning
### How much better did your model preform after trying different hyper parameters?
After performing the hyper parameters tunings, the first model hpo had a 23% improvement and hpo1 had a 25% improvement in the model score.

### If you were given more time with this dataset, where do you think you would spend more time?
If given more time, I would have implemented more feature engineering steps or include more relevant features to improve the model's performance.
Optimize the hyper parameters and include more relevant features in the Tabular Autogluon.

### Create a table with the models you ran, the hyperparameters modified, and the kaggle score.
|model|hpo1|hpo2|hpo3|score|
|--|--|--|--|--|
|initial|prescribed_values|prescribed_values|"presets: 'high quality' (auto_stack=True)"|1.78607|
|add_features|prescribed_values|prescribed_values|"presets: 'high quality' (auto_stack=True)"|0.69576|
|hpo (top-hpo-model: hpo1)|Tree-Based Models: (GBM, XT, XGB & RF)|KNN|"presets: 'optimize_for_deployment"|0.52512|

### Create a line plot showing the top model score for the three (or more) training runs during the project.



![model_train_score.png](img/Image1.png)

### Create a line plot showing the top kaggle score for the three (or more) prediction submissions during the project.



![model_test_score.png](img/Image2.png)

## Summary
* Being the first time working with Tabular AutoGluon and using AWS Sagemaker, it was a bit challenging task for me initially.
* The AutoGluon framework's capabilities were fully utilized to make automated stack ensembled as well as individually distinct configured regression models trained on tabular data. It assisted in quickly prototyping a base-line model.
* The top-ranked AutoGluon-based model improved results significantly by utilizing data obtained after extensive exploratory data analysis (EDA) and feature engineering without hyperparameter optimization.
* Leveraging automatic hyperparameter tuning, model selection/ensembling and architecture search allowed AutGluon to explore and exploit the best possible options.
* Addtionally, hyperparameter tuning using AutoGluon also offered improved performance over the initial raw submission; and was better than that of the model with EDA, feature engineering and no hyperparameter tuning.
* AutoGluon framework needs to be studied more and utilized for more machine learning projects/jobs.

