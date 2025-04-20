# Mogelijk voorstel voor Capstone Project: Triple Negative Breast Cancer uit RNA gegevens

In het GDC Data Portal staat data van het TCGA project over borstkanker (TCGA-BRCA). Hier vindt je onder andere RNA sequencing van meer dan duizend cases. Ook kan je gegevens over de patiënten en hun diagnose vinden. (Dit was een voorbeeld in de les.)

Mijn idee is om te kijken of we uit de RNA gegevens kunnen detecteren of een patiënt ‘Triple-negative breast cancer’ (TNBC) heeft. Dat is de meest agressieve vorm van borstkanker, die niet reageert op hormoontherapieën. Dit zou volgens mij heel nuttig zijn omdat hier nu alleen nog complexe methodes voor bestaan. Zie bijvoorbeeld deze bron:
> Triple Negative Breast Cancer: A Review of Present and Future Diagnostic Modalities: https://www.mdpi.com/1648-9144/57/1/62
 
De ‘Triple negative’ gaat over de Estrogen Receptor (ER), Progesterone Receptor (PR) en Human Epidermal Growth Factor Receptor 2 (HER2). De informatie over deze drie receptoren is beschikbaar in de patientdata; als ze allemaal ‘Negative’ zijn dan heeft die patient dus ‘Triple Negative’.

Het idee zou zijn om een model te trainen die dat detecteert uit RNA data.

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


## Downloaden van de data

In deze repository vind je twee bestanden: `gdc_manifest.2025-04-01.222006.txt` en `metadata.cart.2025-04-01.json`.

Met het manifest kan je de juiste bestanden downloaden. Gebruik hiervoor de GDC Client command line tool: https://gdc.cancer.gov/access-data/gdc-data-transfer-tool

Command: `gdc-client download -m gdc_manifest.2025-04-01.222006.txt` 

(Let op, dan ga je 5 GB aan bestanden downloaden)

Met de informatie uit het metadata-bestand kan je de RNA bestanden aan de juiste patient koppelen:

````JSON
{
    "associated_entities": {
        "case_id": "XXX"
    },
    "file_id": "YYY"
}
````

## Zelf de data vinden in het GDC Data Portal

- Zoek op **TCGA-BRCA** (borstkanker data) of directe link: https://portal.gdc.cancer.gov/projects/TCGA-BRCA
- **Save New Cohort**, klik op **Repository**, open het cohort: 1098 cases.
- Voor de RNA sequencing, filter op: Experimental Stragegy: **RNA-Seq**, Access: **Open**, Tissue Type: **Tumor**. Resultaat: 1118 files van 1095 cases. Klik op **Add all files to cart**.
- Voor patientgegevens/diagnose: Reset filters, en dan: Data Category: **Clinical**, Data Format: **bcr biotab**. Je ziet o.a. bestand: **nationwidechildrens.org_clinical_patient_brca.txt** (1.7MB), voeg die ook toe aan cart.
- Open de cart (bovenaan) en kies **Download Cart** > **Manifest**. En daarna ook **Metadata** (knop iets verder naar rechts, naast Remove Cart).



## Eerste onderzoek van de data

Ik ben zelf in de data gedoken van de cases om uit te zoeken hoe bruikbaar het is. Niet bij alle gevallen zijn alledrie de relevante kolommen ingevuld, maar als er ook maar één waarde "Positive" is weten we dat dat in ieder geval geen _triple negative_ is. Ook heb ik de cases gematcht met de RNA bestanden. Het resultaat staat in de Excel file "Cases.xlsx".

Hieruit komt dat we van 863 cases weten dat het _niet_ triple negative is, van 116 dat het _wel_ triple negative is, en van 118 weten we het niet. RNA files hebben we van bijna alle cases, op 3 na (waarvan 1 niet triple negative, 1 wel en ook 1 onbekende). Zo houden we dus **977** cases over met bruikbare data. Net iets minder dan de gevraagde 1000, maar valt me nog alles mee.


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

Als ik aan AI vraag hoe 'er', 'pr' en 'her2' te bepalen zijn is het antwoord;
   - ESR1 for estrogen receptor (ER)
   - PGR for progesterone receptor (PR)
   - ERBB2 for HER2

Als ik voor voorgenoemde data ga kijken, zijn alle drie aanwezig.

Hoe komt 'her2' op negative? Is mijn beeld, gedachtengang hierboven, verkeerd?

Tot slot, het inlezen van de cohort data (de bron van 'cases') heb ik gezet in
\data\cohortdata.ipynb



