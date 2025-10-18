# Final Report — Results, Analysis, and Next Steps #

## 1. Summary of Models and Metrics ##
- Dataset: binary classification (Saint George vs. non‑Saint George). Positive ≈ 40%, Negative ≈ 60%
- Models evaluated: `ResNet34`, `ResNeXt50`
- Training setup (common): epochs = 100, lr = 0.0001, weight_decay = 1e-6, cost function = weighted cross entropy, optimizer = AdamW, augmentations = random horizontal flip, color jitter, random rotation, center crop, random erasing / cutout, normalization

## Performance on test set

| Model | Test Accuracy| Precision | Recall  |  F1 Score  |
|----------|----------|----------|-----------|----------|
| ResNet34 | 94.27% | 95.39% |90.54% | 92.90% | 
| ResNeXt50| **95.20%** | 93.47% |95.06% | 94.26%|

## 2. Interpretation
Interpretation

- Overall: Both models perform very well on the test set, with high accuracy and balanced precision/recall — the classifier is reliable.

- ResNet34 (Accuracy 94.27%): Strong precision (95.39%) and good recall (90.54%), yielding an F1 of 92.90. This indicates `ResNet34` is slightly conservative in predicting positives (fewer false positives) while still recovering most true positives.

- ResNeXt50 (Accuracy 95.20%, best): Slightly higher overall accuracy and the best F1 (94.26). Its recall (95.06%) is notably higher than `ResNet34`’s, meaning `ResNeXt50` finds more true positives. Precision (93.47%) is slightly lower than ResNet34’s but still high, so the increased sensitivity comes with only a small rise in false positives.

- Summary: `ResNeXt50` offers a better balance for this task — it detects more positives (higher recall) while maintaining high precision, resulting in superior F1 and accuracy. If missing positives is costly, prefer `ResNeXt50`; if minimizing false positives is a priority, `ResNet34` is a reasonable alternative.

## 3. Example Misclassifications (qualitative)
- False negatives (missed positives): often when Saint George appears small in the image, heavily occluded, stylized (coin portrait), low contrast, or artistically abstracted.
- False positives (incorrectly predicted positive): non‑George images containing human figures, ornamental motifs, or shapes resembling George iconography.
- Representative misclassified examples are included in the repo (reports/misclassified/) in the format of `image, true label, predicted label` for helping diagnose learned cues.

## 4. Analysis of Causes
- High intra-class variation within positives (different media and styles) increases recognition difficulty.
- Negative class diversity introduces many distractors and spurious correlations.
- Pretrained backbones reduce training time but fine-tuning on limited diverse positives remains challenging.
- Current augmentations help but may not cover all relevant variations (scale, occlusion, artistic styles).
  
## 5. Actions Taken to Mitigate Overfitting
- Early stopping on validation loss with patience to avoid overtraining.
- Cutout / Random Erasing added to force robustness to occlusion.
- Mixed augmentations (flip, rotation, cutout, erasing, color jitter) and transfer learning with pretrained backbones.
These measures reduced overfitting and improved test accuracies (all models > 93%), with `ResNeXt50` at ≈95.30%.

## 6. Recommended Improvements
- Expand dataset: collect more positive examples across styles or use synthetic augmentation (style transfer).
- Frequency-domain features: experiment with **Fourier features** or hybrid spatial+frequency inputs.
- Architecture search: try hybrid `CNN‑Transformer` models.
  
## 7. Reproducibility & Artifacts
Repo contains: 
- [Google Colab Notebook](../SaintGeorgeClassify.ipynb) for the entire pipeline: data processing, dataset preparation, model training, model inference, and model evaluation.
- Experiment logs ([training logs](./logs/training_logs.log) and [training metrics](./logs/training_loss_and_accuracy.log)) contain the loss and accuracy for each epoch for each model, the training start time and end time for tracking time complexity of running each model, and model evaluation metrics
- [Experiment.md](./experiment.md) report
- [Misclassified images](./misclassified/)
- CI: add a workflow to run notebook tests and validate execution (install kernel, required packages, run with papermill).

## 9. Final Recommendation
Continue with `ResNeXt50` as the primary candidate, and focus on:
- minority class augmentation
- loss-level adjustments to incorporate dataset imbalance
- ensembling once individual models are improved.
