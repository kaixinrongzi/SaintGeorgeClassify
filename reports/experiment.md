# Experiment Report: Image Classification of Saint George Pictures

## Dataset Description
The dataset contains `5570` images and consists of two categories: `positive` (containing Saint George) and `negative` (non-Saint George). The positive class accounts for approximately `40%` of the dataset, while the negative class makes up about `60%`. Both classes feature images with relatively consistent artistic styles, primarily depicting artistic renditions of Saint George, such as paintings or sculptures, which helps maintain stylistic coherence across the dataset.

The negative (non-Saint George) images are highly diversified. They include a wide variety of subjects, such as portraits of people, everyday objects, animals, and more abstract or unrelated scenes. This diversity introduces variability that can challenge the model’s ability to distinguish Saint George images based solely on content. Similarly, the Saint George images themselves exhibit substantial diversity. They encompass sculptures, painted portraits, images of currency with George’s portrait, and other artistic representations. This intra-class variability underscores the importance of robust feature extraction to accurately identify Saint George across different styles and formats.

## Approach
In this project, we employed three state-of-the-art `ResNet34` and `ResNext50` —to perform binary classification of Saint George images. Both `ResNet` and `ResNext50` were selected for its deep residual learning capabilities, allowing effective extraction of local, fine-grained features. 

The models were pretrained on ImageNet, facilitating transfer learning and reducing training time, with fine-tuning performed on the task-specific dataset. The choice of these architectures provides a diverse set of feature extraction strategies—local, efficient, and global—allowing comprehensive evaluation and comparison to determine the most effective approach for the classification of Saint George images.

To improve the robustness and generalization capability of the models, several data augmentation methods are employed during training. `Random rotations` introduce orientation variability by rotating images within a specified range, enabling the model to recognize objects regardless of their angle. `Flipping` images, such as horizontal flips, simulate different viewpoints and mirror images, helping the model become invariant to left-right changes. `Color jitter` varies image attributes like brightness, contrast, saturation, and hue, mimicking real-world lighting and environmental variations, which prevents the model from over-relying on specific color features. 'Cutout' removes a random part of images, improving images variants and mitigating overfitting issues. In addition to augmentations applied directly to the images, batch normalization is used within the neural network architecture to normalize the inputs for every mini-batch. This technique remove outliers of inputs from affecting models performance, stabilizes and accelerates training by maintaining consistent input distributions, ultimately leading to faster convergence and improved model performance. 

Furthermore, the cross-entropy loss was adapted to account for dataset imbalance by using class-weighted cross-entropy, which assigns larger loss weights to underrepresented classes which are negative class in this project.

Collectively, these augmentation strategies enhance the diversity of training data and the cost function modification technique enforces models to focus a little bit more on minority class which is the positive class.


## Models Used
- ResNet34
- ResNeXt50

## Training Configuration
- Number of Epochs: 100
- Learning Rate: 0.0001
- Weight Decay: 1e-6
- Optimizer: AdamW

## Data Augmentation Techniques
To improve model robustness and generalization, the following augmentations were applied:

- Random Erasing
- Random rectangle part removal
- Random horizontal flip
- Color jitter (brightness, contrast, saturation, hue variations)
- Random rotation within a reasonable angle range
- Pixel normalization to match pretrained model standards

## Rationale
### Models Selection
Overall, we used pretrained models to take advantage of knowledge transferring power from previous training.

The chosen models leverage different strengths:

`ResNet` and `ResNeXt50` are convolutional architectures optimized for feature extraction, effectively capturing local patterns in images. `ResNet` is well-known for its residual connections, which alleviate the vanishing gradient problem and enhance the training of very deep networks. Empirically, `ResNet` excels at extracting fine-grained, local features, aiding in identifying small details characteristic of Saint George images. Besides, `ResNet` was trained on 1 million images across a quite broad range of 1000 classes, making its pretrained weights to play an essential role of classifying Saint George in our dataset. 

`ResNeXt-50` delivers improved accuracy over ResNet-like baselines while remaining computationally practical, making it a strong candidate for fine-tuning on image classification tasks. Meanwhile, it provides higher efficiency over `ResNet34` by its grouped convolution feature.

