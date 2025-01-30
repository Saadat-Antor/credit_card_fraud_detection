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
4. An important feature was made called ```Time_Diff``` which represents the time gap (in seconds) between consecutive transactions. For fraudulent transactions, the average time gap is approximately 1.07 seconds, with a maximum gap of 16 seconds. Most fraudulent transactions (75%) occur with a time gap of 1 second or less, and half of them have no gap at all.
In contrast, normal transactions have a lower average time gap of 0.61 seconds, but the maximum gap extends to 32 seconds. Similarly, 75% of normal transactions also occur within a gap of 1 second or less, and 50% have no time gap.
5. To conduct a time of day analysis another feature ```Hour``` was created and the ```Time_Diff``` was plotted against it.
![image](https://github.com/user-attachments/assets/7c84c5d0-ef4c-4b58-a811-f2af43851521)
Fraudulent transactions display a clear tendency to occur in bursts or clusters, as shown by significant spikes in average time differences during certain hours (e.g., around hours 5 and 28). These bursts suggest that fraudulent transactions are often concentrated within short intervals, possibly indicative of coordinated attacks or automated processes.
6.


