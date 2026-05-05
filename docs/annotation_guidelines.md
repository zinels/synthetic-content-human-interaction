# Annotation Guidelines

## Purpose

The annotation task is to label Reddit comments based on **writing style**.

Annotators are not deciding whether a comment was truly written by artificial intelligence. Instead, annotators judge whether the comment appears more human-like or synthetic-like based on the text alone.

## Labels

| Label | Meaning |
|-------|---------|
| `0` | Human-like |
| `1` | Synthetic-like |
| `-1` | Unsure |

Use `-1` only when the comment is too short, too ambiguous, or too context-dependent to make a reasonable judgment. Do not overuse it — if the comment provides enough stylistic evidence, choose `0` or `1`.

## Label 0: Human-like

Use `0` when the comment reads like a natural person responding in context.

**Common indicators:**
- Specific details and concrete references
- Personal tone or lived experience
- Informal phrasing, humor, frustration, or opinion
- Subreddit-specific awareness
- Direct engagement with the parent post or comment
- Slightly uneven or imperfect structure

Human-like comments do not need to be grammatically perfect — small imperfections often make writing feel more natural.

## Label 1: Synthetic-like

Use `1` when the comment appears polished, generic, formulaic, or machine-like.

**Common indicators:**
- Overly balanced structure
- Generic explanations without contextual grounding
- Repetitive or templated phrasing
- Very polished or formal tone in a casual setting
- Lists that feel auto-generated
- Lack of personal voice or subreddit-specific awareness
- Abstract or broad statements instead of specific details
- Smooth but emotionally flat writing
- Phrasing that sounds like a general-purpose assistant

> Synthetic-like does not mean the comment is definitely AI-generated. It only means the style *appears* synthetic-like.

## Label -1: Unsure

Use `-1` when there is not enough evidence to decide.

**Examples:**
- Very short or one-word replies
- Comments containing only links or usernames
- Comments that only quote another user
- Comments requiring missing context to interpret
- Comments that are equally plausible as either class

## Annotation Rules

1. Do not label based on whether you agree with or find the comment helpful.
2. Do not label based on factual correctness.
3. Do not treat length alone as evidence of either class.
4. Do not assume polished writing is automatically synthetic-like.
5. Do not assume informal writing is automatically human-like.
6. Focus on: **writing style, context awareness, specificity, and naturalness**.

## Quick Reference: Style Signals

| Human-like | Synthetic-like |
|-----------|---------------|
| Reacts directly to another user | Generic, could fit many threads |
| Includes personal experience | Clean but detached |
| Casual or uneven wording | Mechanically balanced structure |
| Makes a joke or shows emotion | Emotionally flat |
| Specific local or situational context | Abstract and broad |
| Slightly imperfect grammar | Unusually polished for the setting |

## Final Reminder

The annotation goal is not perfection. The goal is to create a **consistent, defensible training set** for estimating synthetic-like writing patterns at scale.
