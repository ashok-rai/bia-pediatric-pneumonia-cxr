# 02 · baselines on the patient-clean split

| model | trained on | threshold rule | threshold | test acc | test sens (k/n) | test spec (k/n) | test AUC | val AUC |
|---|---|---|---|---|---|---|---|---|
| floor (always PNEUMONIA) | patient train | - | - | 62.5% | 390/390 | 0/234 | 0.500 | 0.500 |
| RF-template image-split | template train (leaky) | >= 0.5 | 0.500 | 76.8% | 385/390 | 94/234 | 0.925 | 0.998 |
| RF-template image-split | template train (leaky) | val sens >= 0.95 | 0.853 | 84.1% | 317/390 | 208/234 | 0.925 | 0.998 |
| RF-template | patient train | >= 0.5 | 0.500 | 78.0% | 384/390 | 103/234 | 0.927 | 0.984 |
| RF-template | patient train | val sens >= 0.95 | 0.633 | 85.9% | 378/390 | 158/234 | 0.927 | 0.984 |
| GLCM-only | patient train | >= 0.5 | 0.500 | 77.4% | 354/390 | 129/234 | 0.846 | 0.938 |
| GLCM-only | patient train | val sens >= 0.95 | 0.333 | 72.1% | 365/390 | 85/234 | 0.846 | 0.938 |
| RF-template+GLCM | patient train | >= 0.5 | 0.500 | 79.2% | 386/390 | 108/234 | 0.927 | 0.984 |
| RF-template+GLCM | patient train | val sens >= 0.95 | 0.593 | 84.0% | 381/390 | 143/234 | 0.927 | 0.984 |