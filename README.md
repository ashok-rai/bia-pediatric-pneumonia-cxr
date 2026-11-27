# Pneumonia or normal? Classifying pediatric chest X-rays (Kermany et al., 2018)

**Biomedical Image Analysis · M.Sc. Applied Data Science and AI · SRH University Munich · WS 2026/27**
**Author:** Ashok Rai · **Last updated:** 29.11.2026 · **Report:** [report.md](report.md)

---

## 1 · My question in one sentence  *(report section 1)*

Can a CNN pretrained on ImageNet tell pneumonia from normal in pediatric chest X-rays reliably enough to help a doctor triage cases where radiologists are scarce?

## 2 · Five lines  *(report sections 1–3)*

| | |
|---|---|
| **Question** | Pneumonia vs. normal on pediatric chest X-rays, as a triage aid |
| **Images** | Kermany et al. 2018, `ChestXRay2017.zip`, Mendeley Data V2 (doi:10.17632/rscbjbr9sj.2, CC BY 4.0), downloaded 19.11.2026: 5,856 JPEGs |
| **Labels** | NORMAL / PNEUMONIA, graded by two expert physicians, evaluation set checked by a third |
| **Metric** | Sensitivity (missing pneumonia is the worst error), with specificity, precision and ROC-AUC; accuracy to compare with the paper (92.8 % acc., 93.2 % sens., 90.1 % spec., AUC 0.968) |
| **Baseline** | Floor: always "pneumonia" = 62.5 % test accuracy. Classical: random forest on histogram + 8×8 thumbnail, and on GLCM texture |

## 3 · Flat images or stacks?  *(report section 2)*

- **2D or 3D:** 2D, one frontal (anterior-posterior) chest X-ray per JPEG
- **Pixel size:** not reported (no DICOM header; image sizes vary)

## 4 · Who made the labels?  *(report section 2)*

Two expert physicians graded the images after a quality check removed unreadable scans; a third expert checked the evaluation set. Patients were children aged 1–5 at Guangzhou Women and Children's Medical Center. The label is the diagnosis from the X-ray, not confirmed by a lab test.

## 5 · Leakage check  *(report sections 2 and 5)*

1. **Several images per child?** Yes, and the official split was not by child: 170 children were in both train and test. **Fixed:** their 457 training images were dropped, and validation is split by child, so 0 children are shared between any two splits (`01_overlap.md`).
2. **Copies?** 0 near-twins between splits (mean pixel difference < 0.03 at 64 × 64).
3. **Means and augmentation after the split?** Normalisation uses the fixed ImageNet mean/std; augmentation (config C) only on training batches.
4. **Epochs and thresholds on validation only?** **Fixed:** the best epoch, the configuration and the threshold are all chosen on validation; the test set is used once, in notebook 04.
5. **Anything that gives the label away?** "R" markers, corner text and tubes are visible, and file names differ per class. Masking the image border lowers AUC from 0.943 to 0.924; the border alone gives 0.762 (`04_masking.md`).

## 6 · Progress: one turn of the cycle

- [x] 0 · Question · [x] 1 · Load · [x] 2 · Look (20 images) · [x] 3 · Count + floor · [x] 4 · Check (split by child) · [x] 5 · Data table · [x] 6 · Network next to floor and baseline

## 7 · How to run it  *(report section 4)*

- **Environment:** Python 3.11, versions in `requirements.txt`. Notebook 03 was trained on Google Colab (Tesla T4); 01, 02 and 04 ran locally. Each notebook downloads the data if it is missing.
- **Order:** `notebooks/01_patient_split_audit` → `02_baselines` → `03_cnn_finetune` → `04_evaluation_shortcuts`. Notebook 04 needs the checkpoint `data/models/03_final.pt` from notebook 03 (not in git, too large).
- **Which file feeds which report section** (all in `results/own/`, plus `splits/patient_split.csv`):

| Notebook | Files | Report section |
|---|---|---|
| 01 | `01_data_table.md`, `01_examples.png`, `01_counts.csv`, `01_overlap.md`, `01_patients_per_id.png`, `splits/patient_split.csv` | 2 · data |
| 02 | `02_baselines.md`, `02_roc.png`, `02_perm_importance.png`, `02_probs.csv` | 5 · baselines, before/after |
| 03 | `03_models.md`, `03_curves.png`, `03_final_choice.json`, `03_probs.csv` | 3 · design, 5 · results |
| 04 | `04_final_table.md`, `04_confusion.png`, `04_roc.png`, `04_bootstrap.png`, `04_calibration.png`, `04_worst.png`, `04_masking.md`, `04_masking.png` | 5 · results |
| 04 | `04_gradcam.png`, `04_sanity.png` | 6 · explainability |
| 04 | `04_summary.md` | abstract |

## 8 · Shared with my Deep Learning project?

No. My Deep Learning project is a different one (Project 6, Kim CNN).

## 9 · Use of AI tools  *(report section 7)*

Dated log: [AI_USAGE_LOG.md](AI_USAGE_LOG.md).
