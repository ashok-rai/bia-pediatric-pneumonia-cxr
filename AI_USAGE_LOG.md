# AI Usage Log

**Project:** Pediatric Pneumonia Detection in Chest X-rays · **Author:** Ashok Rai · **Last updated:** 24.11.2026
**Tools:** ChatGPT (OpenAI), GitHub Copilot, Devin AI (Cognition, partly)

## Rules I followed

- No number in the report comes from an AI tool: all results are notebook outputs in `results/`.
- Every AI suggestion was checked by running the code, reading the output, or comparing with the data set page and the Kermany et al. (2018) paper.
- Final wording, interpretation and decisions are my own.
- No patient data was shared with any AI tool (public, de-identified data set only).

## Log

| Date | Tool | Purpose | Task accomplished | How I checked it |
|---|---|---|---|---|
| 05.11.2026 | ChatGPT | Planning | Compared candidate data sets; chose Kermany 2018 chest X-rays (2D, public, CC BY 4.0) | Checked data set page, licence, size |
| 06.11.2026 | ChatGPT | Planning | Drafted the workplan: question → data → floor → baseline → CNN → critique (parts A–C) | Matched against the course template and session plan |
| 10.11.2026 | ChatGPT | Concepts | Explained transfer learning, frozen backbone, class-weighted loss | Compared with lecture slides |
| 12.11.2026–17.11.2026 | GitHub Copilot | Code | Autocompleted data loading / resizing helpers and random-forest features (histogram + 8 × 8 thumbnail) | Ran cells; image counts 5,232 / 624; RF 76.9 % above floor 62.5 % |
| 13.11.2026 | ChatGPT | Debug | Fixed Colab download/unzip path errors for `ChestXRay2017.zip` | Cell ran end-to-end; counts matched A2 |
| 14.11.2026 | GitHub Copilot | Writing | First drafts of README and report skeleton (question, five lines) | Rewrote in my own words; committed 14.11. |
| 16.11.2026 | ChatGPT | Code | Patient-ID parsing rule (personN / IM-xxxx) for leakage check A4 | Inspected file names by hand; result 161 shared IDs |
| 18.11.2026 | ChatGPT | Debug | Grad-CAM shape/hook errors on ResNet-18 | B4/B5 figures produced; sanity correlations checked |
| 19.11.2026 | ChatGPT, GitHub Copilot | Writing | Filled README blocks 1–8 and report sections 1–6, 8 from notebook outputs | Every number cross-checked with `results/` files |
| 21.11.2026 | ChatGPT | Concepts | Explained calibration (ECE), bootstrap CI, test-set peeking | Matched C2/C3 outputs; added honest notes in report section 5 |
| 24.11.2026 | Devin AI | Review | Audited the repository against the professor's checkpoint; found path mismatch, missing `requirements.txt`, empty A5 fields, empty report section 7 | Verified each finding by opening the files |

## Limits

- AI tools can be wrong; derived specificity values and the paper's numbers are marked "to verify" in the report.
