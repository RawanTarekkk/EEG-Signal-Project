# EEG-Signal-Project

## Table Contents 
* [Introduction](Project/blob/main/README.md#introduction)

* [Data Preprocessing](https://github.com/RawanTarekkk/EEG-Signal-Project/blob/main/README.md#data-processing-and-augmentation)

* [CNN Model](https://github.com/RawanTarekkk/EEG-Signal-Project/blob/main/README.md#convolutional-neural-network-cnn-model)

* [Evaluation](https://github.com/RawanTarekkk/EEG-Signal-Project/blob/main/README.md#model-evaluation-summary)


## Introduction
This project focuses on analyzing Electroencephalogram (EEG) data to classify between healthy individuals and patients with schizophrenia. 
EEG is a non-invasive neuroimaging technique that measures electrical activity in the brain using electrodes placed on the scalp. By analyzing EEG signals, we aim to identify biomarkers in the signals for schizophrenia and develop a predictive CNN model for early diagnosis and treatment monitoring.

EEG signals are recorded from 19 channels (electrodes) placed at specific locations on the scalp. Each channel captures electrical activity generated by neuronal firing in the underlying brain regions. The EEG data consists of continuous voltage measurements collected over time, typically sampled at a high frequency (e.g., 250 Hz).

## Download the Data 
[Link to Google Drive File](https://drive.google.com/file/d/1C_-97ewUv3LwI-yODNY2fHTUxdJlo5os/view?usp=sharing)


## Data Processing and Augmentation

### Reading Data
We use the `glob` module to retrieve the file paths of all EDF files containing EEG recordings from healthy subjects and patients with schizophrenia and we also used mne library to analyse and process on the EEG data. 
These files are stored in the specified directory and contain multichannel EEG data.

### Data Splitting and Standardization
We perform repeated random sub-sampling validation to split the data into training, validation, and test sets as in cross-validation idea. 
The training set is further split into training and validation sets to facilitate model training and hyperparameter tuning. 

We standardize the data using a `StandardScaler` to ensure that each feature has a mean of 0 and a standard deviation of 1.

### Data Augmentation
Data augmentation is performed to increase the diversity of the training dataset and improve the generalization ability of the model. 
We apply augmentation to each sample in the training set, which involves stretching or compressing the time axis of the EEG signals. 
This technique helps simulate variations in the duration of EEG recordings and makes the model more robust to temporal distortions.

## Convolutional Neural Network (CNN) Model

### Model Architecture
We define a Convolutional Neural Network (CNN) model using the TensorFlow Keras API to classify EEG signals into healthy and patient groups.
The model architecture consists of several Conv1D layers followed by BatchNormalization, LeakyReLU activation, and pooling layers. 
The final layer uses a sigmoid activation function to output the probability of each sample belonging to the positive class (patient group).
![image](https://github.com/RawanTarekkk/EEG-Signal-Project/assets/161609730/01538168-a2f5-49db-a799-b07dfd313325)


### Model Training
We compile the model using the Adam optimizer and binary cross-entropy loss function. 
The model is trained on the training data for a specified number of epochs, with a mini-batch size set to 128. 
We use the validation data for model evaluation during training and monitor the validation accuracy to assess model performance.

### Model Evaluation
After training, we evaluate the model on the test data to assess its generalization ability.
#### By Accuracy 
We compute the test accuracy, which represents the percentage of correctly classified samples in the test set. 
Additionally, we calculate the train accuracy to evaluate the model's performance on the training data.
![image](https://github.com/RawanTarekkk/EEG-Signal-Project/assets/161609730/36f20665-e105-4fbd-a5c6-bdfad56c7a15)


### Training Visualization
We visualize the training process by plotting the validation accuracy across epochs for each fold in the repeated random sub-sampling validation. We also plot the average validation accuracy to assess the overall performance of the model.

### Model Saving and Loading
Finally, we save the trained model to a file named 'my_model.h5' using the `save` method. We then load the saved model using the `load_model` function to make predictions on new data or continue training.

## Model Evaluation Summary

This section of the code is dedicated to evaluating the performance of a Deep learning model for binary classification tasks. Here's a brief overview of what each part does:

1. **Import Necessary Libraries**: Imports essential libraries like NumPy, Seaborn, Matplotlib, and scikit-learn's metrics for evaluation.

2. **Get Predicted Probabilities from the Model**: Retrieves predicted probabilities for the test data from the trained model.

3. **Determines several Thresholds**: to Establishe a ROC evaluation curve.

4. **Determine the Best Threshold**: Establishes a threshold value ( 0.8) to convert predicted probabilities into binary classifications.

5. **Calculate Overall Metrics**: Computes various evaluation metrics such as accuracy, precision, recall (sensitivity), and F1-score using scikit-learn's metrics.

6. **Calculate Specificity**: Defines a function to calculate specificity and computes it based on the confusion matrix.

7. **Print Overall Metrics**: Displays the calculated evaluation metrics to assess the model's performance.
![image](https://github.com/RawanTarekkk/EEG-Signal-Project/assets/161609730/a3216398-d77f-49b4-aadd-4088f496fc19)

8. **Print Detailed Classification Report**: Generates a detailed classification report including precision, recall, F1-score, and support for each class.

9. **Plot Confusion Matrix**: Visualizes the confusion matrix to understand the model's performance in terms of true positives, true negatives, false positives, and false negatives.
   
![image](https://github.com/RawanTarekkk/EEG-Signal-Project/assets/161609730/6a1ab3f3-4db6-44c8-9dba-75979ddb2a19)

10. **Calculate and Plot ROC Curve and AUC**: Computes the Receiver Operating Characteristic (ROC) curve and the Area Under the Curve (AUC) to evaluate the model's ability to discriminate between positive and negative classes.

![image](https://github.com/RawanTarekkk/EEG-Signal-Project/assets/161609730/168829c4-16dc-4f03-ad49-060acc23e70a)
