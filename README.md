# Pneumonia or normal? Classifying pediatric chest X-rays (Kermany et al., 2018)

**Biomedical Image Analysis · M.Sc. Applied Data Science and AI · SRH University Munich · WS 2026/27**
**Author:** Ashok Rai · **Last updated:** 24.11.2026

---

## 1 · My question in one sentence  *(Session 12 · report section 1)*

Can a CNN pretrained on ImageNet (transfer learning) tell pneumonia from normal in pediatric chest X-rays reliably enough to help a doctor triage (prioritise) cases where radiologists are scarce?

## 2 · Five lines  *(Session 6 · report sections 1–3)*

| | |
|---|---|
| **Question** | Pneumonia vs. normal on pediatric chest X-rays, as a triage aid |
| **Images** | Kermany et al. 2018, "ChestXRay2017" from Mendeley Data V2 (https://data.mendeley.com/datasets/rscbjbr9sj), downloaded 19.11.2026: 5,856 JPEGs, 5,232 train / 624 test |
| **Labels** | One class per image: NORMAL / PNEUMONIA (file names also say bacterial or viral) |
| **Metric** | Sensitivity (missing pneumonia is the worst error), specificity, ROC-AUC. Also accuracy, to compare with the paper (92.8 % acc., 93.2 % sens., 90.1 % spec., AUC 96.8 % — to verify against the paper) |
| **Baseline** | Floor: always "pneumonia" = 390/624 ≈ 62.5 % test accuracy (sensitivity 100 %, specificity 0 %). Classical: intensity histogram + 8×8 thumbnail + random forest; texture features (GLCM) are still planned |

## 3 · Flat images or stacks?  *(Session 10 · report section 2)*

- **2D or 3D:** 2D, one frontal (anterior-posterior) chest X-ray per JPEG file
- **Pixel or voxel size:** Not reported (JPEGs have no DICOM header; image sizes vary)
- **3D only:** Not applicable

## 4 · Who made the labels?  *(Session 11 · report section 2)*

1. **Who:** Expert physicians graded the images after a quality check removed unreadable scans. Patients were children aged 1–5 at Guangzhou Women and Children's Medical Center.
2. **How many:** The number of graders per image is not reported in the data files. The paper describes grading by expert physicians (to verify in the paper's Methods section).
3. **What it means:** The label is the physicians' diagnosis from the X-ray, not confirmed by a lab test. Bacterial or viral is only given in the file names.

## 5 · Leakage check  *(Session 7 · report sections 2 and 5)*

1. **Several images per patient?** Yes. I read the patient ID from the file name: "personN" for pneumonia, "IM-xxxx" / "NORMAL2-IM-xxxx" for normal (the IM rule is my assumption). 161 patient IDs are in both training and test, and 297 in both training and validation, because the split is by image, not by patient.
2. **Copies?** 0 of 624 test images have a near-twin in training (mean pixel difference < 0.03 at 64 × 64).
3. **Means and augmentation after the split?** No augmentation. Normalisation uses the fixed ImageNet mean/std, not values computed from my data, so nothing leaks.
4. **Epochs and thresholds on validation only?** No. The validation set is not used: 10 epochs and the argmax threshold are fixed, and I chose "balanced" over "plain" by looking at the test numbers (B3).
5. **Anything that gives the label away?** Possibly: "R" markers, corner text and tubes/electrodes (A1, C4); Grad-CAM often lights up the image edges (B4); the file names follow a different pattern per class.

## 6 · Progress: one turn of the cycle  *(Session 12)*

- [x] 0 · Question: one sentence (block 1)
- [x] 1 · Load: my data downloads in Colab
- [x] 2 · Look: 20 images with their labels, looked at by eye
- [x] 3 · Count: images per class or share of foreground pixels; the floor
- [x] 4 · Check: twins, the same patient twice (block 5)
- [x] 5 · Table: the data table in report section 2 is filled in
- [x] 6 · Number: a first network next to the floor and the classical baseline *(after 19.11.)*

## 7 · How to run it  *(report section 4)*

- **Environment:** Google Colab with a Tesla T4 GPU. Python 3, PyTorch + torchvision. Versions in `requirements.txt`: numpy 2.4.6, torch 2.14.1, torchvision 0.29.1, scikit-learn 1.6.1, plus matplotlib, Pillow, requests.
- **Order:** One notebook, `notebooks/BIA_W6_Project_Latest.ipynb`: run the download cell (Mendeley zip), check the YOUR DATA cell, then Runtime → Run all.
- **Which file makes which table or figure:** The notebook writes its files to `results/` (repository root).
  - `A1_examples.png` → report section 2, figure of typical images
  - `A2_counts.csv`, `A5_data_table.md` → report section 2, data table
  - `B2_confusion.png`, `B3_numbers.md`, `C1_seeds.json`, `C2_bootstrap.png` → report section 5, results table
  - `C3_calibration.png`, `C4_worst.png` → report section 5, calibration and worst cases
  - `B4_gradcam.png`, `B5_sanity.png` → report section 6, heat maps
  - `C5_summary.md` → report abstract

## 8 · Shared with my Deep Learning project?

No. My Deep Learning project is a different one (Project 6, Kim CNN).

## 9 · Use of AI tools  *(report section 7)*

Dated log of how I used ChatGPT, GitHub Copilot and Devin AI: `AI_USAGE_LOG.md`.