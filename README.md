<p align="center">
  <img src="assets/banner.svg" alt="What Makes a Claim Expensive? Claim severity modeling with Gamma GLMs and gradient boosting on French motor insurance data (freMTPL2)" width="100%">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/status-in%20progress-d29922" alt="Status: in progress">
  <img src="https://img.shields.io/badge/started-Nov%206%2C%202026-0969da" alt="Started November 6, 2026">
  <img src="https://img.shields.io/badge/python-3.12-3776AB?logo=python&logoColor=white" alt="Python 3.12">
  <img src="https://img.shields.io/badge/models-Gamma%20GLM%20%C2%B7%20LightGBM-6e7781" alt="Models: Gamma GLM and LightGBM">
  <img src="https://img.shields.io/badge/license-MIT-6e7781" alt="License: MIT">
</p>

<p align="center"><b>Timeline:</b> November 6, 2026 to present · <b>By</b> <a href="https://nafisatibrahim.com/">Nafisat Ibrahim</a></p>

> **What makes a claim expensive, and can we predict its cost at the time the policy is written?**

## Problem

Insurers price on **frequency × severity**. This project models severity: *once a claim happens, what will it cost?*

- **Target:** average cost per claim, per policy (weighted by number of claims)
- **Features:** underwriting info only (driver age, vehicle, bonus-malus, region, density). No injury or damage details.
- **Approach:** mean baseline → Gamma GLM → LightGBM. If complexity can't beat the baseline, severity isn't predictable from these features.
- **Why a Gamma GLM:** claim costs are positive and heavily skewed; Gamma GLMs handle that and give explainable relativities, which is why they're widely used in pricing.

## Success metrics

| Question | Metric | What "good" looks like |
|---|---|---|
| Is it accurate? | Gamma deviance *(primary)*, MAE | Lower than the baseline |
| Does it rank risks? | Gini | Above 0 (baseline scores 0) |
| Is the book priced right? | Balance ratio (predicted ÷ actual cost) | ≈ 1.00 |
| Does it separate cheap from expensive? | Decile lift | Top decile clearly above bottom |
| What drives cost? | GLM relativities, SHAP values | Consistent, explainable drivers |

## Data

**freMTPL2** (French Motor Third-Party Liability): ~678k policies and ~26.6k claims, available on OpenML:

| Table | OpenML id | Rows × columns | Content |
|---|---|---|---|
| `freMTPL2freq` | 41214 | 678,013 × 12 | One row per policy: exposure, claim count, driver/vehicle/region features |
| `freMTPL2sev` | 41215 | 26,639 × 2 | One row per claim: policy id, claim amount |

Raw data lives in `data/raw/` and is not committed.

## Plan & checklist

<p align="center">
  <img src="assets/roadmap.svg" alt="Project roadmap: Frame (done), Data (in progress), Model (to do), Learn (to do)" width="100%">
</p>

Detailed plan, metric definitions, and decision log: **[plan.md](plan.md)**

- [x] 1. Problem formulation
- [x] 2. Success metrics (technical + business)
- [ ] 3. Data acquisition & join *(acquisition done; join next)*
- [ ] 4. Data profiling & quality checks *(in progress)*
- [ ] 5. Exploratory data analysis
- [ ] 6. Train/test split
- [ ] 7. Preprocessing & feature engineering
- [ ] 8. Modelling: baseline, Gamma GLM, LightGBM
- [ ] 9. Evaluation: how predictable is severity?
- [ ] 10. Driver analysis: GLM relativities, SHAP values
- [ ] 11. Conclusion: what makes a claim expensive, and is it predictable at underwriting?
- [ ] 12. Stretch: frequency model, Tweedie, drift monitoring plan

## Project structure

```
├── assets/             # README images (banner, roadmap, icons)
├── data/
│   ├── raw/            # original downloads (git-ignored)
│   └── processed/      # cleaned / modelling tables (git-ignored)
├── notebooks/          # exploration and narrative, numbered (01_eda.ipynb, ...)
├── src/                # reusable code: data loading, features, metrics, models
├── tests/              # unit tests for src/
├── models/             # saved model artefacts (git-ignored)
├── reports/figures/    # exported plots
├── plan.md             # plan, metrics, decision log
└── requirements.txt
```

## Setup

```bash
python -m venv .venv
.venv\Scripts\activate          # Windows  (source .venv/bin/activate on macOS/Linux)
pip install -r requirements.txt
```

## Results

_To be filled in._

### Predictability

| Model | Gamma deviance | MAE | Gini | Balance ratio |
|---|---|---|---|---|
| Baseline (mean) | | | | |
| Gamma GLM | | | | |
| LightGBM | | | | |

### Cost drivers

| Driver | GLM relativity | SHAP rank | Takeaway |
|---|---|---|---|
| | | | |

### Answer to the project question

_What makes a claim expensive, and how much of it is predictable at underwriting?_

## Author

**Nafisat Ibrahim**

<p>
  <a href="https://github.com/Nafisatibrahim" title="GitHub"><img src="assets/icons/github.svg" alt="GitHub" width="28" height="28"></a>
  &nbsp;&nbsp;
  <a href="https://www.linkedin.com/in/nafisatibrahim/" title="LinkedIn"><img src="assets/icons/linkedin.svg" alt="LinkedIn" width="28" height="28"></a>
  &nbsp;&nbsp;
  <a href="https://nafisatibrahim.com/" title="Website"><img src="assets/icons/website.svg" alt="Website" width="28" height="28"></a>
</p>
