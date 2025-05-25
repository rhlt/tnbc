# Basic implementations of ML models

## Prerequisites

- Python 3.8+
- Required packages
  - Pandas
  - scikit-learn
- patient_genes.csv: Run the following [notebook](Preparation\PrepareData.ipynb) if the file does not exist in tnbc/Data/

### Notebook contents [[#notebook]](Model\Model.ipynb)

This notebook contains the initial setup of the ML models based on the algorithms specified in the proposal:

- Logistic Regression
- Support Vector Machines (SVM)
- Random Forest

Dataset used:

- patient_genes.csv

Uses sklearn.model_selection.train_test_split() to split the dataset:

- 80% training data
- 20% test data

Each model is trained on the training set, evaluated on the test set, and basic validation is performed with n-fold cross-validation (n=5).

A summarization of the cross-validation results can found be at the end of the notebook.

### Next step

Applying additional evalutions and validations and creating additonal metrics
to properly assess models.
