# EEG-Signal-Project
# EEG Data Analysis Project

## Introduction
This project focuses on analyzing Electroencephalogram (EEG) data to investigate differences between healthy individuals and patients with schizophrenia. EEG is a non-invasive neuroimaging technique that measures electrical activity in the brain using electrodes placed on the scalp. By analyzing EEG signals, we aim to identify biomarkers for schizophrenia and develop predictive models for early diagnosis and treatment monitoring.

EEG signals are recorded from multiple channels (electrodes) placed at specific locations on the scalp. Each channel captures electrical activity generated by neuronal firing in the underlying brain regions. The EEG data consists of continuous voltage measurements collected over time, typically sampled at a high frequency (e.g., 250 Hz).

## Data Processing and Augmentation

### Reading Data
We use the `glob` module to retrieve the file paths of all EDF files containing EEG recordings from healthy subjects and patients with schizophrenia. These files are stored in the specified directory and contain multichannel EEG data.

### Data Splitting and Standardization
We perform repeated random sub-sampling validation to split the data into training, validation, and test sets. The training set is further split into training and validation sets to facilitate model training and hyperparameter tuning. We standardize the data using a `StandardScaler` to ensure that each feature has a mean of 0 and a standard deviation of 1.

### Data Augmentation
Data augmentation is performed to increase the diversity of the training dataset and improve the generalization ability of the model. We apply time warping augmentation to each sample in the training set, which involves stretching or compressing the time axis of the EEG signals. This technique helps simulate variations in the duration of EEG recordings and makes the model more robust to temporal distortions.

## Convolutional Neural Network (CNN) Model

### Model Architecture
We define a Convolutional Neural Network (CNN) model using the TensorFlow Keras API to classify EEG signals into healthy and patient groups. The model architecture consists of several Conv1D layers followed by BatchNormalization, LeakyReLU activation, and pooling layers. The final layer uses a sigmoid activation function to output the probability of each sample belonging to the positive class (patient group).

### Model Training
We compile the model using the Adam optimizer and binary cross-entropy loss function. The model is trained on the training data for a specified number of epochs, with a mini-batch size set to 128. We use the validation data for model evaluation during training and monitor the validation accuracy to assess model performance.

### Model Evaluation
After training, we evaluate the model on the test data to assess its generalization ability. We compute the test accuracy, which represents the percentage of correctly classified samples in the test set. Additionally, we calculate the train accuracy to evaluate the model's performance on the training data.

### Training Visualization
We visualize the training process by plotting the validation accuracy across epochs for each fold in the repeated random sub-sampling validation. We also plot the average validation accuracy to assess the overall performance of the model.

### Model Saving and Loading
Finally, we save the trained model to a file named 'my_model.h5' using the `save` method. We then load the saved model using the `load_model` function to make predictions on new data or continue training.

