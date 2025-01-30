# Credit Card Fraud Detection
**Goal:** The goal of this project is to predict fraudulent transactions using historical data i.e. transactions made by credit cards in September 2013 by European cardholders.
**Planning:** The following planning steps are taken to accomplish the goal:
1. Gathering Data
2. EDA & Feature Engineering
3. Model Selection

## 1. Gathering Data:
To accomplish our goal we have taken a dataset from Kaggle. This dataset presents transactions that occurred in two days by credit cards in September 2013 by European cardholders, where we have 492 frauds out of 284,807 transactions. The dataset is highly unbalanced, the positive class (frauds) account for 0.132% of all transactions.

## 2. EDA & Feature Engineering:
1. Have used describe() and info() funcions of pandas to understand the dataset. Have found out that there was no missing values and all the data types were accurate and made sense.
2. There were 1825 rows that are zero-dollar transactions and 27 out of them were flagged as fraud. But it is not unsusual in credit card transactions.
3. The ```Time``` feature is quite important and its' distribution among two classes i.e. Class=0(normal) and Class=1(Fraud) shows that fraudulent transactions are more evenly distributed than the normal ones. The normal ones actually shows a cyclic distribution which indicates both 'peak' and 'off-peak' times.
![image](https://github.com/user-attachments/assets/fcf01da7-ca74-48fd-98c1-77aca37d156f)
4. 

