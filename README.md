# POS Tagging for the Healthcare Domain

Compares **rule-based** and **statistical (HMM)** part-of-speech tagging on medical text, and measures how **domain-specific vocabulary** affects tagging accuracy.

## Overview

- **Data:** [MTSamples medical transcriptions](https://www.kaggle.com/datasets/tboyle10/medicaltranscriptions). One sentence from each of 200 reports: 40 for adaptation, 160 for testing.
- **Reference tags:** generated automatically by spaCy `en_core_web_sm` and mapped to the 12-tag Universal tagset.
- **Taggers:**
  - **Rule-based:** word lists, a medical lexicon and suffix rules
  - **HMM (general):** trained on the NLTK Penn Treebank sample, with Lidstone smoothing
  - **HMM (adapted):** Penn Treebank plus the 40 healthcare sentences

## Results

| Tagger | Accuracy | Macro F1 |
|---|---|---|
| Rule-based | 0.839 | 0.757 |
| HMM (general) | 0.769 | 0.669 |
| HMM (adapted) | 0.789 | 0.695 |

- On words **unseen** in the Penn Treebank (22.8% of test tokens), general HMM accuracy drops from **89.9% to 33.0%**. The rule-based tagger drops only from 85.0% to 80.1%.
- Adding 40 healthcare sentences improves the HMM by **+1.95 points** (paired bootstrap 95% CI: +1.4 to +2.6).

## How to run

1. Open `nlp_assignment2_reliable_comparison.ipynb` in Google Colab.
2. Choose **Runtime → Run all**.
3. Enter your Kaggle username and API key when prompted, to download the dataset.

## Files

| File | Description |
|---|---|
| `nlp_assignment2_reliable_comparison.ipynb` | Full code: data, taggers, evaluation, charts |
| `POS_Tagging_Healthcare_Report_Final.docx` / `.pdf` | Project report |

## Limitations

The reference tags come from spaCy, not human annotation, so the scores measure **agreement with spaCy**, not true accuracy. The samples are also small (40 adaptation and 160 test sentences).

## Tools

Python, NLTK, spaCy, scikit-learn, pandas, matplotlib, seaborn
