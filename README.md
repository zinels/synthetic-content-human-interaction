
# Synthetic Content & Human Interaction in Online Communities

> Are subreddit-weeks with higher synthetic-like content prevalence associated with lower levels of human-to-human reply interaction?

A Social Media Mining project studying the relationship between synthetic-style writing and human interaction patterns across Reddit communities. This project **does not** attempt to detect AI-generated content estimating whether comments appear more *synthetic-like* or *human-like* based on linguistic patterns, then examines how aggregated synthetic prevalence correlates with community interaction at the subreddit-week level.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Repository Structure](#repository-structure)
- [Dataset](#dataset)
- [Methodology](#methodology)
- [Results](#results)
- [Getting Started](#getting-started)
- [Ethical Considerations](#ethical-considerations)
- [Limitations](#limitations)
- [Author](#author)

---

## Project Overview

This project investigates whether higher levels of synthetic-like writing in a subreddit during a given week are associated with reduced human-to-human reply interaction. Analysis is performed at the **subreddit-week level**: comment-level synthetic-likeness scores are aggregated weekly and compared against a human-to-human interaction metric (`h2h_ratio`).

**Important framing:** A comment labeled *synthetic-like* is not a verified AI-generated post. The classifier estimates the *appearance* of synthetic-style writing based on features like polish, generic structure, formulaic phrasing, and lack of contextual specificity. All findings describe associations, not causation.

**Subreddits studied:**
- r/AskScience
- r/AskDocs
- r/Advice
- r/TodayILearned

**Collection window:** October 6, 2025 – December 28, 2025 (12 weeks)

---

## Repository Structure

```
synthetic-content-human-interaction/
│
├── README.md
├── requirements.txt
├── .gitignore
├── LICENSE
│
├── notebooks/
│   ├── README.md
│   ├── 01_collect_askscience.ipynb
│   ├── 02_collect_todayilearned.ipynb
│   ├── 03_collect_askdocs.ipynb
│   ├── 04_collect_advice.ipynb
│   └── 05_modeling_and_analysis.ipynb
│
├── docs/
│   ├── project_overview.md
│   ├── methodology.md
│   ├── annotation_guidelines.md
│   ├── data_dictionary.md
│   ├── ethical_considerations.md
│   ├── results_summary.md
│   ├── limitations.md
│   └── team_contributions.md
│
├── data/           # Raw/cleaned CSVs (not included — see Data Availability)
├── results/        # Output figures and tables
├── models/         # Saved model artifacts
└── assets/         # Supporting assets
```

---

## Dataset

The final cleaned corpus contains **7,606 Reddit comments** across four subreddits:

| Subreddit | Clean Comments |
|-----------|---------------|
| Advice | 2,498 |
| AskDocs | 1,572 |
| AskScience | 2,541 |
| TodayILearned | 995 |
| **Total** | **7,606** |

The final analysis dataset contains **48 subreddit-week observations** (4 subreddits × 12 weeks).

---

## Methodology

### Two-Level Design

**Comment level** — Reddit comments are cleaned, sampled, manually labeled, and used to train a synthetic-likeness classifier.

**Subreddit-week level** — Classifier scores are aggregated weekly. Weekly synthetic prevalence values are then regressed against the `h2h_ratio` (human-to-human interaction metric).

### Regression Model

```
h2h_ratio ~ synthetic_prevalence + C(subreddit)
```

### Models Compared

| Model | Embedding |
|-------|-----------|
| Logistic Regression | TF-IDF |
| XGBoost | TF-IDF |
| Logistic Regression ✅ | Sentence Embeddings |
| XGBoost | Sentence Embeddings |

Grouped train/test splitting is performed by `post_id` to prevent data leakage across comments from the same submission.

**Best model: Sentence Embeddings + Logistic Regression**

| Metric | Value |
|--------|-------|
| Accuracy | 0.8172 |
| F1 Score | 0.3288 |
| ROC-AUC | 0.8491 |

> The low F1 reflects that the positive (synthetic-like) class is difficult to identify at the individual-comment level. For this reason, the project focuses on **aggregated subreddit-week patterns** rather than individual comment predictions.

---

## Results

The aggregated analysis reveals a strong negative association between weekly synthetic prevalence and human-to-human interaction:

| Statistic | Value |
|-----------|-------|
| Correlation | −0.9009 |
| Regression coefficient | −1.4913 |
| p-value | < 0.001 |
| R² | 0.863 |

### Subreddit-Level Averages

| Subreddit | Synthetic Prevalence | h2h_ratio |
|-----------|---------------------|-----------|
| TodayILearned | 0.1204 | 0.9680 |
| Advice | 0.2722 | 0.8142 |
| AskDocs | 0.3241 | 0.6128 |
| AskScience | 0.4061 | 0.5216 |

Subreddit-weeks with more synthetic-like writing also tend to show weaker human-to-human reply interaction. **This finding describes an association, not a causal relationship.**

---

## Getting Started

### Installation

```bash
pip install -r requirements.txt
```

### Dependencies

```
pandas · numpy · scikit-learn · sentence-transformers · xgboost
matplotlib · seaborn · statsmodels · tqdm · requests · beautifulsoup4
jupyter · notebook · ipykernel
```

### Workflow

Run the notebooks in order:

| Notebook | Description |
|----------|-------------|
| `01_collect_askscience.ipynb` | Collect and clean AskScience comments |
| `02_collect_todayilearned.ipynb` | Collect and clean TodayILearned comments |
| `03_collect_askdocs.ipynb` | Collect and clean AskDocs comments |
| `04_collect_advice.ipynb` | Collect and clean Advice comments |
| `05_modeling_and_analysis.ipynb` | Train models, score comments, compute metrics, run regression |

### Data Availability

Raw Reddit data is **not included** in this repository. Communities like r/AskDocs and r/Advice contain sensitive user-generated content that warrants careful handling. The full pipeline, cleaning logic, annotation approach, and aggregate results are documented here. If working locally, place CSV files in `data/` per the structure in `data/README.md`.

---

## Ethical Considerations

This project works with public Reddit comments but treats user-generated content carefully:

- Raw usernames and sensitive personal details are not exposed
- No medical details from r/AskDocs are reproduced
- Analysis is conducted at an aggregate level
- The classifier is framed as a *synthetic-likeness estimator*, not an AI-authorship detector

See [`docs/ethical_considerations.md`](docs/ethical_considerations.md) for the full discussion.

---

## Limitations

- The classifier estimates synthetic-*likeness*, not verified AI authorship
- Manual labels are based on writing style and can be subjective
- The positive class is difficult to classify at the individual-comment level
- Reddit communities differ in moderation norms, conversation structure, and user behavior
- The study is observational — no causal claims can be made
- A 0.5 threshold is used operationally for downstream scoring, but is not a ground-truth boundary

See [`docs/limitations.md`](docs/limitations.md) for more detail.

---

## Authors

**Nafis Anwar**, **Tanzeel Rahman**, **Cem Tutar**, **Paul Bautista-Solis**  


University of South Florida  
Social Media Mining Project
```
