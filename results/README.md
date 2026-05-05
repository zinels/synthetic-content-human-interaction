# Results

This folder stores result tables, model evaluation outputs, regression summaries, and generated figures.

## Model Performance

**Best model: Sentence Embeddings + Logistic Regression**

| Metric | Value |
|--------|-------|
| Accuracy | 0.8172 |
| F1 Score | 0.3288 |
| ROC-AUC | 0.8491 |

## Main Aggregate Finding

| Statistic | Value |
|-----------|-------|
| Correlation | −0.9009 |
| Regression coefficient on synthetic prevalence | −1.4913 |
| p-value | < 0.001 |
| R² | 0.863 |

## Subreddit-Level Summary

| Subreddit | Synthetic Prevalence | h2h_ratio |
|-----------|--------------------:|----------:|
| TodayILearned | 0.1204 | 0.9680 |
| Advice | 0.2722 | 0.8142 |
| AskDocs | 0.3241 | 0.6128 |
| AskScience | 0.4061 | 0.5216 |

## Recommended File Structure
results/
│
├── model_results.csv
├── subreddit_summary.csv
├── regression_summary.txt
├── synthetic_prevalence_vs_h2h_ratio.png
└── weekly_subreddit_trends.png

## Figures

- Scatter plot of `synthetic_prevalence` vs. `h2h_ratio` (colored by subreddit):
  <img width="889" height="590" alt="image" src="https://github.com/user-attachments/assets/c87e605a-514f-4639-b1c7-f8a85cdf6fad" />

- Bar chart of average synthetic prevalence by subreddit:
  <img width="790" height="490" alt="image" src="https://github.com/user-attachments/assets/2aa6e820-1e7f-40cc-9f8f-cac26cf7369e" />

- Bar chart of average h2h_ratio by subreddit:
  <img width="790" height="490" alt="image" src="https://github.com/user-attachments/assets/971659d7-ae43-4821-a1dc-c15a12a99847" />

- Weekly trend lines of synthetic prevalence by subreddit:
  <img width="1089" height="590" alt="image" src="https://github.com/user-attachments/assets/cacb2407-9967-424d-b5dd-d491d705ae72" />

- Weekly trend lines of h2h_ratio by subreddit:
  <img width="1089" height="590" alt="image" src="https://github.com/user-attachments/assets/dbbd85d8-255a-4a76-ab9d-0abf90a8d4c2" />


> **Reminder:** Results are observational. The project finds an association between synthetic-like prevalence and lower human-to-human interaction — it does not prove causation or verified AI authorship.
