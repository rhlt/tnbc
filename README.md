# Detection of Triple Negative Breast Cancer from RNA sequencing data using Machine Learning


## Workflow

Below is a list of steps of the workflow that we have implemented. All steps (except Documentation) have a specific folder that contains one or more Jupyter notebooks where this step happens. Every notebook will import some existing data from the *Data* folder, work on it, and then export the result to a new file in the *Data* folder. These results are not committed to the repository. For every step, different variants may exist, for example for developing different models or different features.

1. **Data acquisition**: Case data from the TCGA-BRCA project should go in the **Data** folder. See the README in that folder for instructions on how to aquire the data;
2. **Data preprocessing**: Cleaning, filtering, and classification (label generation) of the data is done in the **Preprocessing** folder. This also links the clinical data to the correct RNA Seq files.
3. **Feature selection**: Features (genes) will be selected based on literature and other methods in the **Features** folder.
4. **Model development**: Different models are trained in the **Model** folder.
5. **Model evaluation**: Visualizations of evaluation metrics are generated in the **Evaluation** folder.
6. **Interpretability and fairness analysis**: ***TODO*** (Analysis folder?)
7. **Documentation and reporting**: The final report, as well as the original proposal, can be found in the top folder.



***(NB: Hier moet dus nog meer definitiefs geschreven worden, voor nu is het hieronder een soort kladblok)***

## Introductie

In het GDC Data Portal staat data van het TCGA project over borstkanker (TCGA-BRCA). Hier vindt je onder andere RNA sequencing van meer dan duizend cases. Ook kan je gegevens over de patiënten en hun diagnose vinden. (Dit was een voorbeeld in de les.)

Het idee is om te kijken of we uit de RNA gegevens kunnen detecteren of een patiënt ‘Triple-negative breast cancer’ (TNBC) heeft. Dat is de meest agressieve vorm van borstkanker, die niet reageert op hormoontherapieën. Dit zou volgens mij heel nuttig zijn omdat hier nu alleen nog complexe methodes voor bestaan. Zie bijvoorbeeld deze bron:
> Triple Negative Breast Cancer: A Review of Present and Future Diagnostic Modalities: https://www.mdpi.com/1648-9144/57/1/62
 
De ‘Triple negative’ gaat over de Estrogen Receptor (ER), Progesterone Receptor (PR) en Human Epidermal Growth Factor Receptor 2 (HER2). De informatie over deze drie receptoren is beschikbaar in de patientdata; als ze allemaal ‘Negative’ zijn dan heeft die patient dus ‘Triple Negative’.

De bedoeling is om modellen te trainen die dat detecteert uit RNA data (zonder dus de clinical data nodig te hebben).


## Uitdagingen

De RNA bestanden zijn ruim 4 MB **per case**. Totaal is het zo’n 5 GB aan data. Dat is heel veel. Dit is wat ChatGPT erover zegt, dus zoiets zouden we dan moeten gaan doen als dit het project wordt:

> The file represents gene expression levels in different normalization formats:
> - TPM (Transcripts Per Million): Normalized for gene length and sequencing depth.
> - FPKM (Fragments Per Kilobase Million): Also accounts for transcript length.
> - FPKM-UQ (Upper Quartile normalization of FPKM): A more robust normalization method to reduce variability.
>
> **How This Relates to TNBC Detection**
> 
> Traditional TNBC (triple-negative breast cancer) diagnosis is based on immunohistochemistry (IHC), which stains for ER, PR, and HER2. While RNA-seq doesn't replace IHC in routine clinical use, it can detect molecular signatures that distinguish TNBC from other subtypes. In fact, RNA-seq can:
> 1.	Identify gene expression patterns associated with TNBC.
> 2.	Detect novel biomarkers for TNBC subtyping and prognosis.
> 3.	Support machine learning models that predict TNBC vs. non-TNBC status more precisely than standard methods.
> 
>  **Usability of This Data**
> 
> Yes, this data is usable for machine learning, but it needs processing and filtering to be feasible. The main challenges are:
> 
> - High dimensionality: 20,000+ genes per sample → requires feature selection.
> - Batch effects: Need normalization across different datasets.
> - Interpretability: Some low-expression genes may be noise rather than signal.
> 
> **How to Filter the Data for Model Training**
> 
> 1. Remove Low-Expression Genes:
>    - Drop genes with low TPM values across most samples (e.g., median TPM < 1).
> 2. Feature Selection (Reduce Dimensionality):
>    - Use variance thresholding (keep only genes with high variance across patients).
>    - Use differential expression analysis (keep genes that significantly differ between TNBC and non-TNBC).
>    - Apply principal component analysis (PCA) or autoencoders to reduce noise.
> 3. Normalize Across Samples:
>    - Convert raw counts to log-transformed TPM for more stable modeling.
> 4. Check for Batch Effects:
>    - Use techniques like Combat or limma to correct differences across sequencing batches.
>
> **Final Thoughts**
> 
> If your goal is TNBC classification, you’d likely train a supervised machine learning model using:
> - Clinical labels (TNBC vs. non-TNBC) as targets
> - Filtered RNA-seq expression values as features



## Verder onderzoek van de data

Een relevant onderdeel van de data is de 'clinical data'. Daarin staan 210 kolommen met diversiteit van data over de patient.
Bijvoorbeeld, geslacht, leeftijd, overlijden, diagnose, locatie.

De data is te vinden in file '8162d394-8b64-4da2-9f5b-d164c54b9608'.
Het gaat ons helpen wanneer we de data koppelen en filteren.

Daarnaast.
Ik heb geprobeerd beeld te krijgen bij de kolommen in 'cases'.
Bijvoorbeeld de eerste rij '6E7D5EC6-A469-467C-B748-237353C23416'.
Bestand '253aa5dc-9853-462a-9bcd-c2e44817833b.rna_seq.augmented_star_gene_counts.tsv'

'''
er_status_by_ihc	pr_status_by_ihc	her2_status_by_ihc
Positive		    Positive		    Negative
'''
