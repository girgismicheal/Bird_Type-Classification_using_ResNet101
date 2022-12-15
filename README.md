# Bird_classification_with_ResNet101

## Overview
This project amis to classify the bird's type among 200 class.

![](Image/image1.png)

**About the dataset [1]** ([Download the dataset](https://www.kaggle.com/datasets/xiaojiu1414/cub-200-2011))

The Caltech-UCSD Birds-200-2011 (CUB-200-2011) dataset is the most widely-used dataset for fine-grained visual categorization task. It contains 11,788 images of 200 subcategories belonging to birds, 5,994 for training and 5,794 for testing. Each image has detailed annotations: 1 subcategory label, 15 part locations, 312 binary attributes and 1 bounding box. The textual information comes from Reed et al.. They expand the CUB-200-2011 dataset by collecting fine-grained natural language descriptions. Ten single-sentence descriptions are collected for each image. The natural language descriptions are collected through the Amazon Mechanical Turk (AMT) platform, and are required at least 10 words, without any information of subcategories and actions.

**Dataset description:**
- Number of categories: 200
- Number of images: 11,788
- Annotations per image: 
  - 15 Part Locations
  - 312 Binary Attributes 
  - 1 Bounding Box

## Results
### Custom model
**For building the model:**
- I used two layers with 256 and 128 neurons to be able to train it with the res-net in Part 2 without any ram issues.
- Also, I used BatchNormalization and  Dropout to reduce the overfitting.

| Loss curve            | Accuracy curve            |
|-----------------------|---------------------------|
| ![](Image/Output.png) | ![](Image/Output2.png)    |


**Conclusion:**
- The training is so slow due to a large number of parameters due to a large number of features in the (32 * 32 * 3) image which causes a huge number of parameters.
- The training accuracy reached above 60% while the testing accuracy was under 10.8% which means the model highly overfitted the training data because of a large number of features and parameters.
- If we used Convolution layers it would work better with this problem as it has many useful features such as:
    - Reducing the required parameter and parameter-sharing features
    - Eliminate the need for manual feature extraction
