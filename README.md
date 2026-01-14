# Stromatoporoid reef size (v16) — main analysis notebook

This repository contains the full analysis workflow for **stromatoporoid reef morphology / reef size** and its relationship to **PBDB diversity** and **environmental proxy time series**.

All input files required by the notebooks are already included in the GitHub repository (so the “upload” prompts in the notebook are normally skipped when you run from this repo).

---

## Notebooks

### 1) `stromatoporoid_reef_size_v16_final_main.ipynb` (PRIMARY; Ordovician–Devonian)
Main analysis notebook for **Ordovician–Devonian** (primary results). It runs the end-to-end workflow:

- builds Ord–Dev stage-level and 5-Myr-binned reef datasets from the PARED reef table
- loads PBDB-derived files (stromatoporoids + coral groups) and aligns them to stages / 5-Myr bins
- loads and interpolates environmental proxy series (temperature, oxygen, DO, sea level, δ¹³C)
- creates “master” merged datasets (stage-level and 5-Myr)
- applies CLR (compositional) transforms for selected proportional variables (including basal vs derived groupings)
- correlation analyses (Spearman and Pearson; stage-level and 5-Myr)
- additional robustness / statistical components implemented in the main notebook (e.g., bootstrap / permutation / partial correlations / detrending / variance partitioning / model selection / LOWESS / lag profiles / segmented or time-series-robust tests depending on the cell)

> **Outputs** are written to `./output/` as intermediate datasets and result tables.

### 2) `stromatoporoid_reef_size_Camb_Dev_Suppv16.ipynb` (SUPPLEMENT; Cambrian–Devonian)
Supplementary notebook that performs the **same core data integration** as the main notebook but expands the time window to **Cambrian–Devonian** and is intentionally limited to **simple correlations** (no advanced statistics beyond the correlation workflow).

---

## Repository contents (inputs)

### Core reef dataset
- `PARED_reef_All_numerical.csv`  
  Source table used to generate stage-level and 5-Myr reef summaries.

### Environmental proxy time series
- `temperature.csv`
- `oxygen.csv`
- `DO.csv`
- `sealevel.csv`
- `d13C_5Myr_Cam-Dev.csv`
- `d13C_stage_binned_Cam-Dev.csv`

> The notebooks are written to look for these filenames in the working directory.

### PBDB-derived input files (already included)
- `pbdb_data_Actinostromatida.csv`
- `pbdb_data_Amphiporida.csv`
- `pbdb_data_Clathrodictyida.csv`
- `pbdb_data_Labechiida.csv`
- `pbdb_data_Rugosa.csv`
- `pbdb_data_Stromatoporellida.csv`
- `pbdb_data_Stromatoporida.csv`
- `pbdb_data_Syringostromatida.csv`
- `pbdb_data_Tabulata.csv`

---

## How to run

### Recommended: Google Colab (zero setup)
1. Open the notebook directly from GitHub in Colab:
   - `stromatoporoid_reef_size_v16_final_main.ipynb` (main)
   - `stromatoporoid_reef_size_Camb_Dev_Suppv16.ipynb` (supplement)

2. Run cells **top-to-bottom**.

Because the required CSVs are already present in the repo, the “upload” cells should automatically print that the files already exist and proceed without prompting.

---

### Local run (Jupyter / VS Code)
**Note:** some cells import `google.colab` (for conditional upload/download). If you run locally, either:
- skip those Colab-only cells, or
- wrap/replace the Colab-only imports in your local copy.

#### 1) Create an environment and install dependencies
Typical dependencies used in the notebooks include:
- `pandas`, `numpy`, `matplotlib`
- `scipy`, `scikit-learn`
- `statsmodels`
- `requests` (and sometimes `geopandas/shapely` if API-based generation is triggered)

Example:
```bash
python -m venv .venv
source .venv/bin/activate   # (Windows: .venv\Scripts\activate)
pip install -U pip
pip install pandas numpy matplotlib scipy scikit-learn statsmodels requests
