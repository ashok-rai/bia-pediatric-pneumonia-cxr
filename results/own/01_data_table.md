# 01 · data table (patient-level split)

| | |
|---|---|
| Question | Can an ImageNet-pretrained CNN tell pneumonia from normal in pediatric chest X-rays reliably enough to help triage? |
| Source, licence | Kermany, Zhang, Goldbaum (2018), "Labeled Optical Coherence Tomography (OCT) and Chest X-Ray Images for Classification", Mendeley Data V2, doi:10.17632/rscbjbr9sj.2 (chest X-ray part, `ChestXRay2017.zip`) · CC BY 4.0 (checked on the data set page) |
| Modality, size | X-ray (chest radiograph, anterior-posterior), 2D, JPEG, pixel size not reported; 5856 images, used at 128 × 128 (baselines, frozen CNN) and 224 × 224 (fine-tuned CNN) |
| Labels | 2 classes: NORMAL, PNEUMONIA. Graded by two expert physicians after a quality check removed unreadable scans; a third expert checked the evaluation set (Kermany et al., 2018). Diagnosis read from the X-ray, not confirmed by a lab test |
| Classes | pneumonia share: training 71.5%, validation 73.1%, test 62.5%; floor (always pneumonia) on test 62.5% |
| Splits | by child: 4043 / 732 / 624 images (training / validation / test) from 2287 / 404 / 427 children; test = the official test folder, unchanged; 457 training images of 170 children who are also in the test set were dropped |
| Quality checks | shared children before (template, split by image) → after (split by child): train∩test 161 → 0, train∩val 297 → 0, val∩test 32 → 0; near-twins val vs train 3 → 0, test vs train 0 → 0. 161 = children in the template's training part and in test; 170 = all children of the official training folder who are in test (template training plus validation) |
| Where my data could differ | site: one hospital (Guangzhou Women and Children's Medical Center) · device and protocol: not reported · population: children aged 1–5 · labels: physicians reading the X-ray |
| A possible shortcut | "R" markers, corner text, tubes/electrodes (see `01_examples.png`); file names follow a different pattern per class (all 170 leaked children are `person*` pneumonia IDs). Tested in notebook 04 by masking the image border (`04_masking.md`) |
