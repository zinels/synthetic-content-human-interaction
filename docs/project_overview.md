# Project Overview

## Research Motivation

Large language models have made it easier to produce polished, formulaic, and synthetic-looking text at scale. As this type of writing becomes more common online, it raises an important social media mining question: do communities with more synthetic-like content show weaker human-to-human interaction?

Reddit is a useful setting for studying this question because it contains many topic-based communities with different norms, moderation practices, and conversation styles. Some subreddits encourage technical or informational responses, while others are more conversational, personal, or advice-based. This variation makes Reddit useful for comparing how synthetic-like writing relates to interaction patterns across communities.

## Research Question

> Are subreddit-weeks with higher synthetic-like content prevalence associated with lower levels of human-to-human reply interaction?

## Core Hypothesis

Higher synthetic-like prevalence will be associated with lower human-to-human interaction. In other words, weeks and communities with more synthetic-like writing are expected to show a lower share of reply interactions where both the child comment and parent comment appear human-like.

## Key Definitions

| Term | Definition |
|------|------------|
| **Synthetic-like content** | Comments that appear stylistically machine-like, polished, generic, formulaic, or detached from the immediate Reddit context. The label is based only on writing style — not verified AI authorship. |
| **Human-like content** | Comments that appear naturally written by a person in context, potentially including personal tone, specific details, informal phrasing, humor, frustration, lived experience, or subreddit-specific awareness. |
| **Synthetic prevalence** | The average synthetic-likeness score among comments in a given subreddit-week. |
| **h2h_ratio** | The share of reply-chain interactions where both the reply comment and its parent comment are classified as human-like. |

## Dataset Scope

**Subreddits:** r/AskScience, r/AskDocs, r/Advice, r/TodayILearned

**Collection window:** October 6, 2025 – December 28, 2025 (12 weeks)

| Subreddit | Clean Comments |
|-----------|---------------|
| Advice | 2,498 |
| AskDocs | 1,572 |
| AskScience | 2,541 |
| TodayILearned | 995 |
| **Total** | **7,606** |

Final analysis dataset: **48 subreddit-week observations** (4 subreddits × 12 weeks)

## Project Pipeline

1. Collect Reddit posts and comments from four subreddits
2. Clean data by removing deleted, removed, blank, moderator, system, and template content
3. Reconstruct reply chains using parent-child comment relationships
4. Create balanced and overlap annotation samples
5. Manually label comments as human-like, synthetic-like, or unsure
6. Train and compare four baseline classifiers
7. Select the best-performing model
8. Score the full cleaned comment corpus
9. Aggregate scores into subreddit-week synthetic prevalence
10. Compute weekly human-to-human interaction ratios
11. Run correlation and regression analysis
12. Interpret results as observational evidence

## Main Finding

Across 48 subreddit-week observations, the analysis finds a strong negative association between synthetic prevalence and human-to-human interaction:

| Statistic | Value |
|-----------|-------|
| Correlation | −0.9009 |
| Regression coefficient | −1.4913 |
| p-value | < 0.001 |
| R² | 0.863 |

Subreddit-weeks with higher synthetic-like prevalence tend to have lower human-to-human interaction. This result does not prove causation and does not prove that individual comments were AI-generated.
