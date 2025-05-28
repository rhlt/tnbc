# 2. Preprocessing: Classification and Filtering of clinical data

***Prerequisite:** Data files (Clinical and RNA sequencing) must have been downloaded as described in **Data**.*

The Jupyter Notebook in this folder will classify and filter the raw clinical data with the following process:

- Load the Clinical Datafile as a Pandas dataframe;
- Determine TNBC status by the columns `er_status_by_ihc`, `pr_status_by_ihc`, and `her2_status_by_ihc`, dropping indeterminable cases;
- Match RNA Seq files to Case IDs using the Metadata file;
- Add the matched files to the clinical dataframe, dropping cases where no RNA Seq file is available;
- Save the resulting dataframe to a new file **clinical.csv** in the Data folder (this will not be included in the repository);

The resulting preprocessed data file can be loaded with the following code:

```py
dataPath = '../Data'
df = pd.read_csv(os.path.join(dataPath, 'clinical.csv'))
```

***Next step:*** Jupyter Notebooks that parse the clinical data, select features using different methods, and link them from all RNA Seq files, can be found in the **Features** folder that lives next to this Preprocessing folder.


## Key findings
From to the available clinical data, 116 can be determined as triple negative (TNBC), as the three relevant  columns are 'Negative'. A further 863 cases can be determined as _not_ triple negative (meaning at least one 'Positive' value in the appropriate columns). This leaves 118 indeterminable cases.

RNA Sequencing files are missing for 3 cases (1 TNBC, 1 non-TNBC, 1 indeterminable), leaving a total of **977** cases with usable data.