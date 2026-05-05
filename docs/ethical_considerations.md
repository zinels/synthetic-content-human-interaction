# Ethical Considerations

## Use of Public Reddit Data

This project analyzes publicly available Reddit comments. Public availability does not remove ethical responsibility — Reddit comments may contain personal experiences, health concerns, emotional topics, or sensitive information, particularly in communities such as r/AskDocs and r/Advice.

For that reason, this project avoids unnecessary exposure of raw user-generated content.

## Privacy Protection

- The repository does not include raw Reddit comment datasets by default, reducing the risk of redistributing sensitive or personally identifiable content.
- Analysis focuses on aggregate subreddit-week patterns rather than individual users.
- The project does not attempt to identify, track, or profile individual Reddit users.

## No Verified AI Authorship Claims

The classifier estimates synthetic-likeness based on writing style. It does not prove that any comment was written by artificial intelligence.

This distinction matters because falsely labeling a user as an AI author or bot could be misleading and unfair.

| ✅ Correct interpretation | The model estimates whether the writing style *appears* synthetic-like. |
|--------------------------|-------------------------------------------------------------------------|
| ❌ Incorrect interpretation | The model proves the comment was written by AI. |

## Sensitive Communities

r/AskDocs and r/Advice can contain sensitive personal information. Even with public posts, these communities require additional care:

- Raw examples from sensitive comments are not displayed in this repository
- Results are reported in aggregate
- The analysis avoids identifying individual users

## Observational Nature of the Study

This project is observational — it measures associations, not causation. The results do not prove that synthetic-like content directly causes lower interaction. Other factors that may influence both measures include subreddit moderation norms, topic type, community size, weekly events, user demographics, post popularity, comment depth, question-answer structure, and platform-level changes.

## Responsible Interpretation

This project should be interpreted as an exploratory social media mining study. Its findings should **not** be used to accuse users, remove content, or make automated moderation decisions without further validation.

## Summary

| Principle | Practice |
|-----------|----------|
| Analyze public data carefully | Raw CSVs excluded from the public repo |
| Avoid exposing unnecessary user content | Results reported at aggregate level only |
| Study patterns, not individuals | No user profiling or identification |
| State limitations clearly | Synthetic-likeness ≠ verified AI authorship |
| Treat results as observational | No causal claims are made |
