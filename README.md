# Gender Bias in Multilingual Transformer Models

![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python&logoColor=white)
![HuggingFace](https://img.shields.io/badge/HuggingFace-Transformers-yellow?logo=huggingface&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-red?logo=pytorch&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green)

**Author:** Charalampos Zisis

---

## Overview

This project investigates **gender bias in mBERT** (`bert-base-multilingual-cased`) across five languages: English, Dutch, French, German, and Spanish. Using controlled fill-mask probing, WinoBias benchmark validation, and corpus co-occurrence analysis on multilingual mC4 data, the project examines whether and how bias varies across linguistic typologies.

---

## Research Question

> *Does gender bias in multilingual transformer models vary across languages, and to what extent can these differences be related to gender-occupation patterns in multilingual data?*

### Sub-questions
| | Question |
|---|---|
| **SQ1** | How does mBERT respond to gendered fill-mask prompts across EN, NL, FR, DE, ES? |
| **SQ2** | Do languages with grammatical gender (FR, DE, ES) show different bias than those without (EN, NL)? |
| **SQ3** | To what extent do gender-occupation patterns in mC4 align with model bias scores? |

---

## Methodology

1. **Controlled fill-mask probing** — Template sentences with a `[MASK]` slot fed to mBERT for 8 occupations per language (4 male-stereotyped, 4 female-stereotyped). Bias measured as:
   ```
   signed_bias = P(male) / (P(male) + P(female)) - 0.5
   ```
   Positive = male-leaning, negative = female-leaning.

2. **WinoBias benchmark validation** — English template results cross-validated against the WinoBias benchmark, achieving **r = 0.794** (strong agreement), confirming template reliability.

3. **mC4 corpus co-occurrence analysis** — Gender-term co-occurrences with occupations counted across 1,000-document samples per language from mC4, then compared with model bias scores.

---

## Key Findings

| Language | Avg Signed Bias | Grammar Type |
|---|:---:|---|
| French | 0.413 | Grammatical gender |
| Dutch | 0.404 | Non-grammatical |
| German | 0.372 | Grammatical gender |
| Spanish | 0.293 | Grammatical gender |
| English | 0.169 | Non-grammatical |

- All five languages show a **male bias** in mBERT; English is the least biased.
- **Dutch** (non-grammatical) shows nearly the same bias as **French** (grammatical) — grammatical gender alone does not drive mBERT male bias.
- **German** is a notable outlier: high model bias but low mC4 male co-occurrence ratio, suggesting morphological gender marking or cross-lingual training dynamics as confounds rather than surface corpus patterns.

---

## Project Structure

```
├── Gender.ipynb                # Main analysis notebook
├── Zisis_Presentation.pdf      # Project presentation slides
├── requirements.txt            # Python dependencies
└── README.md
```

> **Note:** Raw datasets (WinoBias, mC4) are streamed automatically from HuggingFace — no local files needed.

---

## How to Run

```bash
# Install dependencies
pip install -r requirements.txt

# Open the notebook
jupyter notebook Gender.ipynb
```

The notebook is also fully runnable on **Google Colab** — open it and run all cells. All datasets load automatically from HuggingFace.

---

## Stack

`Python` `PyTorch` `HuggingFace Transformers` `Pandas` `NumPy` `Matplotlib` `Seaborn` `SciPy`  
Datasets: WinoBias · mC4 (multilingual)

---

## Citation

If you use or reference this work, please cite:

```
Zisis, C. (2025). Gender Bias in Multilingual Transformer Models.
Utrecht University — INFOMTLAC.
GitHub: https://github.com/Hariszss/gender-bias-multilingual-mBERT
```
