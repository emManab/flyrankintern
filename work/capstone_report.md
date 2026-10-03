# Capstone Report — Freestyle Search Intelligence: Content Risk Ranking

- **Author:** Manab Barman
- **Lane:** Freestyle — custom search/discoverability question
- **Repo:** emManab/flyrankintern
- **Date:** 2026-10-03

## 0. Abstract

This study asks whether a compact set of public-safe search and content signals can rank pages for human review when the observed data contains an associated performance-decline label. I use the FlyRank anonymized starter release of 30,000 pseudonymized content items with 90-day activity and content-context fields. I compare a transparent rule baseline with logistic regression, a decision tree, and a random forest using a client-aware holdout, while excluding label-derived trend fields and pseudonymous IDs from the feature vector. In the bundled reference run, Precision@50 was 0.240 for the baseline and about 0.740 for the random forest, with a 0.542 decline-label base rate. The resulting ranked queue is decision support for human review and signal discovery, not a causal estimate of traffic impact or a prediction of Google's ranking system.

## 1. Problem framing

### Research question

**Can a compact, public-safe set of search and content signals produce a useful ranking of pages associated with performance decline, without using the decline label itself as a feature?**

This is a freestyle question because the goal is not to reproduce one of the predefined lane labels verbatim. The decision supported is **which pages should receive human investigation first** when review capacity is limited.

- **Unit of analysis:** one pseudonymized content item.
- **Output:** a ranked risk score, action category, and reason codes.
- **Human action:** inspect the page and its search/engagement context before deciding whether to refresh, review metadata, expand content, or monitor.
- **Cost of a wrong call:** false positives consume editorial review time; false negatives can leave potentially useful review opportunities lower in the queue.

The model is intentionally a prioritization aid. It does not automate publishing decisions.

## 2. Data safety

The analysis uses the public-safe anonymized starter release at `data/raw/content_refresh_anonymized.csv`. The starter release contains approximately 30,000 pseudonymized content items and 44 columns; the activity fields include 90-day aggregates.

The label used for the bundled experiment is:

`is_declining_label = trend_direction == "down"`

This is a **snapshot-derived proxy label**, not a future treatment outcome. The stronger future-looking question would require a clean historical feature window followed by a separate future outcome window.

### Feature exclusions

The following are not model features:

- `trend_direction` and `trend_pct` — label-derived fields.
- `content_id` — row identity.
- `client_id` — grouping/context only; used for client-aware validation.
- Any future/overlapping outcome information identified during leakage review.
- Client names, domains, URLs, private queries, credentials, or raw private exports.

The repository contains only the supplied public-safe starter data and derived public-safe artifacts.

## 3. Baseline

The baseline is a transparent hand-written score combining observable visibility, freshness, position opportunity, and content-depth signals. It is a fair comparison because it ranks the same rows and is evaluated with the same primary metric as the learned models.

Reference result:

- **Baseline Precision@50:** 0.240

The baseline is intentionally simple: if a learned model cannot improve the review queue over a transparent rule, the added complexity is difficult to justify.

## 4. Model / analysis

The target is the snapshot-derived decline indicator defined above. The learned ranking compares:

1. Logistic regression — readable linear reference.
2. Decision tree — nonlinear, interpretable structure.
3. Random forest — ensemble ranking model for interactions and nonlinearities.

The model probability is used as the ranking score.

The feature policy is built from approved numeric and categorical search/content signals in `scripts/ml_utils.py`. Important observed signals include visibility, impressions, clicks, sessions, CTR, average position, content age, freshness, content depth, and engagement measures.

### Validation design

A client-aware holdout is preferred because rows from the same pseudonymized client can share hidden characteristics. Keeping a client on one side of the split reduces the risk that the model is rewarded for memorizing client-specific patterns.

Leakage checks explicitly remove the decline label and pseudonymous identifiers from model inputs.

## 5. Results

The bundled reference run reports the following comparison on the same evaluation setup:

| Method | ROC AUC | Average precision | Precision@50 |
|---|---:|---:|---:|
| Baseline rules | 0.627 | 0.468 | 0.240 |
| Logistic regression | 0.700 | 0.522 | 0.400 |
| Decision tree | 0.742 | 0.575 | 0.540 |
| Random forest | 0.750 | 0.618 | 0.740 |

The decline-label base rate is **0.542**. Because the starter target is already common, Precision@50 must be read together with the base rate and ranking metrics rather than as an isolated accuracy claim.

The reference run's random-forest feature importances are led by:

- `days_with_impressions`
- `log_impressions_90d`
- `avg_position`
- `content_age_days`
- `char_count`
- `word_count`
- `log_clicks_90d`
- `ctr`
- `scroll_rate`

These are **associations in this dataset**. Feature importance does not establish that changing any one signal will cause performance to change.

### Visual evidence

The repository includes the generated action mix, confidence mix, reason-code distribution, feature importance, and label distribution charts under `outputs/charts/`.

## 6. Limitations & honest framing

1. **Snapshot label:** the decline label is derived from the observed snapshot. It is not a clean future-window outcome.
2. **No causal claim:** the study cannot show that refreshing a page will improve traffic, rankings, clicks, or engagement.
3. **Starter-release scope:** results describe this anonymized release and should not be treated as universal search behavior.
4. **Client generalization:** client-aware validation helps reduce client leakage, but it does not guarantee performance on every future dataset.
5. **Model-version sensitivity:** tree-ensemble metrics can move slightly with library versions; the stable interpretation is the broad ranking separation, not false precision in the third decimal.
6. **Human review remains necessary:** a high score identifies a page for investigation; it does not prove that a specific editorial action is correct.

The appropriate language is **observed, measured, associated, directional, and decision-support**.

## 7. Ranked recommendations

The queue should be used as a review playbook:

1. **High-confidence multi-signal pages** — inspect first when several independent reason codes support review.
2. **Visible low-CTR pages** — check title/snippet and search-intent alignment before rewriting the page.
3. **Thin but visible pages** — inspect completeness and intent coverage before expanding content.
4. **Engagement-review candidates** — inspect usefulness and page experience before changing copy.
5. **Low-confidence items** — monitor rather than automatically acting on the model score.

The model should therefore determine **review order**, while the final editorial decision remains human.

## 8. Reproducibility

From the repository root:

```bash
pip install -r requirements.txt
python scripts/01_prepare_features.py
python scripts/02_baseline_score.py
python scripts/03_train_model.py
python scripts/04_evaluate_and_export.py
```

Or run the full reference pipeline:

```bash
python scripts/run_all.py
```

The modeling seed is 42. The capstone notebook is `work/notebooks/capstone.ipynb`. The weekly research trail is under `work/notebooks/`.

The deployed paper is generated from `docs/index.html` and published through the repository's GitHub Pages workflow.

## 9. Acknowledgments & data credit

**Built on the FlyRank ML Internship dataset.** Data credit: [FlyRank](https://flyrank.ai).

