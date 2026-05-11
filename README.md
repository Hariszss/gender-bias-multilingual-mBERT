# Gender Bias in Multilingual Transformer Models

**Course:** INFOMTLAC — Utrecht University, 2025  
**Author:** Charalampos Zisis

## Overview

This project investigates gender bias in **mBERT** (`bert-base-multilingual-cased`) across five languages: English, Dutch, French, German, and Spanish.

## Research Question

> Does gender bias in multilingual transformer models vary across languages, and to what extent can these differences be related to gender-occupation patterns in multilingual data?

### Sub-questions
- **SQ1:** How does mBERT respond to gendered fill-mask prompts across the five languages?
- **SQ2:** Do languages with grammatical gender (FR, DE, ES) show different bias patterns compared to those without (EN, NL)?
- **SQ3:** To what extent do gender-occupation patterns in mC4 align with the bias scores produced by the model?

## Methodology

1. **Controlled fill-mask probing** — Template sentences with a `[MASK]` slot fed to mBERT across 8 occupations (4 male-stereotyped, 4 female-stereotyped) per language. Bias measured as `signed_bias = P(male) / (P(male) + P(female)) - 0.5`.
2. **WinoBias benchmark validation** — English template results cross-validated against WinoBias (r = 0.794), confirming template reliability.
3. **mC4 corpus co-occurrence analysis** — Gender-term co-occurrences with occupations counted in 1,000-document samples per language from mC4, compared with model predictions.

## Key Findings

| Language | Avg Signed Bias | Grammar Type |
|---|---|---|
| French | 0.413 | Grammatical gender |
| Dutch | 0.404 | Non-grammatical |
| German | 0.372 | Grammatical gender |
| Spanish | 0.293 | Grammatical gender |
| English | 0.169 | Non-grammatical |

- All five languages show a male bias in mBERT, with English the least biased.
- Dutch (non-grammatical) shows nearly the same bias as French (grammatical), suggesting grammatical gender alone does not drive mBERT male bias.
- German is a notable outlier: high model bias but low mC4 male co-occurrence ratio, suggesting morphological gender marking or cross-lingual training dynamics as confounds.

## Stack

- Python, PyTorch, HuggingFace Transformers
- Pandas, NumPy, Matplotlib, Seaborn, SciPy
- Datasets: WinoBias, mC4 (multilingual)