### Optimizer Selection
We choose `AdamW` as the optimizer because AdamW is an optimization algorithm that combines the adaptive learning rate benefits of Adam with a better handling of weight decay regularization. Unlike Adam, AdamW decouples weight decay from the gradient-based update, allowing us to apply weight decay as a separate step, leading to more effective regularization. Also, AdamW has empirical success recently by studies and experiments have shown that AdamW generally outputperforms or matches Adam.

### Hyperparameters Selection
- Learning rate: We selected `0.0001` as the learning rate because it is a commonly used starting point in deep learning by providing a good balance between convergence speed and training stability. Besides, this value tends to work well with optimizer like AdamW for most image classification tasks, allowing the model to converge steadily towards optimal parameters.
- Weight decay: The weight decay serves as a regularization factor to prevent overfitting, especially important in datasets that are imbalanced, which is exactly this dataset our project works on. It applies a small penalty to large weights, mitigating the features that correspond to large weights to overwhelm the classification results. Thus, it encourages model to learn more generalized features. The value of `1e-6` is relatively mild, providing regularization without overly constraining the model, thereby maintaining learning flexibility and stability.
- Epoch number: We selected `100` as the epoch number based on empirical observations and time efficiency. Through prior experiments, it’s observed that models tend to reach satisfactory accuracy within around 100 epochs. Starting with 100 epochs provides a long enough training window to evaluate model performance. Also, since we applied early stopping, the training process won't last for this long time unless necessary.


## Experiments
### Overfitting Issue
During the training of all three models (`ResNet`, and `ResNeXt50`), I encountered severe overfitting, with the models performing well on training data but poorly on validation data. The training and validation accuracy could achived over 95% by all of our models, and their testing accuracies ranges from 93% to 95%, which outperform a random guess (50%) and meets or slightly outperforms the benchmark (93%). To achieve this, I implemented several techniques aimed at improving generalization and preventing overfitting:

- Early Stopping:
I integrated early stopping based on validation loss. During each epoch, the model's performance on the validation set was monitored. If the validation loss did not decrease for a predefined number of epochs (patience parameter), the training process was automatically halted. This approach prevents overtraining, reduces the risk of overfitting, and ensures that the model retains parameters corresponding to the best validation performance. It also conserves computational resources by stopping training once the model stops improving.

- Data Augmentation with Random Erasing Cutout:
To increase the robustness of models and reduce reliance on specific image regions, I added the random Erasing Cutout augmentation method to the training pipeline. During each training iteration, random parts will be erases and random rectangular sections of input images were masked out (filled with zeros). This compels the models to learn features that are distributed across the entire image and helps them recognize objects even when parts are occluded or missing. 

### Training Time Consumption
Given limited compute and a tight timeline, I balanced model quality with training efficiency. Training multiple deep architectures (`ResNet`, `ResNeXt`) can be slow, so I ran the three trainings concurrently using **multithreading** to observe their behavior **in parallel**. This allowed rapid feedback on whether training was proceeding correctly and which models produced promising outputs, enabling quick identification of poor hyperparameter choices and providing a practical starting point for further tuning.

## Results
### Time Complexity
- `ResNet34` takes 2 to 3 minutes per epoch on average
- `ResNeXt50` takes 2 minutes per epoch on average

### Metrics
#### Loss and Accuracy

##### ResNet34 #####

<img src="../assets/ResNet34Metrics.png" alt="Alt Text" width="500"/>

##### ResneXt50 #####

<img src="../assets/ResNext50Metrics.png" alt="Alt Text" width="500"/>

### Model Evaluation
| Model | Test Accuracy| Precision | Recall  |  F1 Score  |
|----------|----------|----------|-----------|----------|
| ResNet34 | 94.27% | 95.39% |90.54% | 92.90% | 
| ResNeXt50| **95.20%** | 93.47% |95.06% | 94.26%|

Among the three models, `ResNeXt50` demonstrates the strongest overall performance, with the highest accuracy at approximately 95.20%. It also slightly outperforms `ResNet` in recall (95.06%), indicating a better ability to identify positive cases, whereas slightly underperforms `ResNet34` in precision (93.47%), indicating a little bit more sensitivity in identifying positive cases. However, overall `ResNeXt50 ` has the highest F1 score, indicating a better positive cases identification. 

#### Summary:
`ResNeXt50` appears most promising for this task, offering the best trade-off between accuracy and positive cases identification. 

