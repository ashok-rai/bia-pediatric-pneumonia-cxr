# Pediatric Pneumonia Detection in Chest X-rays

**Biomedical Image Analysis · M.Sc. Applied Data Science and AI · SRH University Munich · Winter semester 2026/27**
**Author(s):** Ashok Rai · **Repository:** https://github.com/ashok-rai/bia-pediatric-pneumonia-cxr · **Date:** 24.11.2026

---

## Abstract

I asked whether an ImageNet-pretrained CNN can tell pneumonia from normal in pediatric chest X-rays (Kermany et al., 2018), as a triage aid. On the 624 official test images, a frozen ResNet-18 with a class-weighted (balanced) last layer found 97.7 % of the pneumonia images (381/390) at 85.6 % accuracy, against a floor of 62.5 % (always "pneumonia") and 76.9 % for a random-forest baseline. Its specificity is only 65.4 % (153/234), and its probabilities are over-confident (calibration error 0.106). The main limitation is that 161 patient IDs appear in both training and test, so the numbers are likely optimistic: the result is promising, but the model is not ready for triage.

## 1 · The biomedical problem (15 %, with section 2)

- **Clinical question:** Can a model flag pediatric chest X-rays that show pneumonia, so a doctor can prioritise (triage) them, especially where radiologists are scarce?
- **Task type:** Binary image classification. Input: one 2D chest X-ray. Output: pneumonia or normal.
- **Why it is hard:** Class imbalance (more pneumonia than normal images). Signs of pneumonia can be subtle and overlap with other findings. Images vary in quality and size.

## 2 · The data (15 %, with section 1)

