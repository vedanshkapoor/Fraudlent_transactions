# Fraudlent_transactions
This is an machine learning project which predicts the probability of fraudlent transactions on an industrial scale


Data Dictionary -
step - maps a unit of time in the real world. In this case 1 step is 1 hour of time. Total steps 744 (30 days simulation).

type - CASH-IN, CASH-OUT, DEBIT, PAYMENT and TRANSFER.

amount - amount of the transaction in local currency.

nameOrig - customer who started the transaction

oldbalanceOrg - initial balance before the transaction

newbalanceOrig - new balance after the transaction

nameDest - customer who is the recipient of the transaction

oldbalanceDest - initial balance recipient before the transaction. Note that there is not information for customers that start with M (Merchants).

newbalanceDest - new balance recipient after the transaction. Note that there is not information for customers that start with M (Merchants).

isFraud - This is the transactions made by the fraudulent agents inside the simulation. In this specific dataset the fraudulent behavior of the agents aims to profit by taking control or customers accounts and try to empty the funds by transferring to another account and then cashing out of the system.

isFlaggedFraud - The business model aims to control massive transfers from one account to another and flags illegal attempts. An illegal attempt in this dataset is an attempt to transfer more than 200.000 in a single transaction.


Selection of metric :
Given the highly skewed data, I use the area under the precision-recall curve (AUPRC) instead of the traditional area under the receiver operating characteristic (AUROC). AUPRC is particularly useful for datasets with 99% negative and 1% positive examples, as it emphasizes the model's performance on the minority class. A high AUPRC indicates that the model effectively handles the positive examples, whereas a low AUPRC suggests poor performance on these examples.


ML algorithm-
A common initial approach to address imbalanced data is to balance it by discarding a portion of the majority class before applying a machine learning algorithm. However, the downside of undersampling is that the resulting model may not perform well on real-world skewed test data since much of the information is discarded. A more effective strategy could be to oversample the minority class, using techniques such as the Synthetic Minority Over-sampling Technique (SMOTE) available in the 'imblearn' library. Inspired by this, I experimented with various anomaly detection and supervised learning approaches. Ultimately, I found that the best results were achieved on the original dataset using machine learning algorithms based on ensembles of decision trees, which inherently perform well on imbalanced data. These algorithms not only handle missing values effectively but also benefit from parallel processing for increased speed. Among these, the extreme gradient-boosted (XGBoost) algorithm stood out. Additionally, XGBoost, like several other machine learning algorithms, allows for adjusting the weighting of the positive class relative to the negative class, which helps address the dataset's skew.
