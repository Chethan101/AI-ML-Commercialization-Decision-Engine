# 🚀 AI/ML Commercialization Decision Engine

An end-to-end AI/ML prototype that helps innovation teams evaluate early-stage AI product concepts and recommend whether they should proceed as **MVP Build**, **Customer Pilot**, **Reusable Asset**, **Incubate**, or **Archive**.

The system combines synthetic customer interaction data, machine learning, explainable AI, and business scoring to transform customer signals into evidence-based commercialization decisions.

---

# 📖 Project Overview

Organizations often struggle to decide which AI product ideas deserve further investment. Decisions are frequently based on intuition rather than measurable customer evidence.

This project addresses that challenge by building an AI-powered commercialization decision engine that analyzes customer demo feedback, sandbox usage, and commercial indicators to generate objective investment recommendations.

The complete workflow is implemented inside a single executable Jupyter Notebook (`decision_engine.ipynb`) so reviewers can reproduce every stage of the pipeline from data generation to final recommendations.

A summarized version of the methodology is also available in **PROBLEM_APPROACH.md**.

---

# ✨ Features

- Synthetic dataset generator producing **460 AI product concepts** across **10 industries**
- Realistic customer interaction, sandbox usage, and commercial business signals
- Injected missing values, duplicate records, outliers, and class imbalance to simulate real enterprise datasets
- Complete data cleaning and preprocessing pipeline
- Exploratory Data Analysis (EDA) with multiple business visualizations
- Feature engineering using business-oriented composite scores
- Benchmark comparison of:
  - Logistic Regression
  - Random Forest
  - Decision Tree
  - XGBoost (optional)
- Automatic model selection based on **Macro-averaged F1 Score**
- Commercialization Readiness Score (0–100)
- Prediction Confidence Score (0–100%)
- AI-generated business explanations and investment recommendations
- SHAP Explainability (with automatic fallback to feature importance)
- Executive dashboard with KPIs, rankings, and business insights
- Recruiter Q&A and project documentation

---

# 🔁 Project Workflow

```text
Synthetic Customer Data
        │
        ▼
Data Cleaning & Preprocessing
        │
        ▼
Exploratory Data Analysis (EDA)
        │
        ▼
Feature Engineering
        │
        ▼
Model Benchmarking
(Logistic Regression, Random Forest,
Decision Tree, XGBoost)
        │
        ▼
Best Model Selection
(Macro F1 Score)
        │
        ▼
Commercialization Prediction
        │
        ▼
Readiness Score + Confidence Score
        │
        ▼
AI Business Recommendation Engine
        │
        ▼
Executive Dashboard & Ranked Portfolio
```

---

# 🤖 Machine Learning Approach

Four machine learning algorithms are benchmarked:

- Logistic Regression
- Random Forest
- Decision Tree
- XGBoost (if installed)

The final model is selected automatically using **Macro-averaged F1 Score**, ensuring balanced performance across all commercialization classes rather than favoring majority classes.

For the current implementation, **Logistic Regression** achieved the highest Macro F1 score and was therefore selected as the production model.

---

# 📊 Dataset

The project generates a synthetic commercialization dataset every time the notebook is executed.

Dataset characteristics:

- 460 Product Concepts
- 10 Industries
- Customer Demo Signals
- Sandbox Usage Metrics
- Commercial Signals
- Short Customer Feedback
- Missing Values
- Duplicate Records
- Outliers
- Imbalanced Commercialization Outcomes

Three datasets are exported during execution:

| File | Description |
|------|-------------|
| commercialization_dataset_raw.csv | Raw generated dataset before preprocessing |
| commercialization_dataset_clean.csv | Cleaned and feature-engineered dataset |
| commercialization_decisions_ranked.csv | Final commercialization recommendations |

---

# 🛠 Technologies Used

| Category | Technology |
|------------|----------------|
| Language | Python 3 |
| Data Processing | Pandas, NumPy |
| Visualization | Matplotlib, Seaborn |
| Machine Learning | Scikit-learn |
| Explainability | SHAP |
| Notebook | Jupyter Notebook |

---

# ⚙ Installation

```bash
git clone https://github.com/Chethan101/AI-ML-Commercialization-Decision-Engine.git

cd AI-ML-Commercialization-Decision-Engine

pip install -r requirements.txt
```

Optional libraries:

- xgboost
- shap

The notebook automatically detects whether these libraries are installed and falls back gracefully if unavailable.

---

# ▶ Usage

Launch Jupyter Notebook:

```bash
jupyter notebook decision_engine.ipynb
```

Run every cell from top to bottom.

The notebook automatically:

- Generates the synthetic dataset
- Cleans the data
- Performs EDA
- Engineers business features
- Benchmarks multiple ML models
- Selects the best-performing model
- Predicts commercialization outcomes
- Generates business recommendations
- Exports the final ranked portfolio

---

# 📁 Project Structure

```
.
├── decision_engine.ipynb
├── README.md
├── PROBLEM_APPROACH.md
├── requirements.txt
├── data
│   ├── commercialization_dataset_raw.csv
│   ├── commercialization_dataset_clean.csv
│   └── commercialization_decisions_ranked.csv
└── screenshots
```

---

# 📈 Results

The notebook benchmarks multiple machine learning algorithms using:

- Accuracy
- Precision
- Recall
- Macro F1 Score
- Confusion Matrix
- Classification Report
- ROC Curves

The model with the highest **Macro F1 Score** is automatically selected.

For the current dataset, **Logistic Regression** achieved the best Macro F1 score and is therefore used to generate commercialization predictions.

Each product concept receives:

- Commercialization Readiness Score (0–100)
- Confidence Score (0–100%)
- Predicted Commercialization Outcome
- Investment Priority
- AI-generated Business Explanation
- Strengths
- Weaknesses
- Business Risk
- Recommended Next Action

The final ranked portfolio is exported as:

```
data/commercialization_decisions_ranked.csv
```

---

# 💼 Business Value

This project demonstrates how machine learning can support innovation portfolio management by replacing subjective decision-making with evidence-driven recommendations.

Business benefits include:

- Objective product prioritization
- Explainable AI recommendations
- Investment decision support
- Commercialization readiness assessment
- Transparent ranking of AI product concepts
- Faster portfolio evaluation

---

# 🚀 Future Scope

- Live CRM integration (Salesforce, HubSpot)
- Real customer feedback ingestion
- LLM-generated business narratives
- Automated model retraining
- Streamlit web application
- Cloud deployment
- REST API for predictions
- Real-time commercialization dashboard

---

# 👨‍💻 Author

**Chethan V**

AI/ML Commercialization Decision Engine

Internship Portfolio Project
