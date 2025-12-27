# suicide-temporal-patterns-mexico

Reproducible pipeline for analyzing temporal patterns in suicide mortality in Mexico using microdata from the *Estadísticas de Defunciones Registradas* (EDR).  
The project applies moving-window analysis, robust outlier detection, and metropolitan-level aggregation to explore seasonal dynamics and population heterogeneity.

---

## Overview

This repository contains a fully reproducible data pipeline designed to study **temporal variation in suicide mortality** at multiple spatial and demographic scales in Mexico.

Rather than focusing on single dates or monthly averages, the analysis compares **moving windows of fixed length (8 days)** across the entire year. This approach allows the identification of short-term peaks, typical periods, and deviations from usual temporal behavior without relying on strong parametric assumptions.

The project was developed as an exploratory and descriptive analysis, with particular attention to careful interpretation and avoidance of overstatement.

---

## Data Sources

All analyses are based on publicly available, official data:

- **Estadísticas de Defunciones Registradas (EDR)**  
  Instituto Nacional de Estadística y Geografía (INEGI), Mexico  
  Microdata at the individual death-record level.

- **Metropolitan areas and municipal bridges**  
  Official metropolitan definitions and municipality-to-metropolis mappings.

- **Auxiliary catalogs**  
  ICD-10 suicide classifications, sex, education, occupation, nationality, and civil status catalogs provided by INEGI.

No proprietary or confidential data are used.

---

## Methodological Approach

The pipeline follows five main stages:

### 1. Data Cleaning and Harmonization
Raw EDR microdata are cleaned and standardized, including:
- date construction from day and month fields,
- harmonization of geographic identifiers,
- translation of coded variables into human-readable labels,
- filtering of suicide-related causes using ICD-10 codes.

The output of this stage is a cleaned, analysis-ready dataset.

### 2. Geographic Aggregation
Individual records are linked to **zones metropolitanas** using official municipality–metropolis bridges.  
Where applicable, residence and occurrence locations are treated separately to preserve spatial context.

### 3. Moving-Window Temporal Analysis
Instead of calendar weeks or months, the analysis uses **rolling windows of 8 consecutive days** across the year.  
For each window, suicide counts are computed and compared to all other windows.

This allows:
- consistent comparisons between periods,
- identification of true short-term peaks,
- avoidance of arbitrary temporal cutoffs.

### 4. Robust Outlier Assessment
To evaluate whether specific periods behave exceptionally, the pipeline uses:
- percentile-based comparisons,
- robust measures of dispersion (Median Absolute Deviation, MAD).

This avoids overinterpreting rare but extreme observations.

### 5. Population Heterogeneity
All analyses are replicated across population subgroups, including:
- sex,
- age groups (15-year intervals),
- selected sociodemographic variables.

Geographic variation is explored at the metropolitan level.

---

## Outputs

The repository generates several analysis-ready outputs, including:

- Cleaned microdata suitable for replication.
- National-level temporal distributions.
- Group-specific temporal comparisons.
- Metropolitan-level summaries for mapping and visualization.

All outputs are stored in the `Output/` directory and can be regenerated from raw data.

---

## Interpretation Notes

This project is **descriptive** in nature.

- Results should be interpreted at the **population level**, not as individual risk estimates.
- The analysis does **not** make causal claims.
- Short temporal windows may produce unstable rates for small populations; therefore, most visualizations rely on counts and relative comparisons rather than short-period rates.

The goal is to better understand **when** suicide mortality tends to concentrate over the year, not **why** it occurs.

---

## Repository Structure

```text
Repositorio/
├── Data/
│   ├── EDR_Catalogos/        # ICD-10 and auxiliary catalogs
│   └── Metro/                # Metropolitan definitions and bridges
├── Output/                   # Cleaned data and analysis outputs
├── SuicidiosNavideños.ipynb  # Main analysis notebook
└── README.md
Reproducibility

All steps are fully reproducible using the provided notebooks, assuming access to the original EDR microdata.

The analysis was developed in Python using standard scientific libraries (pandas, numpy, matplotlib).

Disclaimer

⚠️ Important
This repository presents a descriptive, exploratory analysis of suicide mortality data.
It does not assess individual-level risk, does not establish causality, and should not be used for clinical decision-making.

If you or someone you know is experiencing emotional distress or suicidal thoughts, please seek professional help or contact local support services.

Contact

For questions, feedback, or collaboration proposals related to spatial or temporal data analysis, feel free to reach out:

Moschata Analytics
Geospatial and demographic data analysis
📩 Contact details available upon request

License

This project is released for academic and research purposes.
Please cite the original data sources (INEGI) when using or adapting this work.
