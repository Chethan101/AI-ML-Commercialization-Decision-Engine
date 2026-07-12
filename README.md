# 🚀 AI/ML Commercialization Decision Engine

An end-to-end AI/ML prototype that helps an innovation team decide whether early-stage AI
product concepts should be **MVP Build**, **Customer Pilot**, **Reusable Asset**, **Incubate**,
or **Archive** — using Machine Learning to analyze customer demo and sandbox-usage signals, and
an AI narrative layer to turn predictions into recruiter/stakeholder-readable recommendations.

---

## 📖 Project Overview

Early-stage AI products rarely fail because the technology doesn't work — they fail because
teams invest in the wrong concepts for too long, guided by opinion rather than evidence. This
project builds a decision-support engine that replaces gut-feel prioritization with a
transparent, data-driven pipeline:

```
Customer signals → ML pattern detection & prediction → AI explanation & recommendation → Commercial decision
```

It's built entirely inside a single, fully-executable Jupyter notebook (`decision_engine.ipynb`)
so it's easy for a reviewer to read top-to-bottom, re-run, and audit every step. A condensed,
standalone version of the approach is also available in [`PROBLEM_APPROACH.md`](PROBLEM_APPROACH.md)
for a quick read before diving into the notebook.

---

## ✨ Features

- **Realistic mock dataset generator** — 460 product-concept records across 10 industries, with
  deliberately injected noise, missing values, outliers, and class imbalance.
- **Full data cleaning & preprocessing** — industry-aware imputation, winsorized outliers,
  encoding, and scaling, all explained in Markdown.
- **10+ EDA visualizations** — industry mix, feedback distribution, correlation heatmap, segment
  and risk breakdowns, each followed by a written insight.
- **7 engineered business features** — Engagement, Demand Intensity, Revenue Potential,
  Feasibility, Strategic Alignment, Repeatability, and Confidence Indicator scores, with exact
  formulas documented.
- **Business Assumptions section** — explicit reasoning for why synthetic data was used and how
  customer behavior was simulated.
- **Multi-model ML comparison** — Random Forest (primary), Decision Tree, Logistic Regression,
  and XGBoost (auto-detected), evaluated on accuracy, precision, recall, F1, confusion matrix,
  classification report, and ROC curves.
- **Commercialization Scoring Engine** — a 0–100 Readiness Score and a 0–100% Confidence Score
  for every concept, with a full portfolio ranking.
- **AI Insight Layer** — a rule-driven narrative generator producing Recommendation, Reason,
  Strengths, Weaknesses, Business Risk, Investment Advice, Expected Commercial Potential, and
  Next Action for every single concept.
- **SHAP explainability** — Summary Plot, Bar Plot, and Waterfall Plot (with plain-English
  explanations after each), auto-falling back to feature importance if SHAP isn't installed.
- **Feature Importance Deep-Dive** — Top 20 features, sorted, with a business-language write-up
  of why each family of features matters.
- **Executive Dashboard** — KPI cards (avg/highest readiness, avg confidence, outcome counts),
  a Top 10 ranked concept table, and six recruiter-facing charts in one view.
- **Recruiter Q&A** — ~15 likely interview questions about this project, answered directly.
- **Limitations & Future Scope** — an honest accounting of what this prototype doesn't do yet,
  and a concrete roadmap for what would come next.

---

## 🔁 Project Workflow

```
Customer Demo & Sandbox Data
        │
        ▼
Data Cleaning & Feature Engineering        (pandas, scikit-learn)
        │
        ▼
ML Classification                          (Random Forest / Decision Tree / Logistic Regression / XGBoost)
        │
        ▼
Commercialization Scoring Engine            (Readiness Score 0-100, Confidence Score 0-100%)
        │
        ▼
AI Insight Layer                            (rule-driven narrative generation)
        │
        ▼
Explainability                              (SHAP or feature-importance fallback)
        │
        ▼
Executive Dashboard + Recruiter Q&A + Executive Summary
```

---

## 🛠️ Technologies Used

| Category | Tools |
|---|---|
| Language | Python 3.11 |
| Data handling | pandas, NumPy |
| Visualization | matplotlib, seaborn |
| Machine Learning | scikit-learn (Random Forest, Decision Tree, Logistic Regression) |
| Optional ML | XGBoost (auto-detected, gracefully skipped if absent) |
| Explainability | SHAP (auto-detected, gracefully falls back to feature importance) |
| Notebook | Jupyter Notebook / JupyterLab |

---

## ⚙️ Installation

