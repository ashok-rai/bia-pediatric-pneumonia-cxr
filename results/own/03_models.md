# 03 · CNN on the patient-clean split

reference: template frozen balanced (image split, argmax): 85.6 % acc, 381/390, 153/234

| config | seeds | threshold rule | threshold (seed 0) | test acc | test sens (k/n) | test spec (k/n) | test AUC (seed 0) | test AUC mean +/- sd | val AUC mean | train time/run |
|---|---|---|---|---|---|---|---|---|---|---|
| frozen (A) | 3 | >= 0.5 | 0.500 | 83.2% | 384/390 | 135/234 | 0.954 | 0.954 +/- 0.000 | 0.994 | 1s |
| frozen (A) | 3 | val sens >= 0.95 | 0.700 | 85.7% | 379/390 | 156/234 | 0.954 | 0.954 +/- 0.000 | 0.994 | 1s |
| finetuned (B) | 1 | >= 0.5 | 0.500 | 77.6% | 390/390 | 94/234 | 0.943 | 0.943 (1 seed) | 0.999 | 153s |
| finetuned (B) | 1 | val sens >= 0.95 | 0.996 | 88.5% | 380/390 | 172/234 | 0.943 | 0.943 (1 seed) | 0.999 | 153s |
| finetuned+aug (C) | 3 | >= 0.5 | 0.500 | 62.5% | 390/390 | 0/234 | 0.667 | 0.809 +/- 0.125 | 0.871 | 150s |
| finetuned+aug (C) | 3 | val sens >= 0.95 | 1.000 | 63.6% | 387/390 | 10/234 | 0.667 | 0.809 +/- 0.125 | 0.871 | 150s |