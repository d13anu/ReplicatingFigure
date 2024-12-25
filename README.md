# Replicating Figures 2b and 3c from the Research Article: 
**Multiplex cerebrospinal fluid proteomics identifies biomarkers for diagnosis and prediction of Alzheimer’s disease**

This repository provides the code and methodology for replicating Figures 2b (Volcano Plot) and 3c from the referenced research article.

---

## Table of Contents
1. [Introduction](#introduction)
2. [Requirements](#requirements)
3. [Data Preparation](#data-preparation)
4. [Generating Figure 2b: Volcano Plot](#generating-figure-2b-volcano-plot)
5. [Additional Information](#additional-information)
6. [Acknowledgments](#acknowledgments)

---

## Introduction
The objective is to identify biomarkers for Alzheimer’s Disease (AD) using cerebrospinal fluid (CSF) proteomics. The steps involve:
- Filtering and preprocessing the dataset.
- Conducting multiple linear regression on protein expression data.
- Adjusting p-values for multiple comparisons.
- Visualizing results with a volcano plot.

---

## Requirements
### Python Libraries
- `pandas`: For data manipulation and preprocessing.
- `matplotlib`: For creating plots.
- `numpy`: For mathematical computations.
- `adjustText`: For text annotation adjustment in plots.
- `statsmodels`: For statistical analysis and regression modeling.

### Data Files
Ensure the following files are in the working directory:
1. **adnimerge_dataR.csv**: Baseline ADNI data.
2. **ADNI_Analyte_expression_data.csv**: Analyte expression data.
3. **ADNI_Analyte_protein_info.csv**: Analyte-protein mapping data.

---

## Data Preparation
### Step 1: Load and Filter ADNI Data
- Load **adnimerge_dataR.csv**.
- Filter for:
  1. Baseline data (`VISCODE` contains "bl").
  2. Control (CN) and Alzheimer’s (AD) samples (`DX.bl` contains "CN" or "AD").

### Step 2: Load Analyte Expression Data
- Load **ADNI_Analyte_expression_data.csv**.
- Merge with filtered ADNI baseline data using the `RID` column.

### Step 3: Preprocess Expression Data
- Log-transform protein expression values.
- Standardize (Z-transform) for normalization.
- Handle missing values by imputing column means.

---

## Generating Figure 2b: Volcano Plot
### Step 1: Perform Multiple Linear Regression
- Regress each protein's expression against clinical covariates (`AGE`, `PTGENDER`, `PTEDUCAT`, `APOE4`) and diagnostic status (`DX.bl`).
- Extract beta coefficients and p-values for diagnostic status (`DX.bl`).

### Step 2: Adjust P-values
- Use Bonferroni correction for multiple testing.
- Compute `-log10` values of raw and adjusted p-values.

### Step 3: Annotate Proteins
- Cross-reference protein analytes with gene symbols from **ADNI_Analyte_protein_info.csv**.

### Step 4: Plot the Volcano Plot
- **X-axis**: Beta coefficients (effect size).
- **Y-axis**: `-log10(adjusted p-value)`.
- Highlight significant proteins (e.g., threshold: p-value < 0.05).

---

## Additional Information
### Data Outputs
- Filtered dataframes and regression results are saved for reproducibility.
- Volcano plot is saved as a `.png` file in the working directory.

### Key Functions
- **`multipletests`**: For Bonferroni correction.
- **`OLS`**: Ordinary Least Squares regression for linear modeling.

---

## Acknowledgments
This work is based on the methods described in the research article:  
**Multiplex cerebrospinal fluid proteomics identifies biomarkers for diagnosis and prediction of Alzheimer’s disease**.  

For questions or issues, please contact anudon@bu.edu.
