# Pneumonia or normal? Classifying pediatric chest X-rays (Kermany et al., 2018)

**Biomedical Image Analysis · M.Sc. Applied Data Science and AI · SRH University Munich · WS 2026/27**
**Author:** Ashok Rai · **Last updated:** 14.11.2026

---

## 1 · My question in one sentence  *(Session 12 · report section 1)*

Can a CNN pretrained on ImageNet (transfer learning) tell pneumonia from normal in pediatric chest X-rays reliably enough to help a doctor triage (prioritise) cases where radiologists are scarce?

## 2 · Five lines  *(Session 6 · report sections 1–3)*

| | |
|---|---|
| **Question** | Pneumonia vs. normal on pediatric chest X-rays, as a triage aid |
| **Images** | Kermany et al. 2018, "ChestXRay2017" from Mendeley Data (https://data.mendeley.com/datasets/rscbjbr9sj): 5,856 JPEGs, 5,232 train / 624 test |
| **Labels** | One class per image: NORMAL / PNEUMONIA (file names also say bacterial or viral) |
| **Metric** | Sensitivity (missing pneumonia is the worst error), specificity, ROC-AUC. Also accuracy, to compare with the paper (92.8 % acc., 93.2 % sens., 90.1 % spec., AUC 96.8 % — to verify against the paper) |
| **Baseline** | Floor: always "pneumonia" = 390/624 ≈ 62.5 % test accuracy (sensitivity 100 %, specificity 0 %). Classical: intensity histogram + texture features (GLCM) with a random forest |

## 3 · Flat images or stacks?  *(Session 10 · report section 2)*

- **2D or 3D:** 2D, one frontal (anterior-posterior) chest X-ray per JPEG file
- **Pixel or voxel size:** Not reported (JPEGs have no DICOM header; image sizes vary)
- **3D only:** Not applicable

## 4 · Who made the labels?  *(Session 11 · report section 2)*

1. **Who:** Expert physicians graded the images after a quality check removed unreadable scans. Patients were children aged 1–5 at Guangzhou Women and Children's Medical Center.
2. **How many:** I do not know yet
3. **What it means:** I do not know yet

## 5 · Leakage check  *(Session 7 · report sections 2 and 5)*

1. **Several images per patient?** I do not know yet
2. **Copies?** I do not know yet
3. **Means and augmentation after the split?** I do not know yet
4. **Epochs and thresholds on validation only?** I do not know yet
5. **Anything that gives the label away?** I do not know yet

## 6 · Progress: one turn of the cycle  *(Session 12)*

- [x] 0 · Question: one sentence (block 1)
- [ ] 1 · Load: my data downloads in Colab
- [ ] 2 · Look: 20 images with their labels, looked at by eye
- [ ] 3 · Count: images per class or share of foreground pixels; the floor
- [ ] 4 · Check: twins, the same patient twice (block 5)
- [ ] 5 · Table: the data table in report section 2 is filled in
- [ ] 6 · Number: a first network next to the floor and the classical baseline *(after 19.11.)*

## 7 · How to run it  *(report section 4)*

- **Environment:** Google Colab (GPU) for training. Python 3, PyTorch + torchvision. `requirements.txt` will be added.
- **Order:** I do not know yet. Planned: `01_load_and_look.ipynb` → `02_counts_and_leakage.ipynb` → `03_baseline.ipynb` → `04_cnn.ipynb`
- **Which file makes which table or figure:** I do not know yet. I will fill this in once the notebooks exist.

## 8 · Shared with my Deep Learning project?

No. My Deep Learning project is a different one (Project 6, Kim CNN).