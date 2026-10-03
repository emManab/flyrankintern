# FlyRank ML Internship — Starter Repo

**Applied Search Intelligence: Google Search Ranking & Discoverability**

This is the starting point for the FlyRank ML Internship. You **clone it into your own public
repo** (one click — *Use this template*), build everything there, and submit that repo URL on
each assignment in your portal — it's your workspace, your submission, and your portfolio all
at once. The rhythm is simple: do the work, commit it, submit on the card. Done.

Everything here runs on a small **anonymized** slice of real FlyRank search data. No credentials,
no private client data, no setup headaches.

> **New here?** Two reads: **[SETUP.md](SETUP.md)** (GitHub, Colab, and data access — ten
> minutes, with every silent pitfall flagged), then **[GUIDE.md](GUIDE.md)** (every file
> explained, what to edit vs. leave alone, and where your own work goes — five minutes).

---

## Quickstart — first win in 2 minutes

The fastest path is Google Colab (one click, zero install). Open Notebook 1 and run all cells:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/emManab/flyrankintern/blob/main/notebooks/01_first_look_and_discovery.ipynb?flush_cache=true)
 **Week 1 — Run it, then discover a real truth yourself**

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/emManab/flyrankintern/blob/main/notebooks/02_your_first_readable_model.ipynb?flush_cache=true)
 **Week 2 — The model is just a rule you can read**

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/emManab/flyrankintern/blob/main/notebooks/03_working_with_the_full_release.ipynb?flush_cache=true)
 **Weeks 3+ — The full release (~79M rows) via DuckDB, no download needed** — hosted at
 [`FlyRank/internship-warehouse`](https://huggingface.co/datasets/FlyRank/internship-warehouse) (gated: request access + accept the data-use terms, approval is instant)

---

## Your assignment notebooks — open, fill, save, done

Every assignment is one pre-named skeleton notebook in `work/notebooks/`. Click its badge,
fill the sections in order, then **File → Save a copy in GitHub → OK** — the dialog is
already pre-filled with your repo and the right path.

> **The badges know whose repo they're in.** About 30 seconds after you create your copy, an
> automatic commit ("Point Colab badges at this copy") rewires every badge in it to open
> **your** notebooks — with your saved work — instead of the shared read-only ones. Reading
> this on the shared starter page? The badges below open blank previews; make your copy
> first ([SETUP.md](SETUP.md), Moment 1).

| Week | Card | Notebook | Open |
|---|---|---|---|
| 1 | ML-02 | `w01_research_question` | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/emManab/flyrankintern/blob/main/work/notebooks/w01_research_question.ipynb?flush_cache=true) |
| 2 | ML-03 | `w02_ml_task_framing` | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/emManab/flyrankintern/blob/main/work/notebooks/w02_ml_task_framing.ipynb?flush_cache=true) |
| 3 | ML-04 | `w03_data_contract` | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/emManab/flyrankintern/blob/main/work/notebooks/w03_data_contract.ipynb?flush_cache=true) |
| 3 | ML-05 | `w03_feature_leakage_check` | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/emManab/flyrankintern/blob/main/work/notebooks/w03_feature_leakage_check.ipynb?flush_cache=true) |
| 4 | ML-06 | `w04_signal_audit` | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/emManab/flyrankintern/blob/main/work/notebooks/w04_signal_audit.ipynb?flush_cache=true) |
| 4 | ML-07 | `w04_baseline_score` | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/emManab/flyrankintern/blob/main/work/notebooks/w04_baseline_score.ipynb?flush_cache=true) |
| 5 | ML-08 | `w05_model` | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/emManab/flyrankintern/blob/main/work/notebooks/w05_model.ipynb?flush_cache=true) |
| 6 | ML-09 | `w06_validation_audit` | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/emManab/flyrankintern/blob/main/work/notebooks/w06_validation_audit.ipynb?flush_cache=true) |
| 7 | ML-10 | `w07_action_playbook` | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/emManab/flyrankintern/blob/main/work/notebooks/w07_action_playbook.ipynb?flush_cache=true) |
| 8 | ML-11 | `capstone` | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/emManab/flyrankintern/blob/main/work/notebooks/capstone.ipynb?flush_cache=true) |

Badges not opening *your* copy? Colab's built-in opener always works: **File → Open notebook
→ GitHub tab** → paste `github.com/you/your-repo` → pick the notebook.

### Prefer local?

```bash
git clone <this-repo-url>
cd flyrank-ml-internship-starter
pip install -r requirements.txt          # or: uv pip install -r requirements.txt
python scripts/run_all.py
```

That runs the whole pipeline on the bundled sample and writes results to `outputs/`.

---

## What you get