```bash
git clone <this-repo-url>
cd ai-ml-commercialization-decision-engine
python -m venv venv
source venv/bin/activate       # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

`xgboost` and `shap` are optional — the notebook automatically detects whether they're installed
and gracefully falls back (Logistic Regression/Decision Tree comparison, feature-importance-based
explainability) if they aren't, without breaking any cell.

---

## ▶️ Usage

```bash
jupyter notebook decision_engine.ipynb
```

Then run all cells top to bottom (`Kernel → Restart & Run All`). No manual edits are required —
the mock dataset is generated fresh on every run (seeded for reproducibility), and every
downstream section (cleaning, EDA, feature engineering, ML, scoring, AI narratives, SHAP,
dashboard) runs automatically in order.

---

## 📁 Folder Structure

```
.
├── decision_engine.ipynb              # main notebook — the full pipeline, fully executed
├── PROBLEM_APPROACH.md                # one-page problem approach (assumptions, data design, ML method, decision logic)
├── README.md                          # this file
├── requirements.txt                   # Python dependencies
├── data/
│   ├── commercialization_dataset_raw.csv       # generated mock data (with noise/missing/outliers)
│   ├── commercialization_dataset_clean.csv     # cleaned + encoded dataset
│   └── commercialization_decisions_ranked.csv  # final ranked concepts + AI narratives
└── screenshots/
    └── dashboard_placeholder.png      # add a screenshot of the notebook's Executive Dashboard here
```

---

## 📸 Screenshots

_Add a screenshot of the notebook's Executive Dashboard (Section 14B) here once you've run it
locally:_

```
screenshots/dashboard_placeholder.png
```

---

## 📊 Results

On the held-out test split, the winning model (selected by macro-averaged F1, to fairly weight
the rare `MVP Build` class alongside the common `Archive`/`Incubate` classes) comfortably
outperforms a majority-class baseline across accuracy, precision, recall, and F1. Full metrics,
the confusion matrix, classification report, and ROC curves are generated live in Section 9 of
the notebook — exact numbers vary slightly between runs since the dataset is regenerated with a
fixed random seed each time, but remain consistent within a narrow range.

Every raw signal is generated from per-concept latent business drivers (engagement/quality,
delivery risk, commercial appetite) instead of independent random draws, so the model is learning
from a dataset where feedback, usage, and commercial signals are genuinely — not superficially —
correlated. The **Commercialization Readiness Score** is a continuous blend of the model's full
probability distribution and five engineered business scores, with no fixed per-outcome bands or
hardcoded values, and Section 4B / Section 14F run explicit business-rule validation passes (e.g.
"strong engagement + budget + usage + low risk" can never be labeled `Archive`) at both
generation time and prediction time.

The final output is a fully ranked portfolio of ~400+ product concepts, each with:

- A **Commercialization Readiness Score (0–100)**
- A **Confidence Score (0–100%)**
- A **predicted commercial outcome**
- A **complete AI-generated narrative** (reason, strengths, weaknesses, risk, investment advice,
  expected potential, and next action)

exported to `data/commercialization_decisions_ranked.csv`.

---

## 💼 Business Value

This project replaces ad hoc, opinion-driven portfolio reviews with a **repeatable, evidence-backed
process**. Every concept — not just the ones a founder happens to champion loudly — gets the same
rigorous evaluation across customer engagement, demand, feasibility, and strategic fit. That gives
an innovation team:

- A **ranked shortlist** to bring into investment committee reviews.
- A **consistent, explainable rationale** for every recommendation (not a black-box score).
- A clear way to separate concepts worth funding now from ones worth incubating or archiving,
  backed by observed customer behavior rather than internal politics.

---

## 🚀 Future Scope

| Area | What it would add |
|---|---|
| 🔌 Live CRM Integration | Pull real demo/opportunity data directly from Salesforce, HubSpot, etc. |
| 💬 Real Customer Feedback | Ingest actual transcripts, tickets, and survey responses. |
| 🤖 LLM-Generated Explanations | Replace the rule-based narrative layer with an LLM for richer, adaptive language. |
| 🔁 Retraining Pipeline | Automate periodic retraining as new outcomes accumulate, with drift monitoring. |
| 🖥️ Streamlit Deployment | An interactive web app for non-technical stakeholders. |
| ☁️ Cloud Deployment | Containerized deployment with a scheduled batch-scoring job and API endpoint. |
| ♻️ Automated Model Retraining | Scheduled/drift-triggered retraining with versioned artifacts. |
| 📊 Business Analytics Dashboard | A persistent BI dashboard tracking portfolio health and prediction accuracy over time. |

See Section 14E of the notebook for the full write-up, and Section 14D for the corresponding
limitations each of these addresses.

---

## 🧑‍💻 Author

Internship candidate — AI/ML Commercialization Decision Engine (portfolio project).
