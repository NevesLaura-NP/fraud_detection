# :money_with_wings: Fraud Detection :exclamation:

This is a project based on historical transactions data from a bank. This will allow the creation of a minimal-viable-product that detects fraudulant payments.

Currently is not possible to import the data to github due to its datafile size limit. However jupiter notebooks will still be able to demonstrate the outputs of the analysed data, allowing the peer review of the code.

# EDA

Through an investigation of the data frame we could observe immediately that the isFlaggedFraud column did not represent our target variable accurately leading us to need to disregard it from our analysis. Once we chose the data that was classified as fraudulent and looked into the distribution of types of transactions we could see that they are limited to only two types: Cash Out and Transfer

![types](img/types.png)

Second, we may look at the median payments made fraudulently, which are typically higher than the median sums for legitimate transactions. Since the amount of rows tends to obscure the presentation of these tendencies, log was necessary for this particular visualization.

![amount](img/amount.png)

We also regarded that almost all names of destiny and origin of the transaction are unique which led us to drop these columns from the analysis.

# Pre-processing

After the analysis we needed to drop all unecessary columns such as isFlaggedFraud, nameDest and nameOrig. Then we made a transformation on the column type and replaced them classifications with a Frequency Encoding due to this columns instrinsic importance to define our fradulent cases. We then grasped a proportionate sample from the data frame so we could save computational expenses.

# Modeling 

Once we imported our newly sampled data we start to model it through Random Forest Classifier. We chose this type of ensemble method as the quantity of rows can make this data quite noisy to be modeled. We thus wanted to avoid potential overfitting of the data while also keeping a good amount of accuracy.

Once we utilize Random Forest Classifier we could regard a great score for test accuracy of 99.99%. However the model sufferend from classification imbalance. Due to non fraudulent transactions being the heavy majority of the data while fraudulent transactions were a minority the f1-score for each classification was different, with: 0.0 = 0.999949 and 1.0 = 0.857143. 

Next, we investigated the hyperparameters. While searching for hyperparameter values that are generally known to work well, I ultimately decided to use Grid Search. Taking into account the magnitude of the data collection, employing Random Search initially may cause delays in the outcomes and evaluation of our modeling, in addition to increasing computational expenses.

After discovering more effective parameters, the f1-score became 1.0 for each classification 100% accurately being able to predict if a transaction was fraudulent.
