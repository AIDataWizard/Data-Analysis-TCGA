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

![Top 20 Features from TCGA Dataset](https://github.com/AIDataWizard/Data-Analysis-TCGA/blob/main/Top_20_feat_plot.png?raw=true)
