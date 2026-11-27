# 01 · patient overlap: template split vs patient-level split

| overlap / twins | template split (image-level) | new split (patient-level) |
|---|---|---|
| patients train &cap; test | 161 | 0 |
| patients train &cap; val | 297 | 0 |
| patients val &cap; test | 32 | 0 |
| near-twins test vs train | 0 | 0 |
| near-twins val vs train | 3 | 0 |

**The 170 patients in official train &cap; official test, by ID type:** person: 170. By label(s): PNEUMONIA: 170.

**Images dropped from training** because their patient also appears in the official test set: **457** of 5232.
