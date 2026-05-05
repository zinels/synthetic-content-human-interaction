# Data Dictionary

This document describes the main fields used across project datasets. Actual CSV files may contain additional helper columns depending on the collection, cleaning, labeling, or modeling stage.

## Raw Comment Fields

| Field | Description |
|-------|-------------|
| `comment_id` | Unique Reddit comment identifier |
| `post_id` | Identifier of the Reddit submission the comment belongs to |
| `parent_id` | Identifier of the parent item (may refer to a post or another comment) |
| `subreddit` | Name of the subreddit |
| `created_utc` | Comment creation timestamp in UTC |
| `body` | Raw comment text |
| `author` | Reddit username, if collected and available |
| `score` | Reddit upvote-based score, if available |
| `permalink` | Link to the comment or post, if available |

## Cleaned Comment Fields

| Field | Description |
|-------|-------------|
| `comment_id` | Unique cleaned comment identifier |
| `post_id` | Reddit submission identifier |
| `parent_id` | Parent post or parent comment identifier |
| `parent_comment_id` | Parent comment identifier when the parent is another comment |
| `subreddit` | Name of the subreddit |
| `week_start` | Start date of the week used for weekly aggregation |
| `clean_text` | Cleaned version of the comment text |
| `is_direct_post_reply` | Whether the comment replies directly to the post |
| `is_comment_reply` | Whether the comment replies to another comment |
| `parent_survived_cleaning` | Whether the parent comment remains in the cleaned dataset |

## Exclusion Log Fields

| Field | Description |
|-------|-------------|
| `comment_id` | Identifier of the removed comment |
| `subreddit` | Subreddit where the comment appeared |
| `reason` | Reason the comment was excluded |
| `body` | Comment text or partial text, depending on the export |

**Common exclusion reasons:** blank text · deleted text · removed text · moderator/system content · template content · meta-thread content · broken parent chain

## Annotation Fields

| Field | Description |
|-------|-------------|
| `comment_id` | Unique comment identifier |
| `post_id` | Reddit submission identifier |
| `subreddit` | Name of the subreddit |
| `clean_text` | Text shown to annotators |
| `label` | Manual annotation label (see below) |
| `annotator` | Annotator identifier, if multiple annotators are used |
| `sample_type` | Whether the row came from the balanced or overlap sample |

| Label | Meaning |
|-------|---------|
| `0` | Human-like |
| `1` | Synthetic-like |
| `-1` | Unsure |

## Model Output Fields

| Field | Description |
|-------|-------------|
| `comment_id` | Unique comment identifier |
| `subreddit` | Name of the subreddit |
| `week_start` | Weekly aggregation date |
| `clean_text` | Cleaned comment text |
| `synthetic_score` | Model-estimated probability/score for synthetic-like writing |
| `synthetic_label` | Binary model label using the selected threshold |
| `human_like_binary` | Whether the comment is treated as human-like in downstream analysis |

## Weekly Analysis Fields

| Field | Description |
|-------|-------------|
| `subreddit` | Name of the subreddit |
| `week_start` | Start date of the weekly observation |
| `n_comments` | Number of cleaned comments in the subreddit-week |
| `synthetic_prevalence` | Mean synthetic score for the subreddit-week |
| `n_reply_edges` | Number of usable parent-child reply interactions |
| `n_human_human_edges` | Number of reply interactions where both child and parent are human-like |
| `h2h_ratio` | Human-to-human reply ratio |

## Key Derived Variables

**`synthetic_prevalence`**synthetic_prevalence = mean(synthetic_score) per subreddit-week

**`h2h_ratio`**h2h_ratio = human-human reply interactions / all usable reply interactions

**`subreddit`** — categorical control variable used in the regression model.

## Final Regression Formulah2h_ratio ~ synthetic_prevalence + C(subreddit)
