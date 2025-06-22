# 3. Preprocessing: Standardasation and scaling of gene expression data

***Prerequisite:** Data files must have been downloaded and initial classification applied as described in **[DataLoading](../DataLoading)**.*

The Jupyter Notebook in this folder will prepare the RNA sequencing data with the following process:

- Load the file generated in the previous step (`clinical.csv`) as a Pandas dataframe;
- Filter to include only genes with the biotype `protein_coding`;
- Extract expression values from the `stranded_first` column;
- Format the data into a single row, with gene names as columns;
- Add clinical metadata including TNBC label and Case ID;
- Handle duplicate case IDs and gene colums;
- Save the resulting dataframe to a new file **geneDataPreProcessed.csv** in the Data folder (this will not be included in the repository);

The resulting preprocessed data file can be loaded with the following code:

```py
dataPath = '../Data'
df = pd.read_csv(os.path.join(dataPath, 'geneDataPreProcessed.csv'))
```

***Next step:*** Jupyter Notebooks that parse the preprocessed data, select features using different methods, and link them from all RNA Seq files, can be found in the **[Features](../Features)** folder that lives next to this Preprocessing folder.


## Key findings
Each file contained expression data for **19,354** protein-coding genes. **24** duplicate genes have been handled. No duplicate case IDs were found.