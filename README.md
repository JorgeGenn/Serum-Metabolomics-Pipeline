# Semi-Untargeted UPLC-TQ/MS Serum Metabolomics Pipeline 

[![Platform](https://img.shields.io/badge/Platform-UPLC--MS%2FMS%20(Waters%20Xevo%20TQ--S)-blue)](#)
[![Software](https://img.shields.io/badge/Software-MS--DIAL%20v4.92%20%7C%20MetaboAnalyst%206.0-orange)](#)
[![Institutions](https://img.shields.io/badge/Institutions-UACM%20%7C%20INPer%20%7C%20INGER-green)](#)

## 📌 Overview
This repository details the bioinformatics protocol and analytical pipeline for semi-untargeted metabolomic processing of human serum samples acquired via **UPLC-TQ-MS/MS (Waters Xevo TQ-S)**. 

The analytical workflow addresses low-resolution MS1 centroid data processing, peak detection, retention time alignment, adduct selection, batch correction, and covariate-adjusted statistical analysis (limma/ANOVA) for cognitive impairment research.

---

## 🔬 Experimental Setup & Acquisition
- **Instrumentation:** Waters ACQUITY UPLC coupled to Xevo TQ-S Mass Spectrometer (ESI+ mode).
- **Stationary Phase:** ACQUITY UPLC BEH Amide Column (1.7 µm, 2.1 x 100 mm).
- **Mobile Phase:** Ammonium Formate (10 mM, pH buffer) & Acetonitrile (LC-MS Grade).
- **Data Acquisition Mode:** Precursor ion scan / MS1 centroid mode (50–2000 Da range).

## 🛠️ Bioinformatics Protocol

### 1. File Conversion
- Convert vendor `.RAW` files to open formats (`.mzML` or `.abf`) using **ProteoWizard MSConvert** (Vendor peak picking enabled on MS1)

- ### 2. MS-DIAL Processing Parameters (v4.92)
- **Data Type:** Soft ionization (LC-MS) | Centroid data (MS1) | ESI Positive.
- **Peak Detection:** Minimum peak height: 3000 amplitude; Mass slice width: 0.1 Da.
- **Smoothing:** Linear-weighted moving average (level 1, min peak width: 5 scans).
- **Identification:** Matched against **MoNA (MassBank of North America)** spectral library (`.msp`) with ID score cutoff > 80%.
- **Adducts Included:** `[M+H]+`, `[M+Na]+`, `[M+NH4]+`, `[M+K]+`, `[2M+H]+`, among others.
- **Alignment:** QC-based alignment with RT tolerance of 0.05 min and MS1 tolerance of 0.015 Da. Blank subtraction enabled.

- ### 3. Statistical Analysis & Quality Control (MetaboAnalyst 6.0)
- **Technical Replicates:** Merged using arithmetic mean (`Merging Technical Replicates`).
- **Batch Correction & Normalization:** Normalized by sum, square root transformation, and mean centering.
- **Filtering:** RSD > 20% filter applied on QC samples.
- **Statistical Testing:** Univariate linear modeling via `limma` adjusting for covariates (e.g., Diagnostic, Sex) with FDR $p < 0.05$.

---

## 🔒 Data Availability
Due to ethical constraints and patient privacy regulations regarding clinical serum samples, raw spectral files (`.RAW`) are restricted. 

- **Demo Data:** A template metadata file (`metadata_example.csv`) and processed peak intensity matrix are provided in `/data` for pipeline evaluation.
- **Data Access:** De-identified data can be made available upon reasonable request through a Data Use Agreement (DUA).
---

## ✍️ Authors & Affiliations
- **Jorge Hurtado Soriano** — Universidad Autónoma de la Ciudad de México (UACM) / Instituto Nacional de Geriatría (INGER) / INPer.
- **Selma Karime Castillo Vásquez** Universidad Nacional Autónoma de México (UNAM).
