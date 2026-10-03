# Capstone Report — Content Refresh Prioritization

- **Author:** Manab Barman
- **Lane:** Content refresh prioritization
- **Repo:** emManab/flyrankintern
- **Date:** 2026-10-03

## 0. Abstract

This project asks how an editorial team can rank existing content pages for refresh review when review capacity is limited. The public-safe starter release contains 30,000 pseudonymized content items across 32 clients with 90-day activity and content-context fields. I compare a transparent rule baseline with logistic regression, a decision tree and a random forest using client-aware validation where class coverage permits. The bundled reference run measured Precision@50 of 0.240 for the baseline and about 0.740 for the random forest, with a 0.542 declining-label base rate. The result is decision-support for human review, not a causal estimate of refresh impact.

## 1. Problem framing

The decision is which pages an editor should inspect first. One row represents one pseudonymized content item in the supplied snapshot. The output is a ranked queue with reason codes and confidence. A false positive consumes review time; a false negative can leave a declining page unattended.

## 2. Data safety

The main release is `data/raw/content_refresh_anonymized.csv`. The model uses approved numeric and categorical feature lists. `trend_direction` and `trend_pct` are label-derived and excluded; `content_id` and `client_id` are grouping/context only. Existing product flags and future/overlapping outcome information are not model inputs. No client names, domains, URLs or private queries are published.

## 3. Baseline

The frozen baseline combines visibility, freshness risk, position opportunity and depth gap with fixed weights and reason codes. The reference evaluation gives the baseline Precision@50 as 0.240.

## 4. Model / analysis

The target is `is_declining_label = trend_direction == down`. Logistic regression provides a readable starting point, followed by a decision tree and random forest. The classifier probability is used as the ranking score. The reference run selected random forest by Precision@50. Its leading features include days with impressions, log impressions, average position and content age. These are associations used for prioritization, not causal drivers.

## 5. Evaluation

The preferred split is client-aware holdout because rows from the same client can share hidden characteristics. The reference run reports:

| Method | ROC AUC | Avg precision | Precision@50 |
|---|---:|---:|---:|
| Baseline rules | 0.627 | 0.468 | 0.240 |
| Logistic regression | 0.700 | 0.522 | 0.400 |
| Decision tree | 0.742 | 0.575 | 0.540 |
| Random forest | 0.750 | 0.618 | 0.740 |

The label base rate is 0.542. The exact third decimal of tree-ensemble metrics can vary with library versions, so the stable interpretation is the approximate ranking lift rather than false precision.

## 6. Interpretation

The learned ranking combines visibility, position, age, content depth and engagement-related signals. The most useful operational interpretation is that pages with several independent supporting signals can be moved earlier in the review queue. Stable pages appearing near the top are important error cases because they show where the ranking can over-prioritize visibility or freshness.

## 7. Recommendation

1. Inspect high-confidence items with multiple supporting reason codes first.
2. For visible low-CTR items, review title/snippet and search-intent alignment before rewriting content.
3. For thin visible items, inspect completeness and expand only when the intent requires it.
4. For engagement candidates, inspect usefulness and page experience before changing copy.
5. Keep low-confidence items in monitor status until fresh evidence changes their priority.

These are review recommendations, not automatic publishing decisions.

## 8. Reproducibility

Run the reference pipeline from the repository root:

```bash
python scripts/01_prepare_features.py
python scripts/02_baseline_score.py
python scripts/03_train_model.py
python scripts/04_evaluate_and_export.py
```

The reference modeling seed is 42. The notebooks in `work/notebooks/` document the research question, task framing, data contract, leakage checks, signal audit, baseline, model comparison, validation, action playbook and capstone summary.

## 9. Acknowledgments & data credit

Built on the FlyRank ML Internship dataset. Data credit: https://flyrank.ai
