# Finetune, Optimize, and Search: AutoML for Vision Datasets

This repository provides a generic AutoML pipeline designed to yield an optimal architecture for classifying images from various datasets. The project is aimed at exploring and improving the performance of vision models through fine-tuning, optimization, and architecture search.

## Goal

The primary goal of this project is to create a robust AutoML pipeline that automatically discovers the best-performing architecture for image classification tasks across diverse datasets.

## Methods Used

- **Bayesian Optimization**
- **Hyperparameter Optimization**
- **Differentiable Architecture Search (DARTS)**
- **ResNet34 Fine-Tuning**
- **Data Augmentation**
- **Model Checkpointing**

## Approach

The pipeline follows a systematic approach:

1. **Data Preprocessing**:
   - Train/test split (80% for training, 20% for validation).
   - Data augmentation techniques: Resize (256), CenterCrop (224), RandomHorizontalFlip(), RandomRotation (30), Normalize.

2. **Model Fine-Tuning**:
   - Fine-tuned ResNet34 is used as the initial feature extractor, with adjustments to optimize for specific datasets.
   - fc1000 layer is replaced with a Multi-Layer Perceptron (MLP) discovered by DARTS, customized per dataset.

3. **Bayesian Optimization**:
   - Used for hyperparameter tuning with Gaussian Processes.
   - Parameters include learning rate, momentum, weight decay, and optimizer selection.
   - Optimizations are applied iteratively every epoch to improve the finetuned model's performance.

4. **Differentiable Architecture Search (DARTS)**:
   - DARTS Classifier searches for the optimal architecture using a mixed layer approach, including blocks with various layer sizes and activation functions.

### Resource Allocation

For development and AutoML, the following resources were utilized:
- **NVIDIA GTX 1050TI**
- **Intel Core i5-7300HQ**

## Empirical Results

The model's performance was evaluated across several datasets, with results compared against baseline metrics:

| Dataset     | Our Method (F1 Score) | Baseline (F1 Score) | Precision | Accuracy |
|-------------|------------------------|----------------------|-----------|----------|
| Emotions    | 0.63                   | N/A                  | 0.64      | 0.66     |
| Fashion     | 0.93                   | 0.93                 | 0.94      | 0.93     |
| Flowers     | 0.93                   | 0.94                 | 0.94      | 0.55     |
| Skin Cancer | 0.77                   | N/A                  | 0.79      | 0.87     |

### Optimal Parameters

- **Bayesian Optimization (Skin Cancer Dataset)**
- **DARTS Parameters for Skin Cancer Dataset**

## Visual Results

The following figures illustrate the distribution of DARTS alpha values and the accuracy achieved using each DARTS operation:

1. **Alpha Distribution (After Training DARTS)** - Shows the distribution of alpha values after DARTS optimization.
2. **Validation vs. Training Loss (Bayesian Optimization)** - Visual representation of loss metrics.
3. **Classification Accuracy per DARTS Operation** - Accuracy achieved by each operation within DARTS on test datasets.

## References

1. He, K., Zhang, X., Ren, S., & Sun, J. (2015). Deep Residual Learning for Image Recognition. 2016 IEEE Conference on Computer Vision and Pattern Recognition (CVPR), 770-778.
2. Liu, H., Simonyan, K., & Yang, Y. (2018). DARTS: Differentiable Architecture Search. arXiv preprint arXiv:1806.09055.
3. Zhu, Y., Zheng, S., & Yao, X. (2020). An Efficient Transfer Learning-based Model for Plant Disease Classification.

## Contact

For questions or further information, please contact the author.
