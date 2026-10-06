**Quadruple Aspect-Based Sentiment Analysis (Quad-ABSA) for Saudi Hospitality Dataset**

This repository contains data and scripts used in the study of quadruple aspect-based sentiment analysis (Quad-ABSA) for customer reviews in the Saudi hospitality sector. The data were collected from Booking.com between September 6th, 2019, and September 6th, 2022, focusing on reviews of accommodations in Saudi Arabia. The aim of this project is to provide a comprehensive dataset that captures customer sentiments, aspects, opinions, and targets to drive actionable insights for the hospitality industry.

**Versions**

This dataset is versioned. Corrections and additions are released as a new version in a new folder. Earlier versions are never edited, so any result computed on them can still be reproduced. Each version is also marked with a git tag (see the repository's *Releases* / *Tags*).

| Version | Folder | Reviews | Quadruples | Status | Used in |
|---|---|---:|---:|---|---|
| v1.0 | `Data V1.0/` | 231 | 1,000 | Frozen | Alharbi et al., WISE 2024 |
| v1.1 | `Data V1.1/` | 231 | 1,000 | **Current, recommended** | Ongoing PhD work |
| — | `archived/` | 240 | 1,040 | Archived interim export (25/10/2024) | — |

- **New work should use v1.1.** It corrects annotation errors found in v1.0. Every change is listed by review ID in `Data V1.1/CHANGELOG.md`.
- **To reproduce the WISE 2024 results, use v1.0.**
- **When citing, name the version you used**, e.g. "QuadABSA-Tourism v1.1".

**Repository layout**

| Path | Contents |
|---|---|
| `Data V1.0/` | The original train / dev / test splits, as published with the WISE 2024 paper. |
| `Data V1.0/Dataset with Promts/P4.jsonl` | The v1.0 data formatted as instruction prompts for LLM fine-tuning. |
| `Data V1.1/quads.csv` | The corrected dataset, one row per quadruple. |
| `Data V1.1/CHANGELOG.md` | Every correction from v1.0 to v1.1, with the decisions behind them. |
| `Data V1.1/splits/` | Train / dev / test in ACOS format, `categories.json`, and `SPLIT_REPORT.md`. |
| `archived/QuadABSA-TourismDataset - 25102024.csv` | An interim export from 25 October 2024, with 9 reviews added after the paper's snapshot. It is kept for transparency and has not been corrected. |

**What changed in v1.1**

The full list is in `Data V1.1/CHANGELOG.md`. In summary:

- Aspect and opinion spans now match the review text exactly, including the reviewers' own spelling (e.g. `worest`, `elevetors` → as written). Extraction models are scored on exact spans, so a span "corrected" away from the source text can never be matched.
- Placeholder `-` for an implicit opinion is unified with `null`.
- Missing categories were filled in, and the label `Nuetral` is spelled `Neutral`.
- `Room-related` is now `Room`. Three categories with very few examples are kept as their own labels: `Bathroom`, `Sales and marketing`, `Security`. v1.1 has 17 categories in total (listed in `splits/categories.json`).
- The v1.1 splits are grouped by review text, so no review appears in more than one split (seed 42; see `splits/SPLIT_REPORT.md`).
- Duplicate review texts are flagged in a `duplicate_of` column rather than deleted.

**Split format (v1.1)**

One review per line: `text####[[aspect, category, sentiment, opinion], ...]`. The bracketed part can be parsed with Python's `ast.literal_eval`. `NULL` marks an implicit aspect or opinion, meaning one not stated in the text.

| Split | Reviews | Quadruples |
|---|---:|---:|
| train | 157 | 677 |
| dev | 23 | 108 |
| test | 44 | 215 |

**Data Overview**

The full corpus consists of 357,583 reviews scraped from Booking.com using an automated script developed by the primary author. These reviews come exclusively from customers who have booked and checked out from accommodations, ensuring that the feedback is authentic and credible.

The annotated subset contains 1,000 quadruples (aspect, category, sentiment, opinion) from 231 randomly chosen reviews, an average of 4.33 quadruples per review. *(The WISE 2024 paper reports 1,001 quadruples. This is a typographical error: every published percentage works out exactly at n = 1,000.)* These quadruples provide insight into various facets of hospitality experiences, including customer satisfaction, preferences, and areas for improvement.

**Data Annotation Process**

The annotation process was conducted by the primary author (with a background in tourism and hospitality) and an expert from the hospitality industry in Saudi Arabia. The reviews were annotated following the detailed guidelines provided by Zhang et al. (2021) to address implicit aspects and opinions.

To ensure consistency and accuracy in labelling:

Implicit aspects and opinions were identified and annotated, even when not explicitly mentioned in the text but inferred from context.
Inter-annotator agreements, spot checks, and feedback sessions were employed to maintain high-quality annotations.
Regular training updates were provided to improve annotation accuracy.

**Categories of Aspects and Sentiments**

The dataset encompasses a diverse range of aspect categories relevant to hospitality operations (v1.1 distribution, n = 1,000):

Amenities (23.1%)
Human Resources (15.5%)
General (12.9%)
Room (8.4%)
Food and Beverage (8.2%)
Housekeeping (7.0%)
Location (6.0%)
Furniture (4.5%)
Engineering (4.4%)
Value (3.7%)
Front Office (2.4%)
Room Services (2.0%)
Lounge (1.0%)
Reservations (0.3%)
Bathroom (0.3%)
Sales and Marketing (0.2%)
Security (0.1%)

In terms of sentiment distribution at the **review** level (as reported in the paper):

- Negative sentiment accounts for 48.1%.
- Positive sentiment makes up 41.8%.
- Neutral sentiment constitutes 10.1%.

At the **quadruple** level (v1.1), which is the label models are trained and evaluated on: 537 negative, 452 positive, 11 neutral.

**Notable Observations** 

Several unique patterns were observed during the annotation process:
- Instances where a single aspect was linked to a single opinion.
- Cases where multiple aspects were associated with a single opinion.
- Scenarios where multiple aspects corresponded to multiple opinions.
- These insights contribute to understanding the complex feedback customers provide in reviews, making this dataset valuable for improving customer satisfaction strategies in the hospitality industry.

**Citation**

If you use this dataset or the scripts in your research, please cite the paper below and state which dataset version you used:

Alharbi, Marwah, Jiao Yin, Yuan Miao, and Jinli Cao. "From Data to Insights: Constructing and Evaluating a Hospitality Dataset for Quadruple Aspect-Based Sentiment Analysis." Proceedings of the International Conference on Web Information Systems Engineering (WISE 2024), pp. 102–113, Singapore: Springer Nature Singapore, November 2024.

Or in BibTeX format:

@inproceedings{alharbi2024data,
  title={From Data to Insights: Constructing and Evaluating a Hospitality Dataset for Quadruple Aspect-Based Sentiment Analysis},
  author={Alharbi, Marwah and Yin, Jiao and Miao, Yuan and Cao, Jinli},
  booktitle={Proceedings of the International Conference on Web Information Systems Engineering (WISE 2024)},
  pages={102--113},
  year={2024},
  organization={Springer},
  address={Singapore},
  publisher={Springer Nature Singapore}
}


**Contact**

For further inquiries or collaboration, please contact Marwah Alharbi at [Marwah.Alharbi@live.vu.edu.au OR MarwahAlharbi@gmail.com].
