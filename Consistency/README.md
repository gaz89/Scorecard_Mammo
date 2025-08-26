# Consistency‐Across‐Subgroups Analysis

This repository provides an interactive Jupyter notebook and supporting CSV files to assess the **consistency** of Synthetic Mammography Data (SMD) quality metrics across user‐defined subgroups (e.g. breast density, BI-RADS). You can compute a suite of variability and statistical‐test metrics, then explore them with bar charts, heatmaps, box/violin plots and more.

---

## Table of Contents

1. [Overview](#overview)  
2. [Directory Structure](#directory-structure)  
3. [Dependencies](#dependencies)  
4. [Usage](#usage)  
5. [Notebook Sections](#notebook-sections)  

---

## Overview

**Consistency** measures how stable SMD quality (Correctness, Coverage, Constraint, Completeness, etc.) is across different patient subgroups or time points. This analysis computes for each dataset and each metric:

- **Variance**  
- **Range** (max − min)  
- **Coefficient of Variation** (std/mean)  
- **Interquartile Range** (IQR)  
- **Median Absolute Deviation** (MAD)  
- **ANOVA p-value** (one-way ANOVA across subgroups)  
- **Levene’s test p-value** (homogeneity of variances)

Then you can interactively visualize and interpret which synthetic datasets are most or least uniform across subgroups.

---

## Directory Structure

├── README.md
├── consistency_analysis.ipynb # Main interactive notebook
├── requirements.txt # Python dependencies
├── Consistency_density.csv # Synthetic breast‐density subgroup metrics
├── Consistency_birads.csv # Synthetic BI-RADS subgroup metrics
└── plots/ # (Optional) generated figures



---

## Dependencies

- **Python** ≥ 3.8  
- **pandas** ≥ 1.0  
- **numpy** ≥ 1.18  
- **matplotlib** ≥ 3.0  
- **seaborn** ≥ 0.10  
- **scipy** ≥ 1.4  

Install all requirements with:

```bash
pip install -r requirements.txt
