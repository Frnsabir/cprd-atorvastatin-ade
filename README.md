# Ethnic Disparities in Adverse Drug Events Among Adults Prescribed Atorvastatin  


---

## 📘 Project Overview
This repository contains **R scripts, configuration files, and documentation** for the project:

> **“Ethnic Disparities in Adverse Drug Events Among Adults Prescribed Atorvastatin”**  
> A retrospective cohort study using CPRD Aurum linked with Hospital Episode Statistics (HES) APC  
>  and Index of Multiple Deprivation (IMD) data.

The project explores how **ethnicity and clinical factors** influence the risk of adverse drug events (ADEs)  
following initiation of atorvastatin in adults aged ≥18 years.

The repository will be used to share codelist for this project, cohort formation and and analysis scripts

## ⚙️ Repository Structure

| Folder | Purpose |
|---------|----------|
| `R/` | All main analysis scripts |
| `R/utils/` | Helper functions (dates, polypharmacy, IMD recoding, etc.) |
| `config/` | Study configuration files (e.g., `study.yml`) |
| `codelists/` | SNOMED/BNF code lists for exposures, covariates, and outcomes |
| `data_raw/` | ⚠️ *Not tracked in Git* – raw CPRD/HES/IMD data (stored securely in TRE) |
| `data_derived/` | ⚠️ *Not tracked in Git* – derived analysis datasets |
| `logs/` | Local processing logs and QC summaries (excluded from Git) |
| `outputs/` | Analysis outputs (tables, figures, model objects) |
| `docs/` | Protocol snippets, flow diagrams, and supporting documents |

All folders are created automatically by the setup script `00_setup_project.R`.

---

## 📈 Analysis Pipeline
The analysis follows a structured sequence of numbered scripts:

1. **00_setup_project.R** — create folder structure & initialise local Git repo  
2. **01_preprocessing_import_clean.R** — import and clean CPRD data  
3. **02_data_linkage.R** — link HES APC and IMD data  
4. **04_define_exposure_and_index.R** — define first atorvastatin prescription (index date)  
5. **05_primary_vs_secondary_prevention.R** — classify prevention type  
6. **06_covariates_baseline.R** — derive baseline covariates (ethnicity, polypharmacy, comorbidity, etc.)  
7. **07_outcome_definitions.R** — identify ADE outcomes  
8. **08_followup_censoring.R** — define follow-up periods and censoring  
9. **09_analysis_dataset_build.R** — merge analysis-ready datasets  
10. **10_models_primary.R** — main logistic and Cox models  
11. **11_models_sensitivity.R** — adherence (PDC ≥ 80%) & time-varying Cox sensitivity analyses  
12. **12_results_tables_figures.R** — output results and figures  
13. **13_qc_and_repro_report.R** — quality-control and reproducibility checks

---

## 📊  Key Variables
- **Exposure:** Atorvastatin initiation (first prescription between 2014–2023)  
- **Covariates:** Ethnicity, age, sex, IMD quintile, smoking, alcohol, BMI, polypharmacy, Cambridge Multimorbidity Score and healthcare utilisation
- **Outcomes:** Categorised in two groups:  
  - *Short-term ADEs:* Myopathy, rhabdomyolysis, Creatinine Kinase (CK) elevation >3x ULN, AKI, Statin Intolerance, Hepatotoxicity  
  - *Long term ADEs:* New-onset of type 2 diabetes, Cognitive Impairment, Falls, Fractures, CKD Progression renal and mortality

---

## 🔒 Data Governance and Privacy
This code was developed and executed within a **Trusted Research Environment (TRE)**.  
All patient-level data remain within the TRE and are not included in this repository.

**No identifiable or raw data** are shared here.  
All scripts are designed for **offline use** within the TRE and comply with CPRD data governance requirements.

---

## ⏳ Dependencies
The analysis uses **base R (≥4.3)** and the following CRAN packages:

`tidyverse`, `data.table`, `lubridate`, `arrow`, `survival`, `broom`, `janitor`, `here`, `yaml`

No external API calls or internet dependencies are required.

---

## 🧑‍💻 Version Control
A local Git repository is initialised automatically by `00_setup_project.R` for safe offline version tracking.  
When code is exported and approved for release, connect to GitHub manually:

```bash
git remote add origin https://github.com/<username>/cprd-atorvastatin-ade.git
git branch -M main
git push -u origin main
