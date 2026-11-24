Question: Can an ImageNet-pretrained CNN tell pneumonia from normal in pediatric chest X-rays reliably enough to help triage?
On 624 test images, the frozen ResNet-18 (balanced) found 381 of 390 pneumonia images (97.7%; 95 % bootstrap interval 96.1% to 99.0%).
Accuracy 85.6% (interval 82.9% to 88.3%); floor 62.5%; random-forest baseline 76.9%.
Three training seeds: pneumonia found 97.8% ± 0.4%. Calibration error for pneumonia: 0.106.
Limits: one data set, test images from the same source (internal validation only); 0 near-twins between training and test; 2685 training / 427 test patients; 161 in both.
