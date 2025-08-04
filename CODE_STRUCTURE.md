# Code Organization & Function Overview

**Author:** Yvan Bayingana

This document explains the layout and functions in the Python modules under `src/`.

---

## Module: `data_cleaning.py`

- `load_pisa(path: str) → pd.DataFrame`  
  Loads PISA 2022 public-use dataset (student + school records)

- `load_timss(path: str, grade: int) → pd.DataFrame`  
  Loads TIMSS 2023 Grade 4 or Grade 8 student & context data

- `harmonize_variables(pisa_df, timss_df) → pd.DataFrame`  
  Harmonises variable names and encodings across datasets

---

## Module: `analysis.py`

- `compute_means_gaps(df, subject: str) → pd.DataFrame`  
  Calculates average scores and subgroup gaps by country

- `run_multilevel_model(df, subject: str) → dict`  
  Fits random-intercept model (students within schools within countries)

- `profile_clusters(df_meta: pd.DataFrame) → dict`  
  Clusters countries by equity-performance profiles

---

## Module: `visualization.py`

- `plot_by_subgroup(df, subject, subgroup, output_path: str)`  
  Creates violin or boxplots by gender or SES groups

- `export_maps(df, subject, path: str)`  
  Generates geography-based performance maps for Power BI

- `prepare_powerbi_export(df, output_path: str)`  
  Writes CSV files and metadata for dashboard input

---

## Usage Example (Python snippet)

```python
from src.data_cleaning import load_pisa, load_timss, harmonize_variables
from src.analysis import compute_means_gaps, run_multilevel_model
from src.visualization import plot_by_subgroup

pisa = load_pisa("data/raw/pisa/")
timss = load_timss("data/raw/timss/", grade=8)
merged = harmonize_variables(pisa, timss)

gaps = compute_means_gaps(merged, subject="pv_creative")
models = run_multilevel_model(merged, subject="pv_math")
plot_by_subgroup(merged, subject="pv_science", subgroup="escs_quintile", output_path="figs/science_by_ses.png")
