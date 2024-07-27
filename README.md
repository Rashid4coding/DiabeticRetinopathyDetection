# Diabetic Retinopathy Detection


# File Organization

Due to size of the Diabetic Retinopathy Dataset you've to extracts manually download the dataset and extract it in **ext** directory

https://www.kaggle.com/competitions/diabetic-retinopathy-detection/data?select=sample.zip

1. **Feature extraction** - Once the data has been downloaded and extracted at ext directory, this file is used to extract features from it. It uses Resnet101 our base model and extract features, flatten them and store them as flatten arrays in **processed/train** directory if they're training images and in **processed/unlabeled** directory if they're testing images.

2. **Selecting Reliable and Unreliable Samples** - Once the features has been extracted and stored in **processed** directory. This file computes **cosine similarities**  between the train set and unlabeled set, and, based on similarity threshold seperates the reliable and unreliable samples, stores the reliable in **data/sampled/reliable/** and unreliable in **data/sampled/unreliable/** directory.

3. **Reliable Pseudo labeling 3 Classifiers** 

    Following are the tasks it performs

    - Loads in the labeled dataset
    - Balance it via SMOTE algorithm
    - Split it into train and validation set
    - trains three classifiers linear, knn, and similarity based classifiers. 
    - Combine them with alpha weightage
    - Evalaute the performance on the combination
    - Predict pseudo labels of the reliable samples

4. **Contrastive learning**

    - It loads in the training data
    - trains the contrastive learner on it
    - pick up the CNN block
    - Extract features from both training and unreliable dataset
    - Use trains Classifier head on training set and assign pseudo labels to unreliable dataset
    - Showcase Cluster graph via tsne of unreliable dataset and its pseudo labels

5. **Updated only Reliable Pseudo-labels results** - loads in the training and reliable data with its reliable pseudo labels, mix them all together, and, balance the data via smote, train test split, trains the model and test it on test set.

6. **Updated Reliable and Unreliable Pseudo-labels results** - loads in the training, reliable data with its reliable pseudo labels, and unreliable data with its unrelable pseudo labels, mix them all together, and, balance the data via smote, train test split, trains the model and test it on test set.

7. **GradCam** - It uses GradCam along with pretrained model to display gradients on Images

*After that we conducted various experiment*

8. **Experiment 1** - Here we trained the model on reliable dataset and tested it on reliable, unreliable, and, mix of reliable and unreliable dataset. For reliable it of course it showed good results, for unreliable terible and for mixture not so good at all.

9. **Experiment 2** - Here we trained the model on mix of reliable and unreliable dataset and tested on reliable, unreliable and mix dataset. The results were very pleasant

10. **Experiment 3** - So far we have been balancing our dataset via SMOTE a lot so we decided not to, and, the results were not so good at all

11. **Experiment 4** - And in our balance we deal with balancing in a peculiar instead of balancing all classes we increase some samples in one class more than the other so model has no way to overfit one class. Therefore we decided to showcase what happens if we keep all classes to have same number of samples to showcase the validity of our approach. There results were nowhere near to the former.