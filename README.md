# Semi-Untargeted UPLC-TQ/MS Serum Metabolomics Pipeline 

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
---

## ✍️ Authors & Affiliations
- **Jorge Hurtado Soriano** — Universidad Autónoma de la Ciudad de México (UACM) / Instituto Nacional de Geriatría (INGER) / INPer.
- **Selma Karime Castillo Vásquez**.
