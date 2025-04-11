# (For inspiration only)



### **Abstract**  
This project aims to develop a machine learning model that can detect Triple Negative Breast Cancer (TNBC) from RNA sequencing data. TNBC is an aggressive form of breast cancer, and current diagnostic methods are complex and time-consuming. Using RNA-seq data from the TCGA, we will preprocess the data, train machine learning models, and evaluate performance to create a system that predicts TNBC status. We anticipate that the project will result in a more efficient diagnostic tool that can potentially complement existing methods.

---

### **1. Introduction**  
Triple Negative Breast Cancer (TNBC) is a subtype of breast cancer that does not express estrogen receptors (ER), progesterone receptors (PR), or HER2. It is one of the most aggressive types of breast cancer and has a poor prognosis. Traditional methods for TNBC diagnosis rely on immunohistochemistry (IHC), which can be time-consuming and limited in its predictive accuracy. The potential to use RNA sequencing data for TNBC detection offers a new approach that could be faster and more accurate, which is why this project uses RNA-seq data to explore this possibility using machine learning techniques.

---

### **2. Literature Review**  
A review of current research shows that while RNA-seq data has been utilized for cancer detection, its application specifically to TNBC diagnosis is still underexplored. Existing methods like IHC and genetic profiling are the standard, but they often fail to detect subtypes or misclassify patients. Research using RNA-seq in TNBC is promising, as gene expression patterns can differentiate TNBC from other subtypes. However, few studies integrate machine learning models to automate this process. This project fills this gap by leveraging machine learning to predict TNBC from RNA data.

**Key References:**
1. "A Review of Present and Future Diagnostic Modalities in TNBC," [Journal Article, Year]
2. [Another Relevant Paper, Year]
3. [Additional Relevant Papers, Year]

---

### **3. Problem Statement and Research Questions**  
The problem this project addresses is the complexity and inaccuracy of current TNBC diagnostic methods. Our key research questions are:
1. Can machine learning models effectively detect TNBC from RNA sequencing data?
2. What preprocessing methods (e.g., gene selection, dimensionality reduction) lead to the best model performance?
3. Can the model be optimized to ensure fairness and avoid biases related to demographic factors (age, race)?

---

### **4. Aim and Objectives**  
**Main Aim**:  
To develop and evaluate a machine learning model that can accurately predict TNBC status from RNA sequencing data.

**Objectives**:
1. Preprocess RNA-seq data to identify relevant gene expression features.
2. Train and optimize multiple machine learning models for TNBC classification.
3. Evaluate model performance using metrics such as accuracy, precision, recall, and fairness.
4. Investigate potential bias in the models and apply bias mitigation techniques to ensure fairness.
5. Deliver a final report and visualization of the results, including ethical considerations.

---

### **5. Significance of the Project**  
This project has technical, clinical, and societal significance. Technically, it provides a demonstration of how machine learning can be applied to large, high-dimensional RNA-seq datasets. Clinically, a well-trained model could aid in faster, more accurate TNBC detection, improving patient outcomes. Societally, reducing diagnostic errors and delays can have significant benefits for public health, especially for underserved populations.

---

### **6. Methodology**  
**6.1 Project Workflow**  
- **Data Preprocessing**:  
   - Match RNA-seq data with clinical metadata to get the correct patient samples.
   - Filter out genes with low expression across most samples.
   - Normalize the RNA-seq data (log transformation of TPM values).
   - Handle missing data and split the data into training and testing sets.

- **Feature Selection & Dimensionality Reduction**:  
   - Apply variance thresholding to retain the most informative genes.
   - Use PCA (Principal Component Analysis) to reduce the dimensionality of the dataset.

- **Model Development**:  
   - Train and evaluate multiple machine learning models: Logistic Regression, Random Forest, Support Vector Machine.
   - Optimize models using grid search or cross-validation.
   - Implement fairness metrics (balanced accuracy, fairness constraints).

- **Model Evaluation & Bias Mitigation**:  
   - Evaluate models using accuracy, recall, precision, and ROC-AUC.
   - Implement simple bias mitigation techniques like resampling or adjusting weights based on class imbalances.

**6.2 Tools**  
- **Python Libraries**:  
   - **Scikit-learn**: For training and evaluating machine learning models.  
   - **Pandas/Numpy**: For data manipulation and preprocessing.  
   - **Matplotlib/Seaborn**: For visualizations like ROC curves and confusion matrices.  
   - **Jupyter Notebook**: For developing and documenting code.

---

### **7. Dataset**  
The dataset comes from the TCGA (The Cancer Genome Atlas), specifically the TCGA-BRCA project, which provides RNA sequencing data for over 1,000 breast cancer cases. The data includes clinical metadata such as TNBC status, patient age, and ethnicity. Some patients have missing data, particularly for the TNBC-related columns, which we will address during preprocessing. The dataset is well-suited for machine learning but requires significant cleaning and preprocessing due to the high-dimensional nature of RNA-seq data.

---

### **8. Ethics**  
Ethical concerns include patient privacy, fairness, and transparency. The TCGA dataset is anonymized, so patient privacy is protected. To avoid bias, we will not include demographic features (age, race) in the model but will consider them during preprocessing for fairness mitigation. We will ensure the model is interpretable and provide transparency regarding the steps taken to ensure fairness.

**Bias Mitigation**:  
We will apply techniques such as resampling or adjusting class weights to address imbalances in the dataset. We will also assess the model for fairness using balanced accuracy and other metrics.

---

### **9. Plan, Team Collaboration, and Contribution of Each Member**  
- **Team Member 1**: Data collection, preprocessing, and matching RNA data with clinical metadata.
- **Team Member 2**: Feature selection, dimensionality reduction, and ensuring data quality.
- **Team Member 3**: Model development, training, and evaluation using Scikit-learn.
- **Team Member 4**: Ethics review, implementing bias mitigation, and evaluating model fairness.
- **Team Member 5**: Documentation, final report writing, and preparing results for presentation.

**Timeline**:
- **May 11 – May 17**: Finalize dataset, preprocessing, and feature selection.
- **May 18 – May 24**: Model development and training.
- **May 25 – June 7**: Model evaluation and bias mitigation.
- **June 8 – June 15**: Report writing, final analysis, and review.
- **June 16 – June 22**: Final deliverables preparation (code, report, results).

---

### **10. Deliverable**  
- **Code**: Python scripts for data preprocessing, model training, evaluation, and bias mitigation.
- **Report**: Final written report documenting methodology, results, analysis, and ethical considerations.
- **Visualizations**: Plots for model performance evaluation (e.g., ROC curves, confusion matrices).

---

### **11. Optional Sections**  
Risk mitigation plans: We will focus on basic explainability techniques (e.g., feature importance, model coefficients) if time permits. If the timeline becomes constrained, we may prioritize model optimization over additional explainability measures. In case of significant delays due to data processing or model performance issues, we will prioritize model simplification or use pre-trained models to demonstrate proof of concept.F

---

### **References**  
[1] Author(s), "A Review of Present and Future Diagnostic Modalities in TNBC," *Journal Name*, Year.  
[2] Author(s), "RNA-seq for Cancer Diagnostics," *Journal Name*, Year.  
[3] Additional references as needed.

---

This structure should provide a clear roadmap for the proposal and cover all the required sections while keeping things focused on the necessary tasks and timeline.