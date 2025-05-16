# Obtaining data

This folder contains two files: `gdc_manifest.2025-04-01.222006.txt` and `metadata.cart.2025-04-01.json`.

The manifest file can be used to download the necessary data files. These are RNA-Seq files, and one clinical data file (`8162d394-8b64-4da2-9f5b-d164c54b9608`). The most straightforward way to obtain the actual files is the GDC Client command line tool found here: https://gdc.cancer.gov/access-data/gdc-data-transfer-tool

Run the following command in this directory: `gdc-client download -m gdc_manifest.2025-04-01.222006.txt` 
This will download gigabytes of data to the correct location that the script expect the data to be in (i.e., this folder).

Alternatively, if files are available locally or elsewhere, just copy them to this folder. Every file should be in a subfolder with its own UUID.

The metadata file allows linking the downloaded RNA files to the cases found in the clinical data, as follows:

````JSON
{
    "associated_entities": {
        "case_id": "XXX"
    },
    "file_id": "YYY",
    "file_name": "ZZZ"
}
````

***Next step:*** A Jupyter Notebook that parses both the downloaded metadata and clinical data to generate these links and determine TNBC status of all cases, can be found in the **Classification** folder that lives next to this Data folder.


## Obtaining the data from the GDC Data Portal

The manifest and metadata were obtained from the GDC Data Portal in the following way:

- Search for **TCGA-BRCA** (breast cancer project) or the following direct link: https://portal.gdc.cancer.gov/projects/TCGA-BRCA
- **Save New Cohort**, click **Repository**, open the cohort: 1098 cases.
- For the RNA sequencing files, filter by: Experimental Stragegy: **RNA-Seq**, Access: **Open**, Tissue Type: **Tumor**. Result: 1118 files of 1095 cases. Click **Add all files to cart**.
- For clinical data: Reset filters, then filter by: Data Category: **Clinical**, Data Format: **bcr biotab**. This will bring up the following file: **nationwidechildrens.org_clinical_patient_brca.txt** (1.7MB), add that to cart as well.
- Open the cart (button at top) and select **Download Cart** > **Manifest**. Then, do the same for **Metadata** (button slightly further to the right, near Remove Cart).