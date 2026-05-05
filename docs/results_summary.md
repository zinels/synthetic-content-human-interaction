# Results Summary

## Cleaned Corpus

| Subreddit | Clean Comments |
|-----------|---------------:|
| Advice | 2,498 |
| AskDocs | 1,572 |
| AskScience | 2,541 |
| TodayILearned | 995 |
| **Total** | **7,606** |

Final analysis dataset: **48 subreddit-week observations** (4 subreddits × 12 weeks)

## Best Model

**Sentence Embeddings + Logistic Regression** outperformed all TF-IDF baselines on the positive synthetic-like class.

| Metric | Value |
|--------|-------|
| Accuracy | 0.8172 |
| F1 Score | 0.3288 |
| ROC-AUC | 0.8491 |

The accuracy and ROC-AUC indicate that the classifier captures useful signal. The modest F1 score reflects that identifying synthetic-like comments at the individual-comment level remains difficult. For this reason, the project focuses on **aggregate subreddit-week patterns** rather than individual-level predictions.

## Subreddit-Level Averages

| Subreddit | Synthetic Prevalence | h2h_ratio |
|-----------|--------------------:|----------:|
| TodayILearned | 0.1204 | 0.9680 |
| Advice | 0.2722 | 0.8142 |
| AskDocs | 0.3241 | 0.6128 |
| AskScience | 0.4061 | 0.5216 |

## Main Association Result

Across 48 subreddit-week observations, synthetic prevalence is strongly negatively associated with human-to-human interaction:

| Statistic | Value |
|-----------|-------|
| Correlation | −0.9009 |
| Regression coefficient on synthetic prevalence | −1.4913 |
| p-value | < 0.001 |
| R² | 0.863 |

## Plain-Language Interpretation

Subreddit-weeks with more synthetic-like writing tend to have lower human-to-human reply interaction. TodayILearned sits at one end of the gradient — lowest synthetic prevalence, highest h2h_ratio — while AskScience sits at the other. Advice and AskDocs fall between these endpoints.

> **Important:** These findings do not prove causation, and the classifier does not prove that individual comments were AI-generated. The results describe a strong observational association at the aggregate level.

## Final Result Statement

The preliminary evidence supports the project's central hypothesis at the observational level: **higher synthetic-like content prevalence is associated with lower human-to-human reply interaction** across subreddit-week communities.
