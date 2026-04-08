# Statistical Analysis — Quantifying Mobility Wellness Across Training Disciplines
 
## Overview
 
This repository contains the statistical analysis pipeline for the capstone thesis *Quantifying Mobility Wellness Across Training Disciplines* (Anna Shats, IE University, 2026). The analysis investigates the relationship between the Mobility Wellness Index (MWI) and health, lifestyle, and training background factors in a sample of 25 adults across four training discipline groups.
 
MWI is defined as:
 
```
MWI = (PROM - AROM) / PROM
```
 
where PROM is passive range of motion and AROM is active range of motion. A higher MWI indicates a larger gap between passive flexibility and active neuromuscular control, reflecting suboptimal musculoskeletal health.
 

## Project Structure

```
MWI_analysis/
├── data/
│   ├── raw/
│   │   ├── Health & Lifestyle Questionnaire (Responses).csv
│   │   ├── Hypermobility assessment (Responses).csv
│   │   └── MWI_raw.csv
│   └── processed/
│       ├── combined_data.csv        ← master dataset (25 × 19)
│       ├── hypermobility.csv        ← intermediate Beighton scores
│       └── MWI_clean.csv            ← per-pose MWI scores
├── notebooks/
│   ├── 01_data_cleaning.ipynb
│   ├── 02_hypermobility.ipynb
│   ├── 03_mwi_computation.ipynb
│   ├── 04_pose_analysis.ipynb
│   ├── 05_eda_basic.ipynb
│   ├── 06_eda_advanced.ipynb
│   └── 07_hypothesis_testing.ipynb
├
└── README.md
```

---

## Notebooks

Run in order — each notebook reads from `data/processed/` and the later ones depend on outputs from the earlier ones.

| # | Notebook | What it does |
|---|---|---|
| 01 | `01_data_cleaning.ipynb` | Loads the Health & Lifestyle survey, renames columns, computes BMI, derives composite variables (sleep quality, stress score, recovery scores), classifies training category, saves `combined_data.csv` |
| 02 | `02_hypermobility.ipynb` | Loads Beighton assessment, applies age-adjusted hypermobility thresholds (≥ 5/9 for adults 18–49), merges `hypermobility` column into `combined_data.csv` |
| 03 | `03_mwi_computation.ipynb` | Loads `MWI_raw.csv`, extracts mi4l scores per pose, computes composite MWI per participant, flags missing poses, merges MWI into `combined_data.csv` |
| 04 | `04_pose_analysis.ipynb` | Per-pose score distributions, bilateral symmetry analysis (Kneeling Knee Flexion & Standing Hip Abduction), Spearman correlations between individual poses and overall MWI |
| 05 | `05_eda_basic.ipynb` | Sample description, missing data audit, categorical and continuous variable distributions, outlier detection, full Spearman correlation matrix |
| 06 | `06_eda_advanced.ipynb` | MWI distribution and patterns by training category, PROM/AROM/ratio analysis, group comparison profiles (continuous + categorical variables), radar chart |
| 07 | `07_hypothesis_testing.ipynb` | Bivariate screening (Spearman ρ for continuous, Mann-Whitney U / Kruskal-Wallis for categorical), Beta regression (primary) and OLS (benchmark), bootstrap 95% CI for sitting_time, residual diagnostics |

---

## Dataset: `combined_data.csv`

25 participants × 19 variables.

| Variable | Type | Description |
|---|---|---|
| `name` | identifier | Participant name |
| `age_group` | ordinal | 18–29, 30–39, 40–49, 50–59 |
| `gender` | binary | Female / Male |
| `bmi` | continuous | Body mass index |
| `training_category` | nominal | Low Active / Strength-dominant / Flexibility-dominant / Hybrid |
| `early_life_training` | nominal | Dominant training background before age 18 |
| `end_range_control` | ordinal | Never / Sometimes / Often / Always |
| `weekly_volume` | ordinal | Training hours per week (4 levels) |
| `injury_presence` | binary | Current injury Yes / No |
| `chronic_pain` | ordinal | No pain / Mild / Moderate |
| `sleep_duration` | ordinal | Hours of sleep per night (3 levels) |
| `sleep_quality` | continuous | Composite score 0–10 |
| `physical_recovery` | continuous | Self-rated 1–6 |
| `mental_recovery` | continuous | Self-rated 1–6 |
| `stress_score` | continuous | Composite score 0–4 |
| `sitting_time` | discrete | Hours seated per day (5 / 7 / 9) |
| `sedentary_score` | continuous | Composite sedentary behaviour score |
| `hypermobility` | binary | Yes / No (Beighton, age-adjusted) |
| `mwi` | continuous | Mobility Within Integrity score ∈ (0, 1) |


---

## Requirements

```
pandas
numpy
matplotlib
seaborn
scipy
statsmodels
prince
```

Install with:

```bash
pip install pandas numpy matplotlib seaborn scipy statsmodels prince
```

Or if using the project conda environment:

```bash
conda activate <your-env>
jupyter notebook
```
