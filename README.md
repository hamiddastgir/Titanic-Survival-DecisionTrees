# Decision Tree and Ensemble Modeling on Titanic Dataset

**Table of Contents**  
- [Overview](#overview)  
- [Data Preparation](#data-preparation)  
- [Feature Engineering and Discretization](#feature-engineering-and-discretization)  
- [Decision Tree Modeling](#decision-tree-modeling)  
- [Model Optimization](#model-optimization)  
- [Advanced Modeling](#advanced-modeling)  
- [Ensemble Methods](#ensemble-methods)  
- [Random Forest Comparison](#random-forest-comparison)  
- [Performance Summary](#performance-summary)  
- [Contributing](#contributing)  

---

## Overview
This project demonstrates how to build, tune, and evaluate Decision Tree models to predict survival on the Titanic passenger dataset. Additionally, it showcases how to assemble multiple decision trees into an ensemble and compares the ensemble's performance with a Random Forest model.

---

## Data Preparation
1. **Loading the Data**  
   - The Titanic dataset is read into a pandas DataFrame.  
   - Basic exploration (e.g., `.head()`, `.info()`) is performed to understand the data’s structure.

2. **Handling Missing Values**  
   - Numerical fields (e.g., `age`, `fare`) are filled with their respective mean values.  
   - Categorical fields (e.g., `embarked`, `home.dest`, `cabin`, `boat`) are filled with their most frequent (mode) values.

3. **Subsetting**  
   - A subset of relevant columns is selected: **`'pclass'`, `'sex'`, `'age'`, `'sibsp'`,** and **`'survived'`**.  
   - The target variable (`survived`) is confirmed to be binary (0 or 1).

4. **Data Splitting**  
   - Data is split into training and test sets using an 80/20 ratio.  
   - `random_state` is used for reproducibility of results.

---

## Feature Engineering and Discretization
- **Discretizing `age`:**  
  Continuous features, such as age, are binned into quantiles for more effective splitting in decision trees.  
- **Encoding Categorical Fields:**  
  - `pclass` is mapped from `{'1st': 1, '2nd': 2, '3rd': 3}`.  
  - `sex` is mapped from `{'male': 1, 'female': 0}`.

---

## Decision Tree Modeling
1. **Initial Decision Tree**  
   - Built with scikit-learn’s `DecisionTreeClassifier`.  
   - Feature importance is analyzed (via `model.feature_importances_`) to determine which features drive splits.

2. **Tree Visualization**  
   - `plot_tree` is used to display the learned structure.  
   - Observed that `sex` often yields the highest information gain.

3. **Evaluation Metrics**  
   - A custom evaluation function is defined to compute **Accuracy**, **Precision**, **Recall**, and **F1** on the test set.  
   - These metrics guide model comparison and tuning.

---

## Model Optimization
- **Hyperparameter Tuning with GridSearchCV**  
  - Explores different values of `max_leaf_nodes` (from 5 to 20).  
  - Selects the model that maximizes accuracy through cross-validation.  
  - A pruned, compact tree is produced using the best hyperparameters.  

---

## Advanced Modeling
1. **Alternative Decision Trees**  
   - Models experimented with different parameters, such as `max_depth` and different splitting criteria (`gini` vs. `entropy`).  
   - Each new tree is visualized and its performance recorded.

2. **Observing Variations**  
   - Deeper trees may capture nuances at the risk of overfitting.  
   - Alternate criteria may produce differing splits and leaf structures.

---

## Ensemble Methods
- **Majority Voting**  
  - Three decision tree models (including the optimally pruned model) are combined via a simple majority vote.  
  - This approach seeks to reduce variance and improve overall stability.

- **Ensemble Results**  
  - Accuracy, Precision, Recall, and F1 are recalculated.  
  - Typically outperforms or at least competes with individual trees.

---

## Random Forest Comparison
- **Random Forest Classifier**  
  - Uses the optimal `max_leaf_nodes` discovered from Grid Search.  
  - Number of estimators (`n_estimators=50`) strikes a balance between speed and accuracy.

- **Comparative Analysis**  
  - The ensemble’s accuracy vs. the Random Forest model is reported.  
  - Notable differences in Precision and Recall are highlighted to demonstrate trade-offs.

---

## Performance Summary
| Model                      | Accuracy | Precision | Recall | F1 Score |
|----------------------------|----------|-----------|--------|----------|
| **Decision Tree (Pruned)** | ~0.767   | ~0.806    | ~0.636 | ~0.711   |
| **Ensemble (3 Trees)**     | ~0.767   | ~0.828    | ~0.610 | ~0.702   |
| **Random Forest**          | ~0.737   | ~0.889    | ~0.475 | ~0.619   |

> **Key Takeaways:**
> - The optimally pruned single Decision Tree yields a good balance of precision and recall.  
> - The Ensemble Model slightly improves certain metrics through majority voting.  
> - The Random Forest shows stronger precision but lower recall, demonstrating a trade-off depending on the application’s needs.

---

## Contributing
Contributions in the form of comments, model improvements, or additional ensemble techniques are always welcomed. If you have ideas for alternate feature engineering strategies or further tuning experiments, feel free to discuss!
