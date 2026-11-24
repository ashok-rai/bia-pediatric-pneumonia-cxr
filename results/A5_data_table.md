| | |
|---|---|
| Question | Can an ImageNet-pretrained CNN tell pneumonia from normal in pediatric chest X-rays reliably enough to help triage? |
| Source, licence | Kermany et al., "Labeled Optical Coherence Tomography (OCT) and Chest X-Ray Images for Classification", Mendeley Data V2 (chest X-ray part, `ChestXRay2017.zip`): https://data.mendeley.com/datasets/rscbjbr9sj · CC BY 4.0 (to verify on the data set page) |
| Modality, size | X-ray (chest radiograph), 2D, JPEG, pixel size not reported; 5856 images, used at 128 × 128 pixels |
| Labels | 2 classes: normal, pneumonia; who decided them: expert physicians, after a quality check removed unreadable scans (diagnosis from the X-ray, not confirmed by a lab test; number of graders: to verify in the paper) |
| Classes | largest: pneumonia 74% of training; focus: pneumonia 74%; floor 62.5% |
| Splits | 4709 / 523 / 624 (training / validation / test) |
| Quality checks | 0 of 624 test images have a near-twin in training; 2685 training / 427 test patients; 161 in both |
| Where my data could differ | site: one hospital (Guangzhou Women and Children's Medical Center) · device: not reported · population: children aged 1–5 · who labelled: expert physicians reading the X-ray |
| A possible shortcut | "R" markers, corner text and tubes/electrodes (A1, C4); Grad-CAM often lights up the image edges (B4); file names follow a different pattern per class |
