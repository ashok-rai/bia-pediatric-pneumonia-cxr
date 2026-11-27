Question: can a pretrained CNN tell pneumonia from normal in pediatric chest X-rays reliably enough for triage?
On the untouched 624-image official test set, the fine-tuned ResNet-18 (chosen on validation only, threshold 0.996) found 380 of 390 pneumonias (97.4%, 95% CI 95.7%-98.9%) at 172/234 specificity and 88.5% accuracy; AUC 0.943 (CI 0.922-0.961).
Calibration error 0.226 as trained, 0.222 after temperature scaling (T = 1.49, fitted on validation; ranking and decisions unchanged).
Masking the outer 15% of each image moved test AUC from 0.943 to 0.924, and keeping ONLY the border left AUC 0.762 - so the decisions rest on the lung field, not the edges.
Limits: one data set from one hospital group, internal test only; validation is easier than test here (val AUC 0.999); config B has a single seed; config C in notebook 03 was invalid (augmentation applied after normalisation) and is excluded.
