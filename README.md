# Zero-Shot-Machine-Unlearning-MNIST-HAM10000

## Overview
This repository demonstrates the implementation of **Machine Unlearning** and **Zero-Shot Machine Unlearning** concepts applied to a skin cancer image dataset. These methods enable selective forgetting of specific data subsets while preserving the model's performance on retained data. The project also explores the trade-offs in efficiency, accuracy, and robustness between these approaches.

---

## Dataset
The dataset used is the **HAM10000 Dataset**, which consists of skin lesion images and their associated metadata. The dataset includes:
- **10,015 high-resolution images** of skin lesions.
- Labels (`dx`) for 7 classes, including melanoma, nevus, and others.
- Images divided into two parts for initial processing.

### Preprocessing Steps:
1. **Data Consolidation**:
   - Combined images from two directories into a single directory.
   - Mapped images to their metadata using unique IDs.
2. **Normalization**:
   - Resized images to `224x224`.
   - Applied pixel value normalization with mean and standard deviation of `0.5`.

---

## Code Explanation

### 1. **Machine Unlearning**
- Implements selective retraining on the **retain dataset** while forgetting specific data.
- Uses data augmentations (e.g., random flips, rotations, color jitter) to improve generalization.
- Includes early stopping to optimize training efficiency.

#### Key Features:
- Retains performance similar to baseline models.
- Incorporates **entropy filters** (via augmentations) to manage variability in retained data.

### 2. **Zero-Shot Machine Unlearning**
- Focuses on **data-free unlearning**, avoiding retraining by leveraging noise or gated knowledge transfer.
- Removes the influence of specific data subsets without accessing the original training data.

---

## Results Comparison

| **Metric**               | **Baseline Re-trained Model** | **Fine-tuned Machine Unlearning Model** |
|---------------------------|-------------------------------|------------------------------------------|
| **Attack Accuracy**       | 0.50                         | 0.50                                    |
| **Initial Loss**          | 0.9350                       | 0.7792                                  |
| **Final Loss**            | 0.7055                       | 0.6932                                  |
| **Test Loss (Mean)**      | 0.735 (\u00b10.230)               | 0.738 (\u00b10.275)                          |
| **Forget Loss (Mean)**    | 0.712 (\u00b10.150)               | 0.719 (\u00b10.180)                          |

**Key Insights:**
- **Attack Accuracy**: Both models achieve equivalent attack resistance, ensuring robustness against privacy breaches.
- **Loss Metrics**: The fine-tuned machine unlearning model demonstrates slightly better final loss, highlighting effective retention of generalization.
- **Efficiency**: The machine unlearning model achieves comparable results in fewer epochs, demonstrating computational efficiency.

---

## References
1. **[Machine Unlearning (SISA)](https://arxiv.org/abs/2003.04247)**:
   - Describes the concept of Sharded, Isolated, Sliced, and Aggregated (SISA) training for efficient unlearning.
   - Provides foundational ideas for data segmentation and retraining.
2. **[Zero-Shot Machine Unlearning](https://arxiv.org/abs/2201.05629)**:
   - Introduces unlearning without retraining through error-minimizing noise and gated knowledge transfer.
   - Inspires the data-free unlearning approach demonstrated in this repository.

---

## Future Work
1. **Incorporating SISA Training**:
   - Extend the implementation to include sharded and sliced training for finer-grained control of unlearning.
2. **Formal Evaluation Metrics**:
   - Implement advanced metrics such as the **Anamnesis Index (AIN)** to evaluate the effectiveness of unlearning quantitatively.
3. **Real-World Applications**:
   - Explore use cases in privacy-preserving AI, healthcare, and compliance with data deletion laws like GDPR.
