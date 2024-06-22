# Data-Analysis-TCGA

The majority of high-dimensional data are "data hungry". Due to high dimensionality, there may be a significant estimation variance for some approaches when a large number of parameters need to be estimated. As a result, trying to lower the problem's dimensionality before modeling is rather frequent. (Another way to do this is to filter before modeling, removing a (potentially big) subset of characteristics.

We used dimension reduction techniques in this analysis, including PCA and some simple filtering based on the ANOVA F-test

This analysis investigated three distinct classifiers—kNN, SVM, and logistic regression—each with a unique personality. 

To determine the number of primary components that optimize prediction performance, this analysis utilized cross-validation.

By contrasting the training error, cross-validation error following the selection of ideal PCs or features, and test error performance, this analysis illustrate the optimism of training. Talk about the differences in optimism between the flexible and rigid classifiers.

# Noisy Mislabeled Data

Research on noisy or incorrectly labeled data and how it affects model training and test data prediction performance is currently very active in research. For example, a cheap, imprecise data gathering approach may provide "dirty data" with mislabeling.

Here, I randomly alter some of the observations' labels to produce a mislabeled data set from the cancer data. Please take note that the test data should be clean; we should only construct mislabels for your training data.

This analysis looks at at least three different degrees of mislabeling: mild cases, which make up 25% of the training data, more severe cases, which make up 50% of the training data, and extremely serious cases, which make up 75% of the training data.

The analysis also examine the predicted accuracy of each approach and makes conclusion about the reasons why certain strategies may do worse than others. The following table shows the characteristics and flexibility of the different models used based on the results retrieved from the analysis.


|                   | kNN                             | Logistic Regression                                     | Support Vector Machines (SVM)                        |
|-------------------|---------------------------------|---------------------------------------------------------|-----------------------------------------------------|
| **Flexibility**   | Very Flexible                   | Rigid                                                   | Moderately Flexible                                  |
| **Characteristics**| Adapts based on nearest data points | First a linear decision boundary                        | Linear kernel is rigid; can use kernels (e.g., RBF) for greater flexibility. |
|                   | Can fit highly non-linear patterns | Struggles with complex, nonlinear data without transformations | Kernel trick allows fitting complex, high-dimensional patterns. |

# Feature Selection (ANOVA F-test)

## Checking for Constant Features

The process begins by identifying constant features in the dataset. Constant features are columns with only one unique value, providing no variability or useful information for modeling. Using the nunique() method, the code counts the unique values in each column and filters out those with only one unique value. These constant features are then dropped from the dataset to reduce dimensionality and avoid potential issues in subsequent modeling steps. The identified constant features include columns like 'V84', 'V402', among others.

## Dropping Constant Features

After identifying the constant features, the code proceeds to remove them from the dataset ('data_df'). This step ensures that only informative features remain, streamlining the dataset and enhancing the efficiency of the machine learning models. The resulting dataset, now free of constant features, is stored in the variable 'X'.

## Stratified Split

The next step involves splitting the dataset into training and testing sets using a stratified split. This ensures that both sets maintain the same class proportion as the original dataset. By specifying 'train_size=0.7', 70% of the data is allocated for training and 30% for testing. This stratification is crucial for maintaining the representativeness of the data, which is essential for reliable model evaluation.

## ANOVA F-test Feature Selection

To identify the most significant features, the code uses the ANOVA F-test. The 'SelectKBest' class, initialized with 'score_func=f_classif', ranks features based on their F-scores, which measure the variance between different classes. The top 20 features with the highest F-scores are selected. High F-scores indicate strong relationships with the target variable, while low P-values suggest statistical significance. For instance, features such as 'V18', 'V1936', and 'V1744' have very high F-scores, underscoring their importance in distinguishing between different classes.

## Creating and Sorting a DataFrame

To facilitate a better understanding of feature significance, a DataFrame is created that combines feature names, their F-scores, and P-values. This DataFrame is then sorted in descending order by F-score, highlighting the most important features. The top 50 features are printed, providing a clear view of the most impactful attributes, which is essential for focused analysis and model building.

## Visualizing Top Features

The following graph shows the top 20 features (gene expression that relates to how much of a gene product (protein) is being produced) 

![Top 20 Features from TCGA Dataset](https://github.com/AIDataWizard/Data-Analysis-TCGA/blob/main/Top_20_feat_plot.png?raw=true)
