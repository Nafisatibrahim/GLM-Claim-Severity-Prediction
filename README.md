# What Makes a Claim Expensive?

**Claim severity modeling with GLMs and gradient boosting**

> **Project question:** What makes a claim expensive, and can we predict its cost at the time the policy is written?

The main goal is to identify the drivers of claim cost and to test how predictable severity is from underwriting information alone. Comparing a mean baseline, a Gamma GLM and a gradient-boosted model (LightGBM) is how we test it: if added model complexity cannot beat the baseline, the cost is mostly not predictable from these features. The project also covers calibration, explainability, and a drift monitoring plan. Built on French motor insurance data (freMTPL2).

## Context

Insurers price policies on the **pure premium**: expected claim frequency × expected claim severity. This project focuses on **severity**: *given that a claim happens, how much will it cost?*

**Constraint: only information known when the policy is written.** The model uses underwriting features only (driver age, vehicle, bonus-malus, region, density). It has no claim-level details such as injury type, damage extent or accident circumstances, which are what actually drive the cost of an individual claim.
Severity data is positive, right-skewed, and heavy-tailed. **Gamma GLMs with a log link** are widely used in insurance pricing for this kind of target, because they handle skewed positive amounts and produce explainable multiplicative relativities. LightGBM (Gamma objective) serves as a flexible challenger to check whether non-linearities and interactions add signal the GLM misses.

**Outputs:**
- **Cost drivers:** GLM relativities and SHAP values answer *what makes a claim expensive*.
- **Predictability:** technical metrics (Gamma deviance, MAE, Gini) and business metrics (portfolio balance, decile lift) answer *can we predict it*.

## Data

**freMTPL2** (French Motor Third-Party Liability): ~678k policies and ~26.6k claims, available on OpenML:

| Table | OpenML id (to verify on load) | Content |
|---|---|---|
| `freMTPL2freq` | 41214 | One row per policy: exposure, claim count, driver/vehicle/region features |
| `freMTPL2sev` | 41215 | One row per claim: policy id, claim amount |

Raw data lives in `data/raw/` and is not committed.

## Plan & checklist

Detailed plan, metric definitions, and decision log: **[plan.md](plan.md)**

- [ ] 1. Problem formulation
- [ ] 2. Success metrics (technical + business)
- [ ] 3. Data acquisition & join
- [ ] 4. Data profiling & quality checks
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
