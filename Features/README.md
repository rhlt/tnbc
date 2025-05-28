# 3. Feature Selection: selecting genes using different methods

***Prerequisite:** Preprocessed clinical data must be available in **clinical.csv** as described in **Preprocessing**.*

The Jupyter Notebooks in this folder will extract the the selected features from the RNA Seq files and combine them with the labeled clinical data with the following process:

- Load the preprocessed Clinical Datafile as a Pandas dataframe, keeping only the case ID, TNBC label, and linked RNA Seq filename;
- Determine the features to be selected (based on literature, statistical analysis or automated dimensionality reduction, depending on notebook);
- Extract the selected features from the RNA Seq files and add these to the labeled clinical dataframe.
- Add the matched files to the clinical dataframe, dropping cases where no RNA Seq file is available;
- Save the resulting dataframe to a new file **patient_genes_[variant].csv** in the Data folder (this will not be included in the repository);

The generated file with the selected features can be loaded with the following code:

```py
dataPath = '../Data'
df = pd.read_csv(os.path.join(dataPath, 'patient_genes_[variant].csv')) # replace [variant] with the variant to use as input (literature, statistical, automated)
```

***Next step:*** Jupyter Notebooks that train different models based on the selected features can be found in the **Model** folder that lives next to this Features folder.


## Key findings
From to the available clinical data, 116 can be determined as triple negative (TNBC), as the three relevant  columns are 'Negative'. A further 863 cases can be determined as _not_ triple negative (meaning at least one 'Positive' value in the appropriate columns). This leaves 118 indeterminable cases.

RNA Sequencing files are missing for 3 cases (1 TNBC, 1 non-TNBC, 1 indeterminable), leaving a total of **977** cases with usable data.