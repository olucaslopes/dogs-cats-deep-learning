# Dogs vs cats

[Portuguese version](./README.pt.md)


College exercise to classify images of dogs and cats and learning concepts of Deep Learning with Python, TensorFlow and Keras.

## Learned concepts

- using data augmentation to increase the size of the training set and reduce overfitting
- using a pretrained model (VGG16) to classify images with three different strategies:
    - extracting features from the convolutional base and training a classifier on top of it (faster and cheaper)
    - adding a classifier on top of the convolutional base and fine-tuning the top layers of the convolutional base alongside the classifier (more expensive and time-consuming, but can lead to better results)
    - fine-tuning the top layers of the convolutional base alongside the classifier (more expensive and time-consuming, but can lead to better results)


## Model descriptions

#### 30 Epochs Conv

A simple convolutional neural network trained for 30 epochs.

#### 100 Epochs Conv Data Aug

A convolutional neural network with data augmentation and trained for 100 epochs.

#### VGG16 Features + 30 Epochs Dense

A pretrained VGG16 model is used to extract features and feed them to a classifier trained for 30 epochs (data is passed through the convolutional base only once, so it's faster and cheaper than fine-tuning the top layers of the convolutional base alongside the classifier).

#### VGG16 Conv Base + 30 Epochs Dense

A pretrained VGG16 model with all layers frozen and with a dense classifier added on top of it and trained for 30 epochs (data is passed through the convolutional base each time, so it's more expensive and time-consuming than extracting features from the convolutional base and training a classifier on top of it, but it can lead to better results).

#### VGG16 Conv Base + Last Layer Tune 100 Epochs

A pretrained VGG16 model with the top layers of the convolutional base unfrozen and a classifier trained on top of it for 100 epochs (more expensive and time-consuming than adding a classifier on top of the convolutional base and training the top layers of the convolutional base alongside the classifier, but it can lead to better results).

## Model training loss and accuracy comparison

### 30 Epochs Conv vs 100 Epochs Conv Data Aug

| Model | Validation Accuracy | Test Accuracy | Training Time | Model File |
| --- | --- | --- | --- | --- |
| 30 Epochs Conv | 0.7030 | 0.7289 | 4 minutes | cats_and_dogs_small_1.keras |
| 100 Epochs Conv Data Aug | 0.8080 | 0.8009 | 17 minutes | cats_and_dogs_small_2.keras |

![Model training loss and accuracy comparison](./charts/cats_and_dogs_small_default_vs_augmented.png)

With this chart we can see that the model with data augmentation has a better performance than the model without data augmentation and increasing the number of epochs to 100 improves the model accuracy (i.e., the model still has room to improve at 30 epochs).

### 100 Epochs Conv Data Aug vs VGG16 Features + 30 Epochs Dense

| Model | Validation Accuracy | Test Accuracy | Training Time | Model File |
| --- | --- | --- | --- | --- |
| 100 Epochs Conv Data Aug | 0.8080 | 0.8009 | 17 minutes | cats_and_dogs_small_2.keras |
| VGG16 Features + 30 Epochs Dense | 0.9090 | 0.8889 | 16 seconds | cats_and_dogs_small_3.keras |

![Model training loss and accuracy comparison](./charts/cats_and_dogs_small_augmented_vs_VGG16.png)

When comparing these two models, we can see that the model using VGG16 features has a better performance even though it was trained for fewer epochs. This shows the power of using a pretrained model to accelerate the training process and improve the model accuracy.

### VGG16 Features + 30 Epochs Dense vs VGG16 Conv Base + 30 Epochs Dense

| Model | Validation Accuracy | Test Accuracy | Training Time | Model File |
| --- | --- | --- | --- | --- |
| VGG16 Features + 30 Epochs Dense | 0.9090 | 0.8889 | 16 seconds | cats_and_dogs_small_3.keras |
| VGG16 Conv Base + 30 Epochs Dense | 0.9060 | 0.8939 | 25 minutes | cats_and_dogs_small_4.keras |

![Model training loss and accuracy comparison](./charts/cats_and_dogs_small_VGG16_vs_fine_tuned.png)

When comparing the features strategy with the top layers fine-tuning strategy, we can see that the fine-tuning strategy has a slightly better performance. However, the fine-tuning strategy is way more expensive and time-consuming than the features strategy.

### VGG16 Conv Base + 30 Epochs Dense vs VGG16 Conv Base + Last Layer Tune 100 Epochs

| Model | Validation Accuracy | Test Accuracy | Training Time | Model File |
| --- | --- | --- | --- | --- |
| VGG16 Conv Base + 30 Epochs Dense | 0.9060 | 0.8939 | 25 minutes | cats_and_dogs_small_4.keras |
| VGG16 Conv Base + Last Layer Tune 100 Epochs | 0.9400 | 0.9409 | 95 minutes | cats_and_dogs_small_4ft.keras |

![Model training loss and accuracy comparison](./charts/cats_and_dogs_small_fine_tuned_vs_VGG16.png)

When comparing the top layers fine-tuning strategy with the last layer fine-tuning strategy, we can see that the last layer fine-tuning strategy is the one with better performance from all trained models. However, the last layer fine-tuning strategy is way more expensive and time-consuming than the top layers fine-tuning strategy.

## Model Results Summary

| Model | Validation Accuracy | Test Accuracy | Training Time | Model File |
| --- | --- | --- | --- | --- |
| 30 Epochs Conv | 0.7030 | 0.7289 | 4 minutes | cats_and_dogs_small_1.keras |
| 100 Epochs Conv Data Aug | 0.8080 | 0.8009 | 17 minutes | cats_and_dogs_small_2.keras |
| VGG16 Features + 30 Epochs Dense | 0.9090 | 0.8889 | 16 seconds | cats_and_dogs_small_3.keras |
| VGG16 Conv Base + 30 Epochs Dense | 0.9060 | 0.8939 | 25 minutes | cats_and_dogs_small_4.keras |
| VGG16 Conv Base + Last Layer Tune 100 Epochs | 0.9400 | 0.9409 | 95 minutes | cats_and_dogs_small_4ft.keras |