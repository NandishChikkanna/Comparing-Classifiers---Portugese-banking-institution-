# Practical Application III: Comparing Classifiers

**Overview**: In this practical application, your goal is to compare the performance of the classifiers we encountered in this section, namely K Nearest Neighbor, Logistic Regression, Decision Trees, and Support Vector Machines.  We will utilize a dataset related to marketing bank products over the telephone.  

Our dataset comes from the UCI Machine Learning repository link. The data is from a Portugese banking institution and is a collection of the results of multiple marketing campaigns. We will make use of the article accompanying the dataset here for more information on the data and features.

🎯 **Business Objective**

Predict whether a bank customer will subscribe to a term deposit (y = yes) based on client and bank-related features.

📊 **Models Evaluated**

You trained and tuned the following models:
- Decision Tree
- Logistic Regression
- Support Vector Machine (SVM)
- K-Nearest Neighbors (KNN) — evaluated on a smaller subset

⚙️ **Best Hyperparameters (from GridSearchCV)**

| Model             | Best Params                                      |
|-------------------|--------------------------------------------------|
| Decision Tree     | criterion='gini', max_depth=3, min_samples_split=2|
| Logistic Reg.     | C=0.01, penalty='l2', solver='lbfgs'             |
| SVM               | C=1, kernel='linear', gamma='scale'              |
| KNN (1k train)    | n_neighbors=7, weights='uniform', metric='euclidean'|

🧪 **Test Set Performance**

| Model                        | Accuracy | Precision (Yes) | Recall (Yes) | F1-Score (Yes) |
|------------------------------|----------|-----------------|--------------|----------------|
| Decision Tree (Tuned)        | 0.8734   | 0.0000          | 0.0000       | 0.0000         |
| Logistic Regression (Tuned)  | 0.8734   | 0.0000          | 0.0000       | 0.0000         |
| SVM (Tuned)                  | 0.8734   | 0.0000          | 0.0000       | 0.0000         |
| KNN (Tuned, 1k train)        | 0.8642   | 0.2358          | 0.0324       | 0.0569         |

🔍 **Confusion Matrix Highlights**

Most models predicted only the majority class (no):
- All models except KNN predicted 0 positives (yes)
- KNN correctly identified 25 true positives, with 81 false positives

⚠️ **Challenges Identified**

- Severe class imbalance (only ~11% of samples are yes)
- Most models fail to identify any positive cases, despite good accuracy

✅ **Recommendations**

- Apply class balancing techniques:
  - Use class_weight='balanced'
  - Try SMOTE or undersampling
- Explore additional features:
  - Economic indicators, campaign performance, etc.
  - Be cautious of duration (information leakage)
- Use better metrics:
  - Focus on F1-score, recall, and ROC-AUC instead of accuracy
- Try ensemble models:
  - Random Forest, XGBoost, or LightGBM often handle imbalance better
