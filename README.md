# server-hack-prediction
This repository contains a model that was trained on anonymous columns related to server logs to predict possible server hack.

I implemented this using the below approach:

The test and train datasets, contain a list of anonymized features that represent server log information to detect potential server intrusion.

After importing the test and train data, I performed EDA by leveraging pandas profiling to generate a report with the key details like feature wise cardinality, zeros etc along with their overall correlation. 

I noticed that data has a date feature, in order to reduce the cardinality and effectively use it for training, I created new features by extracting the month,year and day to add additional information for model training and testing.

Based on the EDA, the field X_12 is the only feature with missing values, which accounted to 0.8% or 182 records.Since the feature is anonymised , replacing the missing values using mean/median may or may not yield desired results. One good approach would be to predicting the missing values by building a model by treating the feature as dependent variable.But as per the EDA, we can observe that there is a high correlation between the features X_12 and X_10. This meant to reduce the complexity,I could the X_12 and accuracy shouldnt be effected.

Based on the recall score of the base model, I could revisit the feature at a later point in time if required.

After choosing the required features, I applied standard scaling would yield better results in this instance.

For the prediction , I am chose a classification model instead of regression, since we simply want to know if it is likely hacked to not instead of knowing the possiblity or a risk score. For this, I am chose random forest classifier as a base model . Random forest models usually,in my experience, are good when we have multiple features and relatively more data to train. Additionally, since it is an ensemble model, it would yield better results even without using techniques like xgboost etc for boosting.

In order to identify the best hyper parameters, to predict and detect if server is hacked using the test data, I wanted to test what paramenter would generate relatively better scores. In order to understand this, I built and tested a model by splitting the training dataset and trying to predict the values on a subset of the training dataset to identify the optimum hyper parameter.


I plotted the results for the base models by plotting the accuracy for various hyper parameters and chose the best combination for building the final model.


I finally trained the model with the updated list of features and hyper parameters to predict if the server got hacked for the given test dataset and created a submission file.