| Path | What it is |
|---|---|
| `notebooks/` | Week 1–2 **first-win notebooks** (Colab-ready). Start here. |
| `scripts/01–05` + `run_all.py` | The runnable reference pipeline: prepare → baseline → train → evaluate → PDF. |
| `data/raw/content_refresh_anonymized.csv` | The anonymized starter dataset (~30k pages). |
| `outputs/` | Example outputs so you can see the **target shape** (`model_report.md`, `refresh_queue_sample.csv`, `charts/`). |
| `work/` | **Your space.** Lane experiments and your capstone live here — see `work/README.md`. |
| `docs/` | The core docs + the data dictionary (see below). |

### Read these (in `docs/`)

1. **`ml-core-foundation-framework.md`** — the first-principles map of ML as a whole system. The backbone of the live sessions.
2. **`ml-intern-dataset-and-lane-guide.md`** — how to use the data safely, the capstone workflow, and the analysis "lanes" you can pick from.
3. **`intern-free-tooling-guide.md`** — the zero-budget tool stack (Python, Colab, free AI assistants). You never need to pay for anything.
4. **`data-dictionary.md`** — all 44 columns: meaning, scale, and gotchas. Keep it open while you work.

---

## The pipeline (what `run_all.py` does)

```text
01_prepare_features.py   clean + build the feature vector, define the label
02_baseline_score.py     a transparent hand-rule "fix this first" score
03_train_model.py        logistic regression, decision tree, random forest (client-holdout split)
04_evaluate_and_export.py  ranked queue + charts + Markdown report
05_build_pdf_report.py   a shareable PDF summary
```

On the bundled sample, the learned model clearly beats the hand-written rule at picking the right
pages to review first (**Precision@50 ≈ 0.24 → 0.74**; the model number can land 0.68–0.74
depending on library versions — the ~3x lift is the point). The notebooks compute these numbers
live, so they always reflect the current data and environment.

**Teaching point:** the model is the capstone, but the *workflow* is the lesson —
`problem framing → data cleaning → baseline → first model → evaluation → explainable recommendation`.

---

## Data safety (read `DATA_USE.md`)

- Only the small **anonymized** CSV ships here — no client names, domains, URLs, titles, or keywords.
- **Never** add raw private client data to this repo or your fork. Need more data? Request an approved
  release from your mentor — never export it yourself.
- Don't paste client data into third-party AI tools.
- Frame every result as **observed / measured / directional / decision-support** — never
  "I predicted Google's algorithm."

The `.gitignore` blocks datasets by default, and CI fails any commit that includes a dataset.

---

## Assignments & schedule

Weekly assignments, live events, and the capstone live on **your portal board** (your
enrollment email has your access link). This repo is the shared technical foundation they all
build on — and the `skills/` folder here is the instruction library for your AI assistant
(start at [skills/README.md](skills/README.md)).

**First time with GitHub?** You need exactly four things (full walkthrough: [SETUP.md](SETUP.md)):
1. A free account at github.com.
2. Your own copy of this repo: **Use this template → Create a new repository** → public.
   (One click — brings the notebooks, `work/`, and the CI leak-guard with it.)
3. In Colab: *File → Save a copy in GitHub* — opened from your copy's badges, the dialog is
   already pre-filled with your repo and path, so it's just OK (Colab handles auth).
4. That's your submission repo — share its **github.com/you/your-repo** URL with Assignment 1
   (never a colab.research.google.com or drive.google.com link).

---

*Track leads: Mirza Ašćerić (ML) · Hole (data engineering). Code under MIT (see `LICENSE`); data under `DATA_USE.md`.*


---

# My Completed Assignment — Content Refresh Prioritization

> **Submission work:** ML-02 → ML-12 completed in `work/notebooks/`, with a capstone report and a public-safe research page.

## What was the task?

The project asks:

**Which existing content pages should an editorial team review first when there is limited capacity for content refresh?**

The goal was not to automatically publish or rewrite pages. The goal was to build an explainable, validated **review-prioritization system** that ranks pages and tells a human reviewer why an item was selected.

### Dataset

- **30,000** anonymized content items
- **32** pseudonymized clients
- **44** columns
- 90-day performance/activity window plus recent-window and content-context fields
- Declining-label rate: **54.2%** in the prepared reference run
- No client names, domains, URLs, titles, or private search queries are exposed

## What I built

| Assignment | What I completed | Main output |
|---|---|---|
| **ML-02** | Research question and decision framing | Defined the refresh-prioritization problem and costs of wrong calls |
| **ML-03** | ML task framing | Binary classification used as a ranking problem; Precision@50 selected as primary metric |
| **ML-04** | Data contract | Defined grain, time windows, features, label, exclusions, and data limitations |
| **ML-05** | Leakage + feature audit | Excluded label-derived fields, IDs, product flags, and unsafe future information |
| **ML-06** | Signal audit | Tested visibility, freshness, and CTR-related signals against the observed label |
| **ML-07** | Transparent baseline | Built a fixed weighted score with human-readable reason codes and top-20 review |
| **ML-08** | Model comparison | Compared logistic regression, decision tree, and random forest |
| **ML-09** | Validation audit | Used client-aware validation and audited methodology/leakage/claims |
| **ML-10** | Action playbook | Converted ranked signals into human-review actions and monitoring triggers |
| **ML-11** | Capstone | Combined the full workflow into a reproducible end-to-end analysis |
| **ML-12** | Demo + communication | Prepared demo outline, social-post version, and employer-facing summary |

