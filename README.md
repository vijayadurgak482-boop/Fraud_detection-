# A Hybrid Machine Learning Approach for Fraud Detection Using Autoencoders and Gradient
Fraud detection in real-world financial data is challenging because fraud cases are extremely rare—typically around 0.1% of all transactions—resulting in a highly imbalanced dataset. In such scenarios, traditional machine learning models can achieve up to 99.9% accuracy simply by predicting every transaction as legitimate. However, this approach completely fails to identify any fraudulent activity, making accuracy a misleading metric. The real objective is therefore not maximizing accuracy, but effectively detecting rare fraud cases while keeping false positives low, ensuring genuine transactions are not incorrectly flagged.


In real-world financial data, fraud accounts for only about 0.1% of all transactions. This creates a highly imbalanced dataset.
The challenge is that traditional machine learning models can achieve very high accuracy simply by predicting every transaction as legitimate.
But this completely fails to detect fraud.
So our goal is to build a model that can detect fraud effectively while also minimizing false alarms.
To understand the challenge better—
If a model predicts every transaction as legitimate, it can still achieve around 99.9% accuracy.
However, it would miss all fraudulent transactions.
So accuracy is not a reliable metric here.
The real challenge is to detect rare fraud cases without generating too many false positives.”

# Data-set 
For this project, we used the PaySim mobile money dataset, which contains over 6.35 million simulated transactions. Out of these millions of records, only a tiny fraction—about 0.1%—are labeled as fraud. When analyzing transaction types, we notice that fraud is heavily concentrated in specific operations like transfers and cash outs.For this project, we used the PaySim mobile money dataset, which contains over 6.35 million simulated transactions. Out of these millions of records, only a tiny fraction—about 0.1%—are labeled as fraud. When analyzing transaction types, we notice that fraud is heavily concentrated in specific operations like transfers and cash outs.

# Data preprocessing 
“To prepare the data, we performed several preprocessing steps.
First, we cleaned the data by removing duplicates and removing null values .
Then we created new features based on balance differences.
We converted categorical variables using one-hot encoding.
We applied log transformations to handle skewness.
We standardized the features and performed a stratified train-test split to maintain the class distribution.”

# Feature engineering
“A key part of our approach was feature engineering.
We created features like balance differences for both sender and receiver accounts.
These features help capture unusual transaction behavior.
For example, sudden changes in account balances can indicate fraudulent activity

# Methodology
Our methodology consists of three stages.
First, we built a baseline model using Logistic Regression.
Second, we used an Autoencoder for anomaly detection.
Finally, we combined both approaches into a hybrid model using Autoencoder and XGBoost.

# logistic Regression

“Logistic Regression was used as the baseline model because it is a simple and interpretable linear classifier.
To handle the imbalanced dataset, we applied class weighting and standardized all features before training.
The model achieved very high recall by detecting most fraud cases, missing only 8 out of 228 fraud transactions. However, it produced over 12,000 false positives, leading to many false alarms.
The Precision–Recall curve was used to evaluate the trade-off between precision and recall. Average Precision is the area under the Precision–Recall curve. It summarizes how well the model maintains high precision across different recall levels. A value closer to 1 indicates better performance. for our model The Average Precision (AP) score was approximately 0.424, indicating moderate performance, where precision decreases as recall increases.
Although the ROC-AUC score was high, it did not reflect the real-world impact of false alarms. This limitation motivated the move to Phase 2 using Deep Learning Autoencoders for better anomaly detection.”
AP ≈ 0.424Moderate performance
Precision drops as recall increases
Although the ROC-AUC score is high, this does not reflect real-world performance because of false alarms .
This directly justified the need to move to Phase 2: Deep Learning Autoencoders to capture better behavioral anomaly signatures. .
# Auto encoders
Fraud detection is an anomaly detection problem due to extreme class imbalance and constantly evolving fraud patterns. We initially used Autoencoders trained on legitimate transactions to learn normal transaction behavior and detect anomalies through reconstruction error. Feature engineering helped expose suspicious balance and transaction patterns more effectively.
Using only Autoencoders, we achieved 99.85% accuracy, 45.5% precision, and 64.6% recall. While recall was reasonably good for fraud detection, precision remained moderate due to false positives.
Since Autoencoders alone may generate false alarms and struggle as fraud patterns evolve, production systems typically combine Autoencoders with supervised ML models to improve overall fraud detection performance.
# Hybrid Model (Autoencoder +Logistic Regression)
We initially built a hybrid fraud detection model combining Autoencoders with Logistic Regression. The Autoencoder learned normal transaction behavior and generated anomaly scores, while Logistic Regression classified transactions using engineered features.
Although this provided a strong baseline, Logistic Regression struggled to capture complex nonlinear fraud patterns and hidden feature interactions, resulting in moderate performance:
Precision: 46.53%
Recall: 57.15%
F1 Score: 51.3%
To overcome these limitations, we replaced Logistic Regression with XGBoost while retaining the Autoencoder-based anomaly detection layer, significantly improving fraud detection performance.
# Hybrid Model (Autoencoder + XGBoost)
We are thinking XGBoost amy  significantly imprrove performance compared to Logistic Regression because it can capture nonlinear relationships, complex feature interactions, and rare fraud patterns in highly imbalanced datasets.
In addition, the Autoencoder  generated  anomaly scores  highly informative features to XGBoost. This hybrid approach may  enable  the model to detect both known fraud patterns and previously unseen anomalous behaviors more effectively, resulting in better fraud detection performance with reduced false alarms.”


