# 3. Feature Selection: selecting genes using different methods

***Prerequisite:** Preprocessed clinical data must be available in **clinical.csv** as described in **[Preprocessing](../Preprocessing)**.*

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

***Next step:*** Jupyter Notebooks that train different models based on the selected features can be found in the **[Model](../Model)** folder that lives next to this Features folder.


## Key findings ***[TODO]***

The RNA Seq files contain gene expression data for tens of thousands of genes, each of which has different expression values. Based on ***[WAT PRECIES]*** we have learned that **stranded_first** is the most appropriate value to use.

Based on literature ***[WAAR KWAM DEZE VANDAAN]***, a list of 20 genes was selected for initially: TBC1D9, GATA3, SLC16A6, ESR1, INPP4B, SLC44A4, ANXA9, AGR2, MCCC2, TSPAN1, STBD1, MLPH, CACNA2D2, RARA, STARD3, PPP1R14C, SFRS13B, LDHB, MFGE8, PSAT1.

Using statistical analysis, a ***similar/different*** list was found **(VINCE)** .....

With automated methods such as PCA **(RUBEN)** ......

## Suggestions for improvement ***[TODO IF TIME PERMITS]***
- Apply SMOTE to remove the imbalance
- Different feature-sets
- Normalize data; in the TCGA-BRCA data the column 'stranded_first' is used. Values range from 0 (missing) to over 30782951