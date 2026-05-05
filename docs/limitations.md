# Limitations

## 1. Synthetic-Likeness Is Not Verified AI Authorship

The most important limitation is that the classifier does not prove whether a comment was written by artificial intelligence. Labels and predictions describe writing style, not confirmed authorship. A human writer can produce synthetic-looking text; an AI tool can produce natural-looking text.

## 2. Manual Labels Are Subjective

Annotation depends on human judgment. Even with a clear rubric, synthetic-likeness can be subjective — some comments may be polished because the writer is careful or knowledgeable, and some may be generic because the topic itself invites a generic response. The overlap annotation sample reduces but cannot eliminate subjectivity.

## 3. Positive-Class Classification Is Difficult

The current best model has a useful ROC-AUC but a modest F1 score. The classifier captures signal but is not strong enough to make confident claims about individual comments. This is why the project focuses on aggregate subreddit-week patterns.

## 4. The 0.5 Threshold Is Operational

The `h2h_ratio` calculation uses a threshold of 0.5 to binarize human-like vs. synthetic-like. This is a practical choice, not a ground-truth boundary. Future work could test alternative thresholds or use continuous scores directly.

## 5. Reddit Communities Differ Naturally

The four subreddits vary in topic, moderation style, user expectations, and conversation structure. AskScience may naturally produce formal answers; Advice may naturally produce personal replies; AskDocs may generate structured responses due to its medical context; TodayILearned may have shorter, more casual reply chains. These inherent differences may independently influence both synthetic prevalence and h2h_ratio.

## 6. Observational Design Cannot Prove Causality

The regression analysis tests association, not causation. Even with a strong negative correlation, the project cannot prove that synthetic-like writing caused lower interaction. Confounding variables are likely present.

## 7. Limited Time Window

The data covers a fixed 12-week window (October 6 – December 28, 2025). This window makes comparisons controlled and manageable, but may not represent long-term subreddit behavior. Future work could expand the time range to test stability.

## 8. Platform and Collection Constraints

Reddit data access can be limited by API restrictions, pagination, deleted content, moderation changes, and endpoint behavior. The custom collection notebooks handle known issues, but some comments or posts may still be missed.

## 9. Cleaning May Remove Some Real Interaction

The cleaning pipeline removes deleted, removed, moderator, system, template, and broken-chain comments. This improves data quality but may also remove content that was part of organic conversation.

## 10. Results Should Be Treated as Preliminary

The current aggregate-level results are strong, but this project should be interpreted as exploratory. It provides evidence that synthetic-like writing *may be associated* with weaker human-to-human interaction — broader claims would require further validation.

## Summary

The project is strongest as an **aggregate observational analysis**. Its main contribution is not detecting AI authorship at the individual level, but showing that synthetic-like writing patterns may be meaningfully associated with community-level interaction patterns.
