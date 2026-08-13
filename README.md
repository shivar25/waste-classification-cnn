# Waste Classification Using CNN

A beginner-level Deep Learning project that uses a Convolutional Neural Network (CNN) to classify waste images into six different categories.

## Project Overview

Waste management and recycling require efficient identification and separation of different types of waste. This project uses a Convolutional Neural Network to automatically classify waste images into six categories:

- Cardboard
- Glass
- Metal
- Paper
- Plastic
- Trash

The project focuses on understanding the complete workflow of an image classification problem using a CNN, including dataset exploration, preprocessing, data augmentation, model training, and evaluation.

## Dataset

This project uses the **TrashNet** dataset, which contains images belonging to six different waste categories.

### Dataset Summary

| Property | Value |
|---|---:|
| Total Images | 2,527 |
| Number of Classes | 6 |
| Training Images | 1,768 |
| Validation Images | 379 |
| Test Images | 380 |
| Original Image Size | 512 × 384 |
| CNN Input Size | 128 × 128 × 3 |

The dataset was divided using a stratified split:

- **70% Training**
- **15% Validation**
- **15% Testing**

Stratification was used to maintain similar class proportions across the training, validation, and test sets.

The test set was kept separate from model training and was used for final evaluation.

## Classes

| Class | Description |
|---|---|
| Cardboard | Cardboard waste |
| Glass | Glass waste |
| Metal | Metal waste |
| Paper | Paper waste |
| Plastic | Plastic waste |
| Trash | General waste |

## Project Workflow

The project follows the following workflow:

1. Dataset loading
2. Dataset exploration
3. Class distribution analysis
4. Stratified train-validation-test split
5. Image preprocessing
6. Image resizing
7. Pixel normalization
8. Online data augmentation
9. CNN model development
10. Model training
11. Training and validation performance analysis
12. Test set evaluation
13. Classification report
14. Confusion matrix analysis
15. Sample prediction visualization
16. Model saving

## Exploratory Data Analysis

The dataset was explored to understand:

- Number of images in each class
- Class distribution
- Image dimensions
- Representative images from each waste category

The dataset is not perfectly balanced. The `trash` category contains considerably fewer images than classes such as `paper` and `glass`.

## Image Preprocessing

The original images have dimensions of approximately:

```text
512 × 384
```

For computational efficiency, all images were resized to:

```text
128 × 128 × 3
```

where:

- `128` = image height
- `128` = image width
- `3` = RGB color channels

Pixel values were normalized from the range `0–255` to `0–1`.

This preprocessing makes the images suitable for CNN training.

## Data Augmentation

Online data augmentation was applied to the training images to improve model generalization and expose the CNN to slightly different versions of the same images.

The following transformations were used:

- Random horizontal flipping
- Random rotation
- Random zoom

Data augmentation was applied only during training.

The validation and test datasets were kept unchanged.

## CNN Architecture

A basic Convolutional Neural Network was built from scratch using TensorFlow and Keras.

The architecture consists of three convolutional blocks followed by fully connected classification layers.

```text
Input: 128 × 128 × 3
        ↓
Conv2D: 32 filters
        ↓
MaxPooling2D
        ↓
Conv2D: 64 filters
        ↓
MaxPooling2D
        ↓
Conv2D: 128 filters
        ↓
MaxPooling2D
        ↓
Flatten
        ↓
Dense: 128 units
        ↓
Dropout: 0.5
        ↓
Dense: 6 units
        ↓
Softmax
```

### Layer Explanation

**Conv2D**

Convolutional layers learn visual features from the images. Earlier layers learn simpler patterns such as edges and textures, while deeper layers learn more complex visual patterns.

**MaxPooling2D**

Max pooling reduces the spatial dimensions of the feature maps while retaining important information.

**Flatten**

The extracted feature maps are converted into a one-dimensional vector before being passed to the fully connected layers.

**Dense**

The dense layer learns combinations of the extracted features for classification.

**Dropout**

A dropout rate of `0.5` was used to reduce overfitting by randomly dropping some neurons during training.

**Softmax**

The final layer produces probabilities for the six waste categories.

## Model Training

The CNN was trained using the following configuration:

