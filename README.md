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

### Resnet-101
#### Freeze Resnet-101 architecture concatenated to the custom model

| Loss curve             | Accuracy curve         |
|------------------------|------------------------|
| ![](Image/Output3.png) | ![](Image/Output4.png) |


#### Unfreeze some layers in the Resnet-101 architecture

| Loss curve             | Accuracy curve         |
|------------------------|------------------------|
| ![](Image/Output5.png) | ![](Image/Output6.png) |


#### ResNet Conclusion
The pre-trained model has an overall better performance than our customized one due to:
- It's trained on an image-net dataset which is a near to our problem.
- It uses CNN which is effective with image and easier to generalize.

By comparing the model with freezing all the layers versus unfreezing some layers we found that:
- First and second figure shows both models overfit the training data, but the unfrozen model perform better on the testing data
- Third and forth figure shows both model losses reduced the same on the training but the unfrozen model perform better on the testing data

- Both models reached almost 100% on the training dataset but that is not a good metric for the performance meature
- The unfreezing model perform better as it reached 70% on the testing set while the freezing model reached only 59% on the testing data
- Also, the loss decreases faster in the unfrozen model.


### Visualizations:

#### Visualizing the best filter's weights
For this section i will visualize the filters learned by your ResNet-101 network using the t-SNE to observe clusters that were learned by your model.

- **Visualizing the last layer's filters**
![](Image/Output7.png)

#### Visualize the best model embedding map
**I would take the features of the last dense layer then localize it in the 2D space using T-sne algorithm.**
![](Image/Output8.png)

#### Visualization's Conclusion
- By visualizing the filters of the first layer and comparing it with the final layer's filters, we easily deduce that the feature captured by the first layer is just simple features such as (points and lines),
but at the last layer, there are more complicated features.
- By visualizing extracted feature of the layer before the softmax using tsne algorithm, we can find the features of the same class are near in the projected space and the different classes are far from each other.
- Also, by visualizing the test set in the projected space, we found the image that has common features such as red wings or something common is clustered together.

