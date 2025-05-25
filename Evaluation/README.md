# Evaluation of models

Multiple evaluation metrics are applied to the models.
These include classification report, confusion matrix, and 5-fold cross validation.

## Key findings
Classification of TNBC has far less performance than the classification of nTNBC.

Suggestions for improvement;
- Apply SMOTE to remove the imbalance
- Different feature-sets
- Normalize data; in the TCGA-BRCA data the column 'stranded_first' is used. Values range from 0 (missing) to over 30782951

