# Correctness Metrics Interactive Runner

An interactive Python tool to compute and visualize *correctness* (congruence) metrics across multiple patient and synthetic feature datasets.

---

## Table of Contents

- [Overview](#overview)  
- [Directory Structure](#directory-structure)  
- [Dependencies](#dependencies)  
- [Configuration](#configuration)  
- [Usage](#usage)  
- [Code Structure](#code-structure)  
- [Examples](#examples)  
- [License](#license)  

---

## Overview

This script allows you to:

- **Load** pre-computed feature CSV files (samples × features) for any number of real (patient) and synthetic datasets.  
- **Choose** among three sampling strategies to handle unequal dataset sizes:  
  1. **No sampling** (use full arrays)  
  2. **Subsample once** (random draw to equalize counts)  
  3. **Bootstrap aggregate** (repeat subsampling and average results)  
- **Compute** seven core metrics with both *manual* and *library* implementations for cross-validation:  
  - Cosine Similarity  
  - Pearson Correlation  
  - Manhattan (L1) Distance  
  - Mahalanobis Distance  
  - Jensen–Shannon Divergence  
  - Earth Mover’s Distance (Wasserstein)  
  - Fréchet Inception Distance (FID)  
- **Generate** per-pair CSV tables and console summaries, automatically collapsing identical manual vs. library values.  
- **Visualize** results via:  
  - Raw feature PCA scatter  
  - Per-dataset feature histograms  
  - Bar plots of each metric  
  - Annotated heatmaps (patient vs. synthetic, within-patients, within-synthetics)  
  - Histograms of metric distributions  

---

## Directory Structure

```
.
├── README.md
├── correctness_metrics.py      # Interactive runner script
├── requirements.txt            # Python dependencies
└── data/
    ├── patient/                # e.g. InBreast.csv, MIAS.csv
    └── synthetic/              # e.g. MSYNTH.csv, Mammo_medigan.csv

# Outputs under:
└── results/
    ├── raw_pca.png             # PCA scatter plot
    ├── <dataset>_feature_hist.png  # Histogram of raw features
    ├── tables/                 # Per-pair CSV metric tables
    ├── barplots/               # Bar plots for each metric
    ├── heatmaps/               # Annotated heatmaps
    └── histograms/             # Histograms of metric values
```

---

## Dependencies

Install via:

```bash
pip install -r requirements.txt
```

**requirements.txt**:
```text
numpy>=1.21
pandas>=1.3
matplotlib>=3.4
scipy>=1.7
scikit-learn>=1.0
```

---

## Configuration

All inputs and outputs are specified at runtime via interactive prompts:

- Enter **patient** and **synthetic** CSV file paths (space-separated).  
- Choose a **sampling method** (1 – no sampling, 2 – subsample once, 3 – bootstrap aggregate).  
- Select **comparisons** to run (patient vs. synthetic, within-patients, within-synthetics).  
- Specify an **output directory**.  
- Opt to **plot raw PCA** and **feature histograms**.  
- Pick **visualization modes** (bar plots, heatmaps, histograms).

No hard-coded file paths.

---

## Usage

```bash
python correctness_metrics.py
```

Follow the prompts to:

1. Provide feature CSV file paths.  
2. Select sampling strategy.  
3. Choose which comparisons to compute.  
4. Optionally plot raw PCA and feature histograms.  
5. Enter an output directory.  
6. Choose visualization modes.

All results are saved under your specified `results/` folder.

---

## Code Structure

1. **I/O Prompts**  
   - `prompt_paths()`, `ask_bool()`: gather user inputs.  
2. **Metric Functions**  
   - Manual vs. SciPy implementations for each metric.  
3. **Sampling Strategies**  
   - `compute_metrics_nosample()`, `compute_metrics_subsample()`, `compute_metrics_bootstrap()`  
4. **Pairwise Loop**  
   - Builds DataFrame of metrics for each dataset pair.  
5. **Raw Feature Visualization**  
   - PCA scatter using `sklearn.decomposition.PCA`  
   - Flattened feature histograms  
6. **Output & Visualizations**  
   - Per-pair CSV tables  
   - Console summaries collapsing identical metric pairs  
   - Bar plots, annotated heatmaps, and histograms of metric values  

---

## Examples

After running, check:

- `results/raw_pca.png`  
- `results/InBreast_feature_hist.png`  
- `results/tables/InBreast_vs_MSYNTH.csv`  
- `results/barplots/Cosine_manual_bar.png`  
- `results/heatmaps/Pearson_pvss_heatmap.png`  
- `results/histograms/FID_hist.png`  

to explore numeric and visual comparisons.

---

## License

[Your License Here]
