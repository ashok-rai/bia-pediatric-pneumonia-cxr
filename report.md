# Pediatric Pneumonia Detection in Chest X-rays

**Biomedical Image Analysis · M.Sc. Applied Data Science and AI · SRH University Munich · Winter semester 2026/27**
**Author(s):** Ashok Rai · **Repository:** https://github.com/ashok-rai/bia-pediatric-pneumonia-cxr · **Date:** 14.11.2026

---

## Abstract

Work in progress. The question is whether pediatric chest X-rays can be classified as pneumonia or normal, using the Kermany et al. (2018) data set. Baseline, model and results: I do not know yet.

## 1 · The biomedical problem (15 %, with section 2)

- **Clinical question:** Can a model flag pediatric chest X-rays that show pneumonia, so a doctor can prioritise (triage) them, especially where radiologists are scarce?
- **Task type:** Binary image classification. Input: one 2D chest X-ray. Output: pneumonia or normal.
- **Why it is hard:** Class imbalance (more pneumonia than normal images). Signs of pneumonia can be subtle and overlap with other findings. Images vary in quality and size.

## 2 · The data (15 %, with section 1)

| | |
|---|---|
| Source, version, download date | Kermany et al., "Labeled Optical Coherence Tomography (OCT) and Chest X-Ray Images for Classification", Mendeley Data, V2: https://data.mendeley.com/datasets/rscbjbr9sj (chest X-ray part, `ChestXRay2017`). Paper: Kermany et al., Cell 172(5), 2018. Download date: I do not know yet |
| Licence | CC BY 4.0 (to verify on the data set page): use and sharing allowed with attribution |
| Modality | X-ray (chest radiograph), 2D |
| Size | 5,856 images (5,232 train / 624 test). Number of patients: I do not know yet. Pixel size: not reported |
| Labels: who made them | Expert physicians graded the images after a quality check removed unreadable scans |
| Labels: agreement | I do not know yet |
| Classes or targets | NORMAL / PNEUMONIA. Counts per class: I do not know yet |
| Splits | Official train / test folders. Whether the split is by patient: I do not know yet |
| Preprocessing | I do not know yet |
| Quality checks | Not done yet |
| Shared with Deep Learning? | No. My Deep Learning project is a different one (Project 6, Kim CNN) |

Figure of typical images: not done yet.

## 3 · Experimental design (15 %)

- **The floor:** I do not know yet
- **Classical baseline:** I do not know yet
- **Deep-learning model:** I do not know yet
- **Augmentation:** I do not know yet
- **Comparisons:** I do not know yet

## 4 · Implementation and reproducibility (25 %)

- **Run it:** I do not know yet. Planned: Google Colab, Python 3, PyTorch, with a `requirements.txt`
- **Seeds, hardware, training time:** I do not know yet
- **Where the results come from:** I do not know yet

## 5 · Evaluation, validation and critical analysis (15 %)

| Setting | [metric] mean | ± spread | seeds |
|---|---|---|---|
| floor | not done yet | | |
| classical baseline | not done yet | | |
| deep-learning model | not done yet | | |
| + [change] | | | |

- **Metrics that fit the task:** Planned: sensitivity, specificity, ROC-AUC
- **Worst cases:** Not done yet
- **Ceiling:** I do not know yet
- **Test set:** used **once**, for the final models only. External data: none planned.
- **Limitations:** I do not know yet. Data from a single hospital and children only, so the results may not carry over to other hospitals or adults.

## 6 · Explainability, ethics and clinical responsibility (5 %)

- [Saliency maps or other explanations (Session 14), and what they can and cannot show]
- [Who could be harmed by a wrong answer; what a doctor would still have to check; privacy of the data]

## 7 · Use of AI tools (5 %)

[Which tools you used, for what (code, text, debugging), and how you checked their output. Be specific.]

## 8 · Conclusion (documentation and communication, 5 %)

Work in progress. Next steps: load the data, look at 20 images, count classes, check for patient overlap.

## References

1. Kermany, D. S., et al. (2018). Identifying Medical Diagnoses and Treatable Diseases by Image-Based Deep Learning. *Cell*, 172(5), 1122–1131.
2. Kermany, D., Zhang, K., Goldbaum, M. (2018). Labeled Optical Coherence Tomography (OCT) and Chest X-Ray Images for Classification. Mendeley Data, V2. https://data.mendeley.com/datasets/rscbjbr9sj