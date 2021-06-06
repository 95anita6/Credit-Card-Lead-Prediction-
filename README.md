# Credit-Card-Lead-Prediction-
Prediction if the customer would be interested to by the recommended credit card services 

## Problem Statement: 

Happy Customer Bank is a mid-sized private bank that deals in all kinds of banking products, like Savings accounts, Current accounts, investment products, credit products, among other offerings.

The bank also cross-sells products to its existing customers and to do so they use different kinds of communication like tele-calling, e-mails, recommendations on net banking, mobile banking, etc. 

In this case, the Happy Customer Bank wants to cross sell its credit cards to its existing customers. The bank has identified a set of customers that are eligible for taking these credit cards.

Now, the bank is looking for your help in identifying customers that could show higher intent towards a recommended credit card, given:
    • Customer details (gender, age, region etc.)
    • Details of his/her relationship with the bank (Channel_Code,Vintage, 'Avg_Asset_Value etc.)

Data Summary:
The given train dataset has 245725 total records for customers and the given test dataset has 105312 records. The given information for customers are as below:
- ID : Unique ID
- Gender
- Age
- Region_Code : Code of the region for customers
- Occupation
- Channel_Code : Acquisition channel for the customers
- Vintage : In months
- Credit_Product : If the customer has any active products
- Avg_Account_Balance : Average Account Balance for the customer in last 12 months
- Is_Active : If the customer was active in the last three months
- Is_Lead : If the customer is interested in the recommended credit card. This is the target variable.

The dataset has 3 numerical features – Age, Vintage, Avg_Account_Balance and rest of features as  categorical features. The categorical features take the below values:
Gender  :  ['Female' 'Male'] 

Region_Code  :  ['RG267' 'RG284' 'RG277' 'RG270' 'RG274' 'RG269' 'RG254' 'RG268' 'RG252'
 'RG272' 'RG250' 'RG280' 'RG265' 'RG283' 'RG281' 'RG262' 'RG279' 'RG257'
 'RG282' 'RG275' 'RG261' 'RG256' 'RG260' 'RG273' 'RG253' 'RG264' 'RG251'
 'RG263' 'RG266' 'RG255' 'RG276' 'RG258' 'RG278' 'RG271' 'RG259'] 

Occupation  :  ['Salaried' 'Self_Employed' 'Other' 'Entrepreneur'] 

Channel_Code  :  ['X1' 'X2' 'X3' 'X4'] 

Credit_Product  :  ['Yes' 'No' nan] 

Is_Active  :  ['No' 'Yes'] 
 
The data contained null values for the column Credit_Product. The mean age was 43.85, mean vintage value 46.97 and the mean avg_account_balance was 1.128749e+06. 

Brief Approach to the Problem:

The problem at hand was solved following below approach:

- The given data was inspected and cleaned for null values or any extra information. The column Credit_Product contained null values which was imputed with the mode values, in this case ‘No’.

- Then the data was analyzed to study the features and how they played with the target as well as each other.

- The data can then be preprocessed to replace the outlier points. The outlier points in the columns Avg_Account_Balance were replaces with 25% and 75% quantile values.

- The categorical features were used to create dummies dropping the first column in the dummies dataframe which is the extra information as part of feature engineering step.
 
- Standardized the data using StandardScaler from sklearn. Standardization was required because the numerical features had completely different scales. Then used MinMaxScaler to scale the range of values between [0,1] as negative values were returned from StandardScaler.

- Logisitic Regression, Decision Tree Classifier,  Random Forest Classifier, Extra Tree Classifier, XGB Classifier, Support Vector Machine, KNN classifier, Multinomial NB Classifier and a neural network MLP Classifier were used as models to be trained.

- These models were trained using all the features and the ROC AUC Score was compared for each model using cross valdation method. Also compare this performance score on train and test data to check for high variance/ overfitting in the model. Decision Tree and Random Forest models were highly overfitted models. Linear model, SVM and KNN performed fairly well. XGB model gave the maximum score and overcomed the overfitting problem from Decision Tree and Random Forest.

- Also used Random Forest and XGB Model to select top 15 features. The features selected from Random Forest model were more inlined with the analysis performed. XGB model was trained using these selected features and evaluated.

- XGB Model was hypertunned using Randomized Search CV but the score obtained was similar as previous XGB model but the variance was reduced.

- HyperOpt parameter tunning method was used to tune a Random Forest model but obtained an overfititng model.

- XGB model was selected as the final model after the training and retraining different models and comapring the performance metrics.


Inferences from data analysis:

- Customers who were more interested in the credit card are having more age than those who were not interested be it male or female

- Customers who are Enterpreneurs have more account balance

- Salaried customers tend to be more interested in credit card with more account balance as compared to the ones who tend to be not interested

- Self Employed customers tend to be the most interested

- More the Vintage more the customers tend to be interested in credit card and male customers with more vintage seem to be more interested than female customers.

- If the customer has not been active in the last three months there is a high chance that they would not be interested in credit card. The portion of customers who happen to have interest is not much affected by the fact that they have been active in that last three months or not.

- If the customer does not have any active credit product there is a high chance that the customer would not be interest in credit card. The customers who have any active credit product tend to less interested than those who don't have any active credit product.

- Customer under region code RG268 have most customers who are not interested followed by RG254 and RG283 and customer under region code RG268 are more interested followed by RG283 and RG284
- Customers with Acquisition Channel Code X1 tend to be most uninterested and X3 has more number of customers who would be interested. The population under X4 is very less
- Not so much correlation among the numeric features
-Different customer groups (clusters)  having average age, vintage and account balance values were obtained that can be targeted
     
