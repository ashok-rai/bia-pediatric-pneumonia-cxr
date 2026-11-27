# 04 · final comparison (test = 624 official images, untouched)

| model | split | threshold chosen on | threshold | test acc | precision | recall = sens (k/n) | spec (k/n) | test AUC |
|---|---|---|---|---|---|---|---|---|
| floor: always pneumonia | patient | - | - | 62.5% | 62.5% | 390/390 | 0/234 | 0.500 |
| template ResNet-18 frozen balanced | image split (leaky) | test (argmax) - quoted | 0.500 | 85.6% | 82.5% | 381/390 | 153/234 | - |
| 02 RF-template | patient | val (sens>=0.95) | 0.633 | 85.9% | 83.3% | 378/390 | 158/234 | 0.927 |
| 03 frozen A (seed 0) | patient | val (sens>=0.95) | 0.700 | 85.7% | 82.9% | 379/390 | 156/234 | 0.954 |
| 03 finetuned B = FINAL | patient | val (sens>=0.95) | 0.996 | 88.5% | 86.0% | 380/390 | 172/234 | 0.943 (95% CI 0.922-0.961) |
| Kermany et al. 2018 | own test (paper, to verify) | paper | - | 92.8% | - | 93.2% | 90.1% | 0.968 |