## Model output

The reference pipeline compares a transparent rule against three learned models using the same ranking objective:

| Method | ROC AUC | Avg. Precision | Precision@50 |
|---|---:|---:|---:|
| Baseline rules | 0.627 | 0.468 | **0.240** |
| Logistic regression | 0.700 | 0.522 | **0.400** |
| Decision tree | 0.742 | 0.575 | **0.540** |
| Random forest | **0.750** | **0.618** | **0.740** |

**Base rate: 0.542.** The bundled reference run selected the random forest by Precision@50.

The leading model features included:

1. `days_with_impressions`
2. `log_impressions_90d`
3. `avg_position`
4. `content_age_days`
5. `char_count`
6. `word_count`
7. `log_clicks_90d`
8. `ctr`
9. `scroll_rate`
10. `days_with_sessions`

These are model signals, **not causal explanations**.

## Final review queue

The reference export produced a ranked queue with:

- **3,605** high-confidence items
- **11,395** medium-confidence items
- **15,000** low-confidence items
- **13,093** monitor recommendations
- **8,178** refresh recommendations
- **6,657** refresh + CTR review recommendations
- **1,990** refresh + engagement review recommendations
- **82** expand + refresh recommendations

Each queue item can carry reason codes such as:

- `declining_with_demand`
- `stale_visible_page`
- `thin_visible_page`
- `low_ctr_visible_page`
- `low_engagement_visible_page`
- `model_decline_risk`
- `visible_model_opportunity`

The queue is designed as **decision-support**. A human should inspect the page and current context before taking action.

## Key methodology decisions

### 1. Transparent baseline before ML

The baseline combines visibility, freshness risk, position opportunity, and content-depth gap. This creates a readable benchmark that the model has to beat.

### 2. Precision@50 instead of accuracy

The practical question is **“Which pages should we review first?”**, so Precision@50 is more aligned with the decision than raw accuracy.

### 3. Client-aware validation

Rows from the same client can share hidden characteristics. The reference training pipeline therefore attempts a client holdout when both classes are represented, with a stratified row holdout only as a fallback.

### 4. Leakage controls

`trend_direction` and `trend_pct` are never model features because the label is derived from the trend. Client/content IDs are used for grouping and audit only. Existing product scores/flags and unsafe future information are excluded from predictors.

### 5. Honest claims

The analysis supports statements such as **“the model ranks/flags pages in this dataset”**. It does **not** claim that refreshing a page will cause traffic growth or that the model predicts Google's algorithm.

## Completed work

### Assignment notebooks

All completed notebooks are in [`work/notebooks/`](work/notebooks/):

- [`w01_research_question.ipynb`](work/notebooks/w01_research_question.ipynb)
- [`w02_ml_task_framing.ipynb`](work/notebooks/w02_ml_task_framing.ipynb)
- [`w03_data_contract.ipynb`](work/notebooks/w03_data_contract.ipynb)
- [`w03_feature_leakage_check.ipynb`](work/notebooks/w03_feature_leakage_check.ipynb)
- [`w04_signal_audit.ipynb`](work/notebooks/w04_signal_audit.ipynb)
- [`w04_baseline_score.ipynb`](work/notebooks/w04_baseline_score.ipynb)
- [`w05_model.ipynb`](work/notebooks/w05_model.ipynb)
- [`w06_validation_audit.ipynb`](work/notebooks/w06_validation_audit.ipynb)
- [`w07_action_playbook.ipynb`](work/notebooks/w07_action_playbook.ipynb)
- [`capstone.ipynb`](work/notebooks/capstone.ipynb)

### Capstone report

- [`work/capstone_report.md`](work/capstone_report.md)
- [`docs/index.html`](docs/index.html) — public-safe research page

### Reference outputs

- [`outputs/model_report.md`](outputs/model_report.md)
- [`outputs/refresh_queue_sample.csv`](outputs/refresh_queue_sample.csv)
- [`outputs/summary.json`](outputs/summary.json)
- [`outputs/model_results.json`](outputs/model_results.json)
- [`outputs/charts/`](outputs/charts/)

## How to reproduce the analysis

From the repository root:

```bash
python scripts/01_prepare_features.py
python scripts/02_baseline_score.py
python scripts/03_train_model.py
python scripts/04_evaluate_and_export.py
```

The modeling seed is **42**. The pipeline regenerates the prepared features, baseline, model predictions, ranked queue, charts, and report.

## What this project demonstrates

**Problem framing → data contract → leakage audit → signal analysis → transparent baseline → ML model → honest validation → explainable action queue → capstone communication.**

The important output is not only the model score. It is the complete workflow for turning an ambiguous content-performance problem into a reproducible and reviewable ML decision-support system.