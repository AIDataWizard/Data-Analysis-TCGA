# Data-Analysis-TCGA

High-dimensional data are often "data hungry," demanding vast amounts of information for accurate analysis. The high dimensionality can cause significant estimation variance, especially when numerous parameters need to be estimated. Consequently, reducing the dimensionality of the problem before modeling is a common practice. This can be achieved through techniques such as dimensionality reduction or feature selection, where a potentially large subset of characteristics is filtered out before the modeling process. Implementing these strategies effectively can enhance model performance and accuracy, providing more reliable outcomes in data analysis.

In this analysis, we employed dimension reduction techniques such as Principal Component Analysis (PCA) and simple filtering based on the ANOVA F-test. We investigated three distinct classifiers—k-Nearest Neighbors (kNN), Support Vector Machine (SVM), and logistic regression—each offering unique advantages. To optimize prediction performance, we determined the number of primary components through cross-validation. This approach ensures a robust and accurate model by leveraging the strengths of each classifier and the most relevant data components.

By contrasting the training error, cross-validation error, and test error performance after selecting the ideal principal components (PCs) or features, this analysis illustrates the optimism inherent in training. Optimism in this context refers to the tendency of the training error to underestimate the true error rate due to overfitting.

Flexible classifiers, such as k-Nearest Neighbors (kNN), typically exhibit higher optimism. They adapt closely to the training data, often capturing noise as well as the underlying patterns, which leads to lower training error but potentially higher cross-validation and test errors. This discrepancy highlights their sensitivity to overfitting, making them appear overly optimistic during training.

In contrast, rigid classifiers, such as Support Vector Machines (SVM) and logistic regression, maintain a more consistent performance across training, cross-validation, and test sets. Their lower flexibility means they generalize better, resulting in less pronounced optimism. The training error for rigid classifiers is often closer to the cross-validation and test errors, indicating a more reliable assessment of their performance.

# Noisy Mislabeled Data

Research on noisy or incorrectly labeled data and its impact on model training and test data prediction performance is a highly active field. Incorrectly labeled data, often resulting from cheap and imprecise data gathering methods, can significantly degrade the quality of the training data. This "dirty data" introduces mislabeling, which can challenge the learning algorithms and affect their performance.

In this analysis, I randomly altered some of the observations' labels to produce a mislabeled dataset from the cancer data. It's important to note that the test data remains clean; only the training data is affected by mislabeling.

In this analysis, we examine the effects of different degrees of mislabeling on model training and prediction performance using the cancer dataset. We investigate three levels of mislabeling: mild (25% of training data), severe (50% of training data), and extremely severe (75% of training data). The test data remains clean to accurately assess the models' generalization performance.

The analysis also examines the predicted accuracy of each approach and draws conclusions about why certain strategies may perform worse than others. By evaluating the performance metrics, we can identify the strengths and weaknesses of each model. The following table showcases the characteristics and flexibility of the different models used, based on the results retrieved from the analysis.


|                   | kNN                             | Logistic Regression                                     | Support Vector Machines (SVM)                        |
|-------------------|---------------------------------|---------------------------------------------------------|-----------------------------------------------------|
| **Flexibility**   | Very Flexible                   | Rigid                                                   | Moderately Flexible                                  |
| **Characteristics**| Adapts based on nearest data points | First a linear decision boundary                        | Linear kernel is rigid; can use kernels (e.g., RBF) for greater flexibility. |
|                   | Can fit highly non-linear patterns | Struggles with complex, nonlinear data without transformations | Kernel trick allows fitting complex, high-dimensional patterns. |

# Feature Selection (ANOVA F-test)

## Checking for Constant Features

The process begins by identifying constant features in the dataset. Constant features are columns with only one unique value, providing no variability or useful information for modeling. Using the nunique() method, the code counts the unique values in each column and filters out those with only one unique value. These constant features are then dropped from the dataset to reduce dimensionality and avoid potential issues in subsequent modeling steps. The identified constant features include columns like 'V84', 'V402', and others. This step is crucial for enhancing model efficiency and accuracy by ensuring that only informative features are utilized in the analysis.

## Dropping Constant Features

After identifying the constant features, the code proceeds to remove them from the dataset ('data_df'). This step ensures that only informative features remain, streamlining the dataset and enhancing the efficiency of the machine learning models. By eliminating these redundant columns, the dataset becomes more manageable and focused, which helps improve model performance and accuracy. The resulting dataset, now free of constant features, is stored in the variable 'X', ready for subsequent modeling steps.

## Stratified Split

The next step involves splitting the dataset into training and testing sets using a stratified split. This method ensures that both sets maintain the same class proportion as the original dataset, preserving the representativeness of the data. By specifying 'train_size=0.7', 70% of the data is allocated for training and 30% for testing. This stratification is crucial for maintaining the data's representativeness, which is essential for reliable model evaluation. By ensuring that the class distribution remains consistent, the model's performance on the test set will more accurately reflect its real-world performance.

## ANOVA F-test Feature Selection

To identify the most significant features, the code uses the ANOVA F-test. The 'SelectKBest' class, initialized with 'score_func=f_classif', ranks features based on their F-scores, which measure the variance between different classes. The top 20 features with the highest F-scores are selected, highlighting those that have the strongest relationships with the target variable. High F-scores indicate a strong relationship, while low P-values suggest statistical significance. For instance, features such as 'V18', 'V1936', and 'V1744' have very high F-scores, underscoring their importance in distinguishing between different classes. This selection process is essential for optimizing model performance by focusing on the most relevant features.

## Creating and Sorting a DataFrame

To facilitate a better understanding of feature significance, a DataFrame is created that combines feature names, their F-scores, and P-values. This DataFrame is then sorted in descending order by F-score, highlighting the most important features. The top 50 features are printed, providing a clear view of the most impactful attributes. This organized presentation is essential for focused analysis and model building, allowing data scientists to prioritize the most significant features for optimal model performance.
## Visualizing Top Features

The following graph shows the top 20 features (gene expression that relates to how much of a gene product (protein) is being produced) 

![Top 20 Features from TCGA Dataset](https://github.com/AIDataWizard/Data-Analysis-TCGA/blob/main/Top_20_feat_plot.png?raw=true)
