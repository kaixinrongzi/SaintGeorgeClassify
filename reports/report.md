# Final Report — Results, Analysis, and Next Steps #

## 1. Summary of Models and Metrics ##
- Dataset: binary classification (Saint George vs. non‑Saint George). Positive ≈ 40%, Negative ≈ 60%
- Models evaluated: `ResNet`, `EfficientNet`, `Vision Transformer (ViT)`
- Training setup (common): epochs = 20, lr = 0.001, weight_decay = 1e-6, optimizer = AdamW, augmentations = random horizontal flip, color jitter, random rotation, center crop, random erasing / cutout, normalization

## Performance on test set

|Model|	Accuracy|	Precision	Recall|	F1 Score|
|-----|---------|------------------|---------|
|ResNet	|0.6158|	0.8542	|0.0869	|0.1577|
|EfficientNet|	0.5877|	0.6250|	0.0106|	0.0208|
|VisionTransformer|	0.6737|	0.6397|	0.4852|	0.5518|

## 2. Interpretation
- **VisionTransformer** demonstrates the strongest overall performance with the highest accuracy (67.4%) and the best balance between precision and recall (F1 ≈ 0.5518). Its higher recall (48.5%) indicates better detection of positive cases.
- **ResNet** achieves high precision (≈85.4%) but very low recall (≈8.7%), meaning it predicts positives rarely but is usually correct when it does — it misses most positive instances.
- **EfficientNet** performs worst overall (accuracy ≈58.8%) with extremely low recall (~1.1%), indicating it largely fails to identify positives.
- **Likely contributors**: intra-class diversity for positives (statues, paintings, coins), high diversity in negatives, and moderate dataset size (~5.7k images). ViT’s global-context modeling helps with diverse representations.

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
- Increased weight decay for stronger L2 regularization.
- Mixed augmentations (flip, rotation, color jitter) and transfer learning with pretrained backbones.
These measures reduced overfitting and improved test accuracies (all models > 58%), with `ViT` at ≈67%.

## 6. Recommended Improvements (prioritized)
### Short term
- Threshold tuning: tune classification threshold (not fixed 0.5) to trade precision/recall per application needs.
- Class rebalancing: use class weights in the loss or a weighted sampler to emphasize the positive class.
- Calibration: apply Platt scaling or isotonic regression to calibrate probabilities.
  
### Medium term
- Stronger augmentations: MixUp, CutMix, multi-scale random crops, random perspective, CLAHE/histogram equalization.
- Alternative losses: focal loss or class-balanced loss to focus on hard/rare examples.
- Ensembling: combine `ViT` with `CNNs` (logit averaging or stacking) to leverage complementary strengths.
- Fine-tune schedule: freeze/unfreeze layers, use lower LR for backbone, longer training with validation-based stopping.

### Long term (more effort)
- Expand dataset: collect more positive examples across styles or use synthetic augmentation (style transfer).
- Frequency-domain features: experiment with **Fourier features** or hybrid spatial+frequency inputs.
- Architecture search: try `ConvNeXt`, hybrid `CNN‑Transformer` models, or larger ViT variants.
  
## 7. Reproducibility & Artifacts
Repo contains: 
- [Google Colab Notebook](../SaintGeorgeClassify.ipynb) for the entire pipeline: data processing, dataset preparation, model training, model inference, and model evaluation.
- Experiment logs ([training logs](../logs/training_logs.log) and [training metrics](../logs/training_loss_and_accuracy.log)) contain the loss and accuracy for each epoch for each model, the training start time and end time for tracking time complexity of running each model, and model evaluation metrics
- [Experiment.md](./experiment.md) report
- [Misclassified images](./misclassified/)
- CI: add a workflow to run notebook tests and validate execution (install kernel, required packages, run with papermill).

## 8. Next Experiments to Run
- Compute ROC curves and AUC for each model.
- Run experiments with class-weighted loss and focal loss; compare precision/recall and F1.
- Ensemble ViT + ResNet/EfficientNet and validate on a held-out set.
- Perform threshold sweep for ViT to identify operating point with desired recall/precision.
- Experiment with additional augmentations (MixUp / CutMix) and increased weight decay values.

## 9. Final Recommendation
Continue with `VisionTransformer` as the primary candidate, and focus on:
- threshold tuning and class rebalancing to increase recall,
- stronger augmentation and loss-level adjustments, and
- ensembling once individual models are improved.