| | |
|---|---|
| Source, version, download date | Kermany et al., "Labeled Optical Coherence Tomography (OCT) and Chest X-Ray Images for Classification", Mendeley Data, V2: https://data.mendeley.com/datasets/rscbjbr9sj (chest X-ray part, `ChestXRay2017.zip`). Paper: Kermany et al., Cell 172(5), 2018. Downloaded 19.11.2026 |
| Licence | CC BY 4.0 (to verify on the data set page): use and sharing allowed with attribution |
| Modality | X-ray (chest radiograph), 2D |
| Size | 5,856 JPEG images (5,232 train / 624 test). Patients (from the file names): 2,685 in my training part, 427 in test. Pixel size: not reported. Images used at 128 × 128 |
| Labels: who made them | Expert physicians graded the images after a quality check removed unreadable scans. The label is the physicians' diagnosis from the X-ray, not confirmed by a lab test. Bacterial or viral is only given in the file names |
| Labels: agreement | Not reported in the data files (number of graders per image: to verify in the paper's Methods section) |
| Classes or targets | NORMAL / PNEUMONIA. Training 1,218 / 3,491 (≈26 % / 74 %), validation 131 / 392, test 234 / 390 |
| Splits | The official train folder (5,232) is split at random into 4,709 training + 523 validation images (10 %, seed 0). Official test folder: 624. The split is by image, **not by patient** |
| Preprocessing | JPEG → RGB, resized to 128 × 128 (bilinear; aspect ratio not kept). For ResNet-18: upsampled to 224 × 224 and normalised with the ImageNet mean/std. No augmentation |
| Quality checks | A1: 20 training images looked at by eye; "R" markers, corner text and tubes/electrodes are visible in some. A3: 0 of 624 test images have a near-twin in training (mean pixel difference < 0.03 at 64 × 64). A4: 161 patient IDs in both training and test, 297 in both training and validation (the IM-xxxx rule for normal images is my assumption; how the 161 split into personN vs IM-xxxx: to check) |
| Shared with Deep Learning? | No. My Deep Learning project is a different one (Project 6, Kim CNN) |

Figure of typical images: `results/A1_examples.png`.

## 3 · Experimental design (15 %)

- **The floor:** Always say "pneumonia" (the largest class in training): 62.5 % test accuracy, 100 % sensitivity, 0 % specificity.
- **Classical baseline:** Random forest (300 trees, random_state 0) on a 48-value intensity histogram (16 bins × 3 identical RGB channels) plus an 8 × 8 thumbnail. No GLCM texture features yet.
- **Deep-learning model:** ResNet-18 pretrained on ImageNet, frozen; only a new linear last layer (512 → 2) is trained. Adam, learning rate 1e-3, batch size 64, 10 epochs; the prediction is the class with the highest probability (argmax). Two versions: plain, and balanced (class-weighted loss). Balanced is used from here on.
- **Augmentation:** None.
- **Comparisons:** Floor vs. random forest vs. ResNet-18 plain vs. ResNet-18 balanced, all on the same 624 test images. Balanced is also trained with 3 seeds.

## 4 · Implementation and reproducibility (25 %)

- **Run it:** Google Colab, one notebook: `notebooks/BIA_W6_Project_Latest.ipynb` (download cell → YOUR DATA cell → Runtime → Run all). Versions in `requirements.txt`: numpy 2.4.6, torch 2.14.1, torchvision 0.29.1, scikit-learn 1.6.1, plus matplotlib, Pillow, requests.
- **Seeds, hardware, training time:** Seeds 0, 1, 2 for the linear last layer; validation split seed 0; random forest random_state 0. Hardware: Google Colab, Tesla T4 GPU. Training time: not measured (I do not know yet).
- **Where the results come from:** All numbers and figures come from the notebook outputs and the files in `results/` (written by the notebook; which file feeds which section is listed in README block 7).

## 5 · Evaluation, validation and critical analysis (15 %)

| Setting | Accuracy | Sensitivity | Specificity (derived unless noted) | seeds |
|---|---|---|---|---|
| floor: always "pneumonia" | 62.5 % | 100 % | 0 % | – |
| random forest (histogram + thumbnail) | 76.9 % | 98.5 % | ≈41 % (derived) | 1 (random_state 0) |
| ResNet-18 frozen, plain | 82.4 % | 98.5 % | ≈56 % (derived) | 1 (seed 0) |
| ResNet-18 frozen, balanced | 85.6 % (95 % CI 82.9–88.3 %) | 97.7 % = 381/390 (95 % CI 96.1–99.0 %) | 65.4 % = 153/234 (from B2_confusion.png) | 1 (seed 0) |
| ResNet-18 frozen, balanced, 3 seeds | 84.9 % ± 0.9 % | 97.8 % ± 0.4 % | ≈63 % ± 3 % (derived from C1_seeds.json) | 3 (0, 1, 2) |
| Kermany et al. 2018 (paper) | 92.8 % | 93.2 % | 90.1 % | – (to verify against the paper) |

Derived specificity = (accuracy × 624 − pneumonia found) / 234 normal test images. CIs: 2,000 bootstrap test sets (C2). ±: standard deviation over 3 seeds (C1).

- **Metrics that fit the task:** Sensitivity matters most, since missing pneumonia is the worst error. But on its own it is misleading: the floor reaches 100 % sensitivity and is useless. So I report specificity next to it, and accuracy to compare with the paper. ROC-AUC: not computed yet (to add).
- **Worst cases:** The 8 most confident mistakes (C4) are all normal images called pneumonia with p = 0.99–1.00. Several show an "R" marker and corner text, which fits the shortcut idea in README block 5.
- **Calibration:** Calibration error (ECE) for pneumonia: 0.106. The curve lies below the diagonal (C3): when the model says pneumonia with high probability, it is right less often than that. It is over-confident.
- **Ceiling:** The paper reports 92.8 % accuracy, 93.2 % sensitivity and 90.1 % specificity (to verify against the paper). My model is higher on sensitivity but far lower on specificity. Likely reasons: frozen ImageNet features, 128-pixel input, no fine-tuning.
- **Test set:** Honest note: I chose "balanced" over "plain" by looking at the test numbers (B3). That is test-set peeking. The validation set is not used (fixed 10 epochs, argmax threshold). External data: none.
- **Limitations:** Data from a single hospital and children aged 1–5 only, so the results may not carry over to other hospitals or adults. 161 patient IDs are in both training and test, so the test numbers are likely optimistic. The validation set is unused and not split by patient either (297 shared IDs). Resizing to 128 × 128 distorts the aspect ratio.

## 6 · Explainability, ethics and clinical responsibility (5 %)

- **Sanity check (B5):** With a random last layer, the Grad-CAM maps change completely. Correlation between trained and random maps: -0.48 -0.59 -0.05 -0.57 -0.49 -0.38 -0.40 -0.00. So the maps depend on the learned layer (check passed). The values are negative likely because a random 2-class layer points roughly the opposite way.
- **A map I would show (B4):** A correctly found pneumonia, p = 1.00 (2nd column): the hot spot lies over the upper lung.
- **A map I would not trust (B4):** The false alarm with p = 0.84: it lights up the top edge and the shoulders, outside the lungs. The missed cases also light up the image edges. Grad-CAM shows where the score reacts, not why, so it cannot prove that the model uses real signs of pneumonia.
- **Harm and responsibility:** A missed pneumonia can delay treatment for a child. With 65.4 % specificity, about 1 in 3 normal children would be flagged, which means extra work and worry. A doctor must still read every image. The data are pediatric and de-identified; I only use the public release.

## 7 · Use of AI tools (5 %)

I used ChatGPT for planning the workplan, explaining concepts (transfer learning, calibration, bootstrap) and debugging (Colab download, Grad-CAM hooks); GitHub Copilot for code completion and first drafts of README and report text; and Devin AI for auditing the repository against the checkpoint and preparing the submission. No result comes from an AI tool: all numbers are notebook outputs in `results/`, and I checked every suggestion by running it, reading the output, or comparing with the data source and the paper. Dated log: `AI_USAGE_LOG.md`.

## 8 · Conclusion (documentation and communication, 5 %)

A frozen ResNet-18 (balanced) finds 97.7 % of pneumonia images but only 65.4 % of normal ones, with patient overlap between training and test. This is promising, but not ready for triage. Next steps:

1. Split training, validation and test by patient.
2. Choose the model on the validation set, not the test set.
3. Report the exact specificity and the ROC-AUC.
4. Fine-tune the network instead of freezing it, at a higher resolution.
5. Add GLCM texture features to the classical baseline.
6. Crop or mask the image borders to test the shortcut idea.
7. Check the 161 overlapping IDs (personN vs IM-xxxx).

## References

1. Kermany, D. S., et al. (2018). Identifying Medical Diagnoses and Treatable Diseases by Image-Based Deep Learning. *Cell*, 172(5), 1122–1131.
2. Kermany, D., Zhang, K., Goldbaum, M. (2018). Labeled Optical Coherence Tomography (OCT) and Chest X-Ray Images for Classification. Mendeley Data, V2. https://data.mendeley.com/datasets/rscbjbr9sj
