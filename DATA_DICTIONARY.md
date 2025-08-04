# Data Dictionary & Cleaning Overview

This documents the **processed student-level merged file** combining PISA 2022 and TIMSS 2023 records.

---

## Raw Data Sources

- `data/raw/pisa/`: PISA 2022 public-use SPSS/SAS files  
- `data/raw/timss/`: TIMSS 2023 international database (Grades 4 & 8 SPSS/SAS) :contentReference[oaicite:15]{index=15}

---

## Processed Files

| Filename             | Description                                           |
|----------------------|-------------------------------------------------------|
| `merged_clean.csv`   | Merged dataset (PISA & TIMSS) with harmonised variables |
| `clean_pisa.csv`     | PISA records with plausible-value averages            |
| `clean_timss_g8.csv` | TIMSS Grade 8 data with home, teacher, and school context |
| `logs/`              | Cleaning and harmonisation logs                       |

---

## Key Variables (in `merged_clean.csv`)

| Column            | Type       | Description                                                      |
|-------------------|------------|------------------------------------------------------------------|
| proc_id           | String     | Unique ID combining survey and case identifier                   |
| country_code      | String     | ISO‑coded country or economy                                      |
| gender            | Categorical| 1=Male, 2=Female                                                  |
| escs_quintile     | Integer    | SES quintile within a country                                     |
| pv_math           | Float      | Plausible-value mean in math                                     |
| pv_science        | Float      | Plausible-value mean in science                                  |
| pv_read           | Float      | Plausible-value mean in reading (PISA only)                      |
| pv_creative       | Float      | Creative thinking plausible-value (PISA only) :contentReference[oaicite:16]{index=16} |
| home_resources    | Categorical| Home educational resource index (derived from TIMSS context)      |
| teacher_degree    | Binary     | 1=Teacher has bachelor’s degree or higher (TIMSS school file)     |

---

## Cleaning & Harmonisation Procedures

1. Imported raw files into CSV, ensuring metadata is preserved  
2. Computed consistent SES/home-resources quintiles across systems  
3. Properly averaged plausible values following OECD/IEA guidance  
4. Applied sampling weights and stratification variables in all analyses  
5. Imputed missing data (numeric = median; categorical = "unknown")  
6. Removed subnational benchmarking regions as needed to maintain comparability (e.g. Quebec, Hong Kong)

---

## Provenance & Versions

- **PISA 2022 public-use files downloaded on:** YYYY‑MM‑DD (fill this)  
- **TIMSS 2023 files downloaded on:** YYYY‑MM‑DD  
- Processing conducted using Python 3.9, logs available in `data/processed/logs/`
