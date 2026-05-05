# Methodology

## Overview

This project uses a dual-level observational design.

At the **micro level**, individual Reddit comments are cleaned, labeled, represented as text features, and classified using supervised machine learning.

At the **macro level**, comment-level classifier scores are aggregated into subreddit-week measures, which are then used to study whether synthetic-like content prevalence is associated with human-to-human interaction.

## Subreddit Selection

| Subreddit | Character |
|-----------|-----------|
| r/AskScience | Informational and expert-oriented |
| r/AskDocs | Question-answer based; often contains sensitive health discussion |
| r/Advice | Interpersonal and conversational |
| r/TodayILearned | General-interest and fact-sharing |

This variation allows the project to compare communities with meaningfully different communication norms.

## Collection Window

October 6, 2025 – December 28, 2025 (12 weeks)

A fixed time window makes subreddit-week units more comparable. Data is organized by week and subreddit rather than allowing high-volume bursts to dominate the analysis.

## Data Collection

Data was collected using custom Python notebooks — one per subreddit. Each notebook collects Reddit posts and comments, preserves parent-child relationships, and exports structured CSV bundles. A **week-balanced strategy** is used to collect approximately comparable numbers of clean comments per subreddit-week.

## Cleaning Pipeline

The preprocessing pipeline removes content that does not represent normal organic user interaction:

- Blank, deleted, and removed comments
- Moderator, system-generated, and AutoModerator-style content
- Repeated templates and boilerplate
- Meta threads that distort ordinary conversation
- Broken reply-chain links where the parent comment did not survive cleaning

Parent-child reply relationships are reconstructed, identifying both direct post replies and comment-to-comment replies.

## Annotation Design

A subset of comments is manually labeled using three labels:

| Label | Meaning |
|-------|---------|
| `0` | Human-like |
| `1` | Synthetic-like |
| `-1` | Unsure |

Labels describe **apparent writing style only** — not verified authorship.

Two sampling strategies are used:

- **Balanced sample** — creates a training set with sufficient examples of both classes
- **Overlap sample** — compares labels across annotators to refine the rubric and identify unclear cases

## Feature Construction

| Method | Description |
|--------|-------------|
| **TF-IDF** | Sparse word/phrase features; useful for detecting repeated terms and vocabulary differences |
| **Sentence Embeddings** | Dense vectors capturing semantic and stylistic similarity; uses `all-MiniLM-L6-v2` |

## Model Comparison

| # | Representation | Classifier |
|---|---------------|------------|
| 1 | TF-IDF | Logistic Regression |
| 2 | TF-IDF | XGBoost |
| 3 ✅ | Sentence Embeddings | Logistic Regression |
| 4 | Sentence Embeddings | XGBoost |

**Best model: Sentence Embeddings + Logistic Regression**

## Train/Test Split

Splitting is grouped by `post_id`. Comments under the same Reddit post share topic, context, and vocabulary — allowing them across both sets would produce overly optimistic evaluation results. Grouped splitting reduces this leakage risk.

## Evaluation Metrics

| Metric | Purpose |
|--------|---------|
| Accuracy | Overall share of correct predictions |
| F1 Score | Accounts for class imbalance on the harder synthetic-like class |
| ROC-AUC | Separability across classification thresholds |

## Full-Corpus Scoring

After selecting the best model, it is retrained on all usable labeled comments and used to assign a `synthetic_score` to every comment in the cleaned corpus. A higher score indicates more synthetic-like writing.

## Aggregation to Subreddit-Week Level

### Synthetic Prevalence

synthetic_prevalence = mean(synthetic_score) per subreddit-week

### Human-to-Human Interaction Ratio

Comments are binarized at a threshold of 0.5:

- `synthetic_score < 0.5` → human-like
- `synthetic_score ≥ 0.5` → synthetic-like

Then:
h2h_ratio = human-human reply interactions / all usable reply interactions

This metric acts as a proxy for person-to-person conversational interaction.

## Final Regression Model
h2h_ratio ~ synthetic_prevalence + C(subreddit)

Controls for subreddit-level differences while testing the association between synthetic prevalence and human-to-human interaction.

## Interpretation

Results are interpreted at the **aggregate level only**. The project does not claim:

- that any individual comment was definitely AI-generated
- that the classifier perfectly identifies AI authorship
- that synthetic-like content *causes* lower interaction

The project claims only that higher synthetic-like prevalence is **associated with** lower human-to-human interaction in the observed subreddit-week data.