| Parameter | Value |
|---|---|
| Optimizer | Adam |
| Loss Function | Sparse Categorical Cross-Entropy |
| Batch Size | 32 |
| Epochs | 40 |
| Input Size | 128 × 128 × 3 |
| Number of Classes | 6 |

The training and validation performance were monitored throughout the training process.

## Results

The final CNN achieved the following performance on the held-out test set:

| Metric | Result |
|---|---:|
| **Test Accuracy** | **76.84%** |
| Test Loss | **0.8435** |
| Macro F1-score | **0.75** |
| Weighted F1-score | **0.77** |

The model correctly classified approximately 77 out of every 100 unseen test images.

## Classification Report

The class-wise performance of the final model was:

| Class | Precision | Recall | F1-score |
|---|---:|---:|---:|
| Cardboard | 0.94 | 0.80 | 0.86 |
| Glass | 0.74 | 0.64 | 0.69 |
| Metal | 0.78 | 0.73 | 0.75 |
| Paper | 0.81 | 0.89 | 0.85 |
| Plastic | 0.64 | 0.82 | 0.72 |
| Trash | 0.79 | 0.55 | 0.65 |

### Observations

The model performed particularly well on:

- Cardboard
- Paper
- Metal

Paper achieved a recall of **89%**, meaning that the model correctly identified most of the actual paper images.

Cardboard achieved a precision of **94%**, indicating that most images predicted as cardboard were actually cardboard.

The more challenging classes were:

- Glass
- Trash

The lower recall for the trash category is partly influenced by the smaller number of trash images available in the dataset.

## Confusion Matrix

A confusion matrix was used to analyze the types of classification errors made by the CNN.

The model showed some confusion between visually similar waste categories, particularly:

- Glass and plastic
- Glass and metal
- Metal and glass
- Plastic and paper

These errors are understandable because several images in the dataset contain objects with similar shapes and visual characteristics, such as bottles and containers.

## Sample Predictions

The project also includes visual examples of predictions made by the CNN on previously unseen test images.

These examples contain both:

- Correct predictions
- Incorrect predictions

This provides a qualitative understanding of the model's performance beyond numerical evaluation metrics.

## Technologies Used

- Python
- TensorFlow
- Keras
- NumPy
- Pandas
- Matplotlib
- Scikit-learn
- Pillow
- Google Colab

```

## Requirements

The main Python libraries used in this project are:

```text
tensorflow
numpy
pandas
matplotlib
scikit-learn
Pillow
```

They can be installed using:

```bash
pip install -r requirements.txt
```

## How to Run the Project

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/waste-classification-cnn.git
```

### 2. Navigate to the Project Directory

```bash
cd waste-classification-cnn
```

### 3. Install the Required Libraries

```bash
pip install -r requirements.txt
```

### 4. Download the Dataset

Download the TrashNet dataset and place the extracted dataset in the directory expected by the notebook.

The dataset should have the following structure:

```text
dataset-resized/
│
├── cardboard/
├── glass/
├── metal/
├── paper/
├── plastic/
└── trash/
```

### 5. Open the Notebook

Open:

```text
Waste_Classification_CNN.ipynb
```

The notebook contains the complete workflow from dataset exploration and preprocessing to model training and evaluation.

```

## Future Improvements

Possible improvements to the project include:

- Increasing the size of the dataset
- Using a more balanced dataset
- Applying class-specific augmentation
- Hyperparameter tuning
- Experimenting with Batch Normalization
- Increasing image resolution
- Comparing different CNN architectures
- Using transfer learning with pretrained models
- Deploying the model as a web application

## Conclusion

This project demonstrates a complete beginner-level Deep Learning workflow for image classification using a Convolutional Neural Network.

The model classifies waste images into six categories:

- Cardboard
- Glass
- Metal
- Paper
- Plastic
- Trash

The complete pipeline includes dataset exploration, stratified data splitting, image preprocessing, online data augmentation, CNN model development, training, and detailed evaluation.

The final CNN achieved a **76.84% accuracy on the held-out test set**.

The results show that a basic CNN can learn useful visual patterns for waste classification, while also highlighting challenges caused by visually similar waste categories and class imbalance.

## Author

**Shiva Ranjan**
