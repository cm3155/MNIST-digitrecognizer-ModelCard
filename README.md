# MNIST Digit Recognizer Model Card

### Basic Information

* **Person or organization developing model**: Cassidy Macklin, `cmacklin@gwu.edu`
* **Model date**: December 9, 2024
* **Model version**: 0.1
* **License**: MIT
* **Model implementation code**: [DigitRecognizerComp.ipynb](https://github.com/cm3155/final-proj/blob/main/DigitRecognizerComp.ipynb)

### Intended Use
* **Primary intended uses**: This model is an educational example of a model that could be used to classify images of hand-written digits from 0-9. 
* **Primary intended users**: Students and those interested in learning about machine learning. 
* **Out-of-scope use cases**: Any use beyond an educational example is out-of-scope.

### Training Data

* **Source of training data**: Kaggle
* **How training data was divided into training and validation data**: 80% training, 20% validation
* **Number of rows in training and validation data**:
  * Training rows: 33,600
  * Validation rows: 4,400

* Data dictionary: 

| Name | Modeling Role | Measurement Level| Description|
| ---- | ------------- | ---------------- | ---------- |
|**Image**| input | array of 784 pixel values | 28x28 gray-scale image of hand-drawn digit (0-9) |
| **Label** | target | int | number (0-9) that describes the image |


### Test Data
* **Source of test data**: Kaggle
* **Number of rows in test data**: 28,000
* **State any differences in columns between training and test data**: Test data does not contain label information

### Model details
* **Columns used as inputs in the final model**: The image is the input, therefore columns 'pixel0' through 'pixel783' were used
* **Column(s) used as target(s) in the final model**: 'label'
* **Type of model**: Convolutional Neural Network 
* **Software used to implement the model**: Python, Keras, Tensorflow, sklearn, pandas, NumPy
* **Version of the modeling software**: tensorflow 2.18.0
* **Hyperparameters or other settings of your model**: 
```
def define_model():
	model = Sequential()
	model.add(Conv2D(32, (3, 3), activation='relu', kernel_initializer='he_uniform', input_shape=(28, 28, 1)))
	model.add(Conv2D(32, (3, 3), activation='relu', kernel_initializer='he_uniform'))
	model.add(MaxPooling2D((2, 2)))
	model.add(Dropout(0.1))
	model.add(Conv2D(64, (3, 3), activation='relu', kernel_initializer='he_uniform'))
	model.add(Conv2D(64, (3, 3), activation='relu', kernel_initializer='he_uniform'))
	model.add(MaxPooling2D((2, 2)))
	model.add(Dropout(0.1))
	model.add(Conv2D(128, (3, 3), activation='relu', kernel_initializer='he_uniform'))
	model.add(MaxPooling2D((2, 2)))
	model.add(Dropout(0.1))
	model.add(Flatten())
	model.add(Dense(10, activation='softmax'))
	# compile model
	model.compile(optimizer='rmsprop', loss='categorical_crossentropy', metrics=['accuracy'])
	return model

model = define_model()
history = model.fit(trainX, trainY, epochs=10, batch_size=64, validation_data=(testX, testY), verbose=0)
_, acc = model.evaluate(testX, testY, verbose=0)
```
*  **Model Architecture**:

![alt text](https://github.com/user-attachments/assets/9769ae41-915c-42da-a94b-fc90f93c58dd)

### Quantitative Analysis

* For this competition, models were assessed with Accuracy: 

| Train Accuracy | Validation Accuracy | Test Accuracy |
| ------ | ------- | -------- |
| 0.9992 | 0.9920  | 0.9923* |

(*Test Accuracy taken from https://www.kaggle.com/competitions/digit-recognizer/submissions)

![alt text](https://github.com/user-attachments/assets/7f02f230-6df1-401d-b5ab-456d6a349eb5)

### Potential negative impacts of using this model:
* This model did not achieve perfect accuracy on the validation or test data sets, meaning that it is likely to also classify some images incorrectly if given further unseen data. 
* It is reasonable to assume that there exists some other model architecture that would perform better on the test data. If the model was used for educational purposes, there is a risk of users basing their own models off of an inferior architecture. 
* If the model was used for an out-of-scope use case, for example, in mailing, incorrectly classfied numbers could lead to addresses being processed incorrectly and mail being sent to the wrong place. This could result in financial losses and breaches in security. 
