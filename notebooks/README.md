# Notebooks

This folder contains the main computational workflow for the project.

The notebooks are organized in the order they should be reviewed.

## Notebook 1: `01_collect_askscience.ipynb`

This notebook collects, cleans, and exports Reddit comments from the AskScience subreddit.

Primary goals:

- Collect comments from the selected 12-week window.
- Preserve post and parent-comment metadata.
- Remove deleted, removed, blank, moderator, and system-generated content.
- Remove repeated templates and boilerplate.
- Reconstruct usable reply-chain relationships.
- Export clean comments and weekly summaries.

## Notebook 2: `02_collect_todayilearned.ipynb`

This notebook collects, cleans, and exports Reddit comments from the TodayILearned subreddit.

Primary goals:

- Collect comments from the selected 12-week window.
- Apply the same cleaning and filtering pipeline as the other subreddit notebooks.
- Export cleaned comments and weekly summaries.
- Preserve comparable subreddit-week structure for downstream analysis.

## Notebook 3: `03_collect_askdocs.ipynb`

This notebook collects, cleans, and exports Reddit comments from the AskDocs subreddit.

Primary goals:

- Collect comments from the selected 12-week window.
- Apply privacy-conscious cleaning due to the sensitive nature of health-related discussions.
- Remove moderator/system content and deleted/removed comments.
- Reconstruct reply-chain relationships.
- Export clean comments and weekly summaries.

## Notebook 4: `04_collect_advice.ipynb`

This notebook collects, cleans, and exports Reddit comments from the Advice subreddit.

Primary goals:

- Collect comments from the selected 12-week window.
- Remove system artifacts, repeated templates, deleted content, and broken reply chains.
- Prepare clean comments for labeling, model scoring, and subreddit-week aggregation.

## Notebook 5: `05_modeling_and_analysis.ipynb`

This notebook contains the modeling and final analysis pipeline.

Primary goals:

- Combine cleaned subreddit datasets.
- Prepare balanced and overlap annotation samples.
- Train and compare four baseline classifiers.
- Select the best-performing classifier.
- Score the full cleaned corpus for synthetic-likeness.
- Compute weekly synthetic prevalence.
- Compute the human-to-human interaction metric, `h2h_ratio`.
- Build the final subreddit-week analysis dataset.
- Run correlation and regression analysis.
- Generate the main result table and figure.

## Recommended Review Order

A professor or reviewer should read the notebooks in this order:

1. `01_collect_askscience.ipynb`
2. `02_collect_todayilearned.ipynb`
3. `03_collect_askdocs.ipynb`
4. `04_collect_advice.ipynb`
5. `05_modeling_and_analysis.ipynb`

## Notes

Raw Reddit CSV files are not included in the repository by default. This is intentional because raw social media data can contain sensitive or personally identifiable content. The notebooks document the workflow used to collect, clean, process, model, and analyze the data.
