# Problem Approach — AI/ML Commercialization Decision Engine

A one-page summary of the approach behind this project, for reviewers who want the gist before
opening the full notebook. (This same content also appears as Section 3B inside
`decision_engine.ipynb`.)

## Problem

An innovation team has many early-stage AI product concepts, each observed through customer
demos, discovery sessions, and sandbox trials. The team needs a repeatable, evidence-based way
to decide, for every concept, whether to pursue **MVP Build**, **Customer Pilot**, **Reusable
Asset**, **Incubate**, or **Archive** — instead of relying on opinion or whoever pitches loudest.

## Assumptions

- Each row/record represents **one product concept**, with demo, sandbox-usage, and commercial
  signals aggregated to the concept level (rather than modeling every individual customer
  touchpoint separately).
- **Industries behave differently** — e.g. Healthcare shows more risk aversion and longer sales
  cycles, Consumer Apps shows higher and noisier engagement. This is modeled with explicit
  per-industry bias parameters rather than uniform randomness.
- The target label (`commercial_outcome`) is derived from a **latent, noisy composite score**
  built from the underlying signals, not hand-labeled directly — this keeps the classification
  problem genuinely learnable but not trivially deterministic, closer to how a real investment
  committee decision only partially correlates with any single observed signal.
- **Real company data was unavailable** for this internship prototype, so the dataset is
  synthetic and clearly documented as such throughout the notebook (see Section 7B).

## Data Design

- **460 mock records** (within the requested 300–500 range) spanning **10 industries**.
- Combines four signal families into one flat table per concept: product-concept attributes,
  customer demo signals, sandbox usage behavior, and commercial signals, plus short synthetic
  text-feedback fields.
- Deliberately **imperfect by design**: ~4–8% missing values in key columns, a handful of
  injected outliers, duplicate rows (simulating a CRM double-export), and a deliberately
  **imbalanced target** (few `MVP Build` breakouts, many `Archive`/`Incubate` concepts) — mirrors
  a realistic innovation funnel rather than a synthetic-perfect dataset.

## Selected ML Method

- **Primary model: Random Forest Classifier** (multi-class, `class_weight="balanced"`),
  benchmarked against Decision Tree, Logistic Regression, and XGBoost (auto-detected, skipped
  gracefully if not installed).
- Selected by **macro-averaged F1** (not raw accuracy) so the rare, high-value `MVP Build` class
  is weighted equally with the common `Archive`/`Incubate` classes during model selection.
- Chosen because it: handles non-linear feature interactions, is robust to the injected noise and
  outliers, needs no feature scaling, supports class balancing directly, and yields built-in
  feature importances for explainability.
- A complementary **unsupervised clustering pass** (KMeans on the engineered feature space,
  visualized via PCA) cross-checks that concepts naturally group in ways consistent with the
  supervised model's predictions — see Section 8B of the notebook.

## Decision Logic

```
Raw signals (feedback, usage, urgency, risk, comments)
        │  engineered into (Section 7)
        ▼
Composite scores (engagement, demand intensity, revenue potential, feasibility,
                   strategic alignment, repeatability, confidence)
        │  fed into (Section 8)
        ▼
Random Forest → predicted commercial_outcome + class probability
        │  blended into (Section 10)
        ▼
Commercialization Readiness Score (0-100)  +  Confidence Score (0-100%)
        │  ranks the portfolio, then translated by (Section 11)
        ▼
AI narrative layer → Recommendation, Reason, Strengths, Weaknesses, Business Risk,
                      Investment Advice, Expected Potential, Next Action
```

The **Readiness Score** blends the model's predicted-outcome anchor (35% weight) with five
engineered business scores (engagement, demand intensity, revenue potential, feasibility,
strategic alignment), so it reflects both what the model predicts and the underlying evidence —
not the raw model output alone. Critically, the anchor is the model's **full probability
distribution** over all five classes (not just a lookup of the predicted label), and the final
score is never clipped into a fixed per-outcome band — two concepts predicted as the same class
can and do land at different readiness scores, and scores naturally overlap at class boundaries,
exactly as a real investment-committee score would. The **Confidence Score** is the model's own
predicted-class probability, expressed as a percentage — a measure of the classifier's
certainty, not of business success probability.

Every raw signal in the dataset is generated from three per-concept latent business drivers
(engagement/quality, delivery risk, commercial appetite) rather than independently, so a
concept's story is internally consistent end to end: strong feedback flows through to higher
repeat usage, more active users, higher willingness to pay, fewer objections, and lower
implementation risk — and the reverse for a weak concept. A dedicated business-rule validation
pass (Section 4B, generation time) and a final validation report (Section 14F, prediction time)
check that no impossible combination — e.g. strong engagement/budget/usage/low-risk labeled
`Archive`, or a `readiness_proxy` below 35 labeled `MVP Build` — makes it into the dataset or the
final portfolio.

## Output

A fully ranked portfolio of concepts (`data/commercialization_decisions_ranked.csv`), each with a
Readiness Score, Confidence Score, predicted outcome, and a complete AI-generated narrative
explaining why — ready for an investment committee to review directly.
