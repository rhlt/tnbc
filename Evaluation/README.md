# 5. Evaluation of models

***Prerequisite:** Files with model output and model metrics named **model_output_[variant].csv** and **model_metrics_[variant].csv**, for all model variants to be evaluated, must be generated as described in **[Model](../Model)**.*

This notebook applies multiple evaluation metrics to the models and visualizes them in MatPlotLib plots. The visualizations support plotting multiple variants at once for comparison, as defined near the top of the notebook.

These include classification report, confusion matrix, and the results of N-fold cross validation. The actual model training and cross-validation is performed in the previous step, this step does not perform any additional model training.

Unlike earlier steps, this step does not generate any output files (yet)
***[TODO: EXPORT VISUALIZATIONS FOR USE IN REPORT, WHEN/IF IT IS CLEAR WHAT WILL BE USED]***

***Next step***: Analyzing the generated models for transparency and validity with different demographic groups, as performed by the notebook in the **[Analysis](../Analysis)** folder, that lives next to this Evaluation folder.

## Key findings
In addition to generally confirming the key findings done in the previous step, it is very clear that the classification of TNBC has far less performance than the classification of non-TNBC.

