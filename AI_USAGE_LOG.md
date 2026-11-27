# AI Usage Log

**Project:** Pediatric Pneumonia Detection in Chest X-rays · **Author:** Ashok Rai · **Last updated:** 27.11.2026
**Tools:** ChatGPT (OpenAI), GitHub Copilot, Devin AI (Cognition)

## Rules I followed

- No number in the report comes from an AI tool: all results are notebook outputs in `results/own/`.
- Every AI suggestion was checked by running the code, reading the output, or comparing with the data set page and the Kermany et al. (2018) paper.
- Final wording, interpretation and decisions are my own.
- No patient data was shared with any AI tool (public, de-identified data set only).

## Log

| Date | Tool | Purpose | Task accomplished | How I checked it |
|---|---|---|---|---|
| 05.11.2026 | ChatGPT | Planning | Compared candidate data sets; chose Kermany 2018 chest X-rays (2D, public, CC BY 4.0) | Checked data set page, licence, size |
| 06.11.2026 | ChatGPT | Planning | Drafted the workplan: question → data → floor → baseline → CNN → critique | Matched against the course template and session plan |
| 10.11.2026 | ChatGPT | Concepts | Explained transfer learning, frozen backbone, class-weighted loss | Compared with lecture slides |
| 12.11.2026–17.11.2026 | GitHub Copilot | Code | Autocompleted data loading / resizing helpers and random-forest features (histogram + 8 × 8 thumbnail) | Ran cells; image counts 5,232 / 624; RF 76.9 % above floor 62.5 % |
| 13.11.2026 | ChatGPT | Debug | Fixed Colab download/unzip path errors for `ChestXRay2017.zip` | Cell ran end-to-end; counts matched |
| 14.11.2026 | GitHub Copilot | Writing | First drafts of README and report skeleton | Rewrote in my own words |
| 16.11.2026 | ChatGPT | Code | Patient-ID parsing rule (personN / IM-xxxx) for the leakage check | Inspected file names by hand; result 161 shared IDs |
| 18.11.2026 | ChatGPT | Debug | Grad-CAM shape/hook errors on ResNet-18 | Figures produced; sanity correlations checked |
| 19.11.2026 | ChatGPT, GitHub Copilot | Writing | Filled README and report sections from notebook outputs | Every number cross-checked with `results/` files |
| 21.11.2026 | ChatGPT | Concepts | Explained calibration (ECE), bootstrap CI, test-set peeking | Matched outputs; added honest notes in report section 5 |
| 24.11.2026 | Devin AI | Review | Audited the repository against the professor's checkpoint (paths, `requirements.txt`, data table, report section 7) | Verified each finding by opening the files |
| 24.11.2026–26.11.2026 | ChatGPT, GitHub Copilot, Devin AI | Code, debug | Notebooks 01–04 after the feedback: split by child, baselines + GLCM, frozen vs. fine-tuned ResNet-18 chosen on validation, final test evaluation with masking test | Asserts in 01 (0 shared children, 170 children / 457 images dropped); 04 reproduces 03's probabilities (max difference 0.00005) |
| 27.11.2026 | Devin AI | Code, writing | Precision/recall in 04, permutation importance for the forest in 02, data table and example figure in 01; updated report and README to the new results | Re-ran 01, 02, 04; split file checksum unchanged; every report number matched to a `results/own/` file; licence checked on the Mendeley page |
