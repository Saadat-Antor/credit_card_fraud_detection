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
2. There were 1825 rows that were zero-dollar transactions and 27 out of them were flagged as fraud. But it is not unusual in credit card transactions.
3. The ```Time``` feature is quite important and its' distribution among two classes i.e. Class=0(normal) and Class=1(Fraud) shows that fraudulent transactions are more evenly distributed than the normal ones. The normal ones actually shows a cyclic distribution which indicates both 'peak' and 'off-peak' times.

![image](https://github.com/user-attachments/assets/fcf01da7-ca74-48fd-98c1-77aca37d156f)

4. An important feature was made called ```Time_Diff``` which represents the time gap (in seconds) between consecutive transactions. For fraudulent transactions, the average time gap is approximately 1.07 seconds, with a maximum gap of 16 seconds. Most fraudulent transactions (75%) occur with a time gap of 1 second or less, and half of them have no gap at all.
In contrast, normal transactions have a lower average time gap of 0.61 seconds, but the maximum gap extends to 32 seconds. Similarly, 75% of normal transactions also occur within a gap of 1 second or less, and 50% have no time gap.
5. To conduct a time of day analysis another feature ```Hour``` was created and the ```Time_Diff``` was plotted against it.

![image](https://github.com/user-attachments/assets/7c84c5d0-ef4c-4b58-a811-f2af43851521)

Fraudulent transactions display a clear tendency to occur in bursts or clusters, as shown by significant spikes in average time differences during certain hours (e.g., around hours 5 and 28). These bursts suggest that fraudulent transactions are often concentrated within short intervals, possibly indicative of coordinated attacks or automated processes.

6. More features are created to improve model performance. They are ```Is_Fraud_Consecutive```, ```is_burst_period```, ```is_peak_hour```, ```mean_time_diff_by_hour```, ```std_time_diff_by_hour```, ```distance_to_peak```, ```time_cluster```, ```fraud_count_last_10```, ```time_diff_normalized```. They serve different purposes for our analysis and provide weight to more accurate results.
7. The ```Amount``` feature showed a right-skewed distribution for the fraudulent class i.e. Class = 1.

![image](https://github.com/user-attachments/assets/182f5ced-e1cd-4947-b1de-ba45d5b010b1)

8. To understand how ```Time_Diff``` can influence the ```Amount``` feature and thus the target feature ```Class```, a strategy called 'binning' is applied onto ```Amount```. The created bins indicate whether the fraudulent transactions cluster around specific amount ranges.

![image](https://github.com/user-attachments/assets/1cfd4d39-982a-4e54-ae4f-7dd6cdd7adc6)

From the above graph, the category 'High'(£1000 to £10,000) may have the highest possibility between the fraudulent amount ranges i.e. most likely the fraudulent amounts will be in this range. Also, a Hypothesis Test i.e. Chi-squared test was conducted to find out whether fraud is more likely in specific ```Amount``` ranges. The p-value was 2.937336960675823e-17 which was way below 0.05. This indicated strong evidence for the hypothesis in this Chi-Square test of independence.

9. After all of that, a heatmap was generated to find the correlation between all the PCA features:

![image](https://github.com/user-attachments/assets/fbe32b1e-9062-494d-a4d7-da773923366e)

This heatmap suggested that there were some PCA features that are positively and negatively correlated with ```Time``` and ```Amount```. V7 and V20 are positively and V2 and V5 are negatively correlated with ```Amount```. Also, V3 is negatively correlated with ```Time```.

10. Also, many distribution graphs were generated for every PCA features with respect to the Fraudulent(Class=1) and Normal(Class=0) to understand how the features were spread around 0:

![image](https://github.com/user-attachments/assets/da6e687b-bf70-4839-a47c-e47566d94484)

The distributions showed that almost all the features are distributed around 0. But some of them went away from zero, especially the distribution of the Class 1(Fraud) such as V1, V3, V4, V7, V9, V10, V11, V14 and so on. There were also features that have almost similar distribution for both the classes, V13, V15, V22, V25, and V26.

## 3. Model Selection
11. As mentioned before the dataset was highly imbalanced, so an oversampling technique called SMOTE was used to balance the dataset. It was done after the split of the main dataset into train, test, and evaluation sets.

12. To keep track of the improvement of the models, they were evaluated twice, once before including the engineered features and once after.

13. To select the best mode(before introducing the engineered features) from the three models i.e. Logistic Regression, Random Forest, and Gradient Boosting, a cross-validation strategy was introduced. To conduct this strategy a function called ```evaluate``` was created. This function cross-validates the models with 5 different versions of the train dataset with set hyperparameters and test the models with the validation set before determining the best model among the mentioned three. The below screenshot provides the scores of each of the models for cross-validation sets and the validation set.

![image](https://github.com/user-attachments/assets/ea189b8e-7b99-4706-8f42-5d057aeafe2a)

After determining the best model, the AUC-ROC score was determined, 0.9731.

14. After introducing the engineered features, the same process was followed and the AUC-ROC score was 0.9999.

![image](https://github.com/user-attachments/assets/25f09f04-2ca9-49f0-a37b-7750b0658568)


