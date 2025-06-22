# Detection of Triple Negative Breast Cancer from RNA sequencing data using Machine Learning

This is a college project where we investigated whether RNA sequencing (RNA-seq) data alone can be used to detect Triple Negative Breast Cancer (TNBC) using machine learning techniques. TNBC is an aggressive variant of breast cancer that responds particularly poorly to treatment. Using data from the TCGA-BRCA project, we developed a binary classification model to distinguish TNBC from non-TNBC cases. The goal was to evaluate different feature selection methods, compare model performance, and analyze the explainability of the best-performing models.

_Ruben Holthuijsen ([@rhlt](https://github.com/rhlt)) • Sander van Swieten ([@1063788](https://github.com/1063788)) • Vince van Doorn ([@Vinciepincie](https://github.com/Vinciepincie)) • Victor de Sousa Gama ([@VictordeSousaGama](https://github.com/VictordeSousaGama)) • Kevin Hartman ([@Kevin4032](https://github.com/Kevin4032))_

## Requirements

- Python 3.8+
- Jupyter Notebook 7.2+
- _Required packages_:
  - Pandas
  - scikit-learn
- Data from the TCGA-BRCA project

## Workflow

Below is a list of steps of the workflow that we have implemented. All steps (except Documentation) have a specific folder that contains one or more Jupyter notebooks where this step happens. Every notebook will import some existing data from the *Data* folder, work on it, and then export the result to a new file in the *Data* folder. These results are not committed to the repository. For every step, different variants may exist, for example for developing different models or selecting different features.

1. **[Data acquisition](./Data)**: Case data from the TCGA-BRCA project should go in the **Data** folder. See the README in that folder for instructions on how to acquire the data;
2. **[Data loading](./DataLoading)**: Cleaning, filtering, and classification (label generation) of the data is done in the **DataLoading** folder. This also links the clinical data to the correct RNA-seq files.
3. **[Preprocessing](./Preprocessing)**: Gene expression data is scaled and standardised in the **Preprocessing** folder.
4. **[Features](./Features)**: Features (genes) will be selected based on literature and other methods in the **Features** folder.
5. **[Model development](./Model)**: Different models are trained in the **Model** folder.
6. **[Model evaluation](./Evaluation)**: Performence of the trained models is evaluated in the **Evaluation** folder.
7. **[Model analysis](./Analysis)**: The results from our analysis of the different models and methods we applied, which was used to select the best performing model, can be found in the **Analysis** folder.
8. **Documentation and reporting**: The final report, as well as the original proposal, can be found in the top folder (here).

## Full process and results

The whole process and all results are documented in the final report that is included in this repository. In summary, the best performing model from our tests was a Random Forest using features selected via LASSO. It achieved a precision of 75.86%, recall of 95.65%, and F1-score of 84.62%. Additional explainability was achieved by applying LIME and SHAP.