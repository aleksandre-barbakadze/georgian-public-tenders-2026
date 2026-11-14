# Georgian Public Tenders 2026: Valuation, Insurance and Audit

A repeatable Python pipeline that turns raw Georgian public procurement data into a clean, categorized dataset and a dashboard, with an AI cross-check of the filtering rules.

**Data:** real public data. 24,840 tenders announced between 1 Jan and 27 Oct 2026, from [tendermonitor.ge](https://tendermonitor.ge) (Transparency International Georgia). The source data is in Georgian.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/aleksandre-barbakadze/georgian-public-tenders-2026/blob/main/tender_analysis.ipynb)

## Why
Public procurement data is large and raw. Finding tenders in a specific niche and understanding competition and prices takes a lot of manual filtering. This project makes that process systematic and repeatable.

## Pipeline
New data file → filter → clean → manual corrections → calculations → risk flags → AI cross-check → export for the dashboard.

A full run, including the AI check, takes about 5 minutes with one "Run all".

## Category rules
1. **Property & asset valuation:** keyword rules on the tender description.
2. **Insurance:** main CPV code starting with 665.
3. **Audit & accounting:** CPV 79200000 (including inventory services), excluding valuation tenders and ISO / SWIFT / certificate-of-origin audits.

Failed tenders are excluded from the analysis and counted separately. Money and winners are counted only from signed contracts, in GEL.

## AI cross-check
The rule-based filter was cross-checked with Gemini (built into Google Colab) on 252 tenders:
- 93% agreement with the rule-based filter;
- the 17 differences were reviewed by hand: AI found 5 valuation tenders the rules missed and was wrong in 8 cases;
- conclusion: CPV rules for strict criteria, AI for the meaning of descriptions, a human for the differences.

AI answers may vary slightly between runs.

## Key results
| Category | Tenders | Failed | Signed contracts | Contract value (GEL) | Avg. price drop | Single bidder |
|---|---|---|---|---|---|---|
| Property valuation | 27 | 7 (26%) | 18 | ~0.52 m | 24.6% | 50% |
| Insurance | 74 | 11 (15%) | 54 | ~32.7 m | 4.6% | 61% |
| Audit & accounting | 71 | 12 (17%) | 48 | ~2.17 m | 18.8% | 50% |

- With a single bidder the average price drop was **1.9%**; with two or more bidders it was **22.7%**.
- In insurance, 3 companies won about 88% of contract value.

## Risk flags
Single bidder, repeated buyer–supplier pair (2+ contracts), price drop under 5%. A flag is a signal for review, not proof of a violation.

## Limitations
- Recently announced tenders may not have a signed contract yet.
- No loss-adjusting tenders were found in 2026.
- The dashboard is updated manually.
- To run the notebook, download the data file from tendermonitor.ge (the data file is not stored in this repository).

## Author
Aleksandre (Alex) Barbakadze · [Portfolio](https://aleksandre-barbakadze.notion.site/Hey-I-am-Aleksandre-Barbakadze-31513f1fef3a80f9b020e025ae6df360) · [LinkedIn](https://www.linkedin.com/in/aleksandre-barbakadze/)
