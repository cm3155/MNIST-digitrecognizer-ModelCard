# MNIST Digit Recognizer Model Card

### Basic Information

* **Person or organization developing model**: Cassidy Macklin, `cmacklin@gwu.edu`
* **Model date**: December 9, 2024
* **Model version**: 0.1
* **License**: MIT
* **Model implementation code**: [DNSC_6301_Example_Project.ipynb](https://github.com/jphall663/GWU_DNSC_6301_project/blob/main/DNSC_6301_Example_Project.ipynb)

### Intended Use
* **Primary intended uses**: This model is an example of a model that could be used to recognize and classify images of hand-written digits from 0-9. 
* **Primary intended users**: Students and those interested in learning about machine learning. 
* **Out-of-scope use cases**: Any use beyond an educational example is out-of-scope.

### Training Data

* Data dictionary: 

| Name | Modeling Role | Measurement Level| Description|
| ---- | ------------- | ---------------- | ---------- |
|**Image**| input | np.array | digit image |
| **Label** | target | int64 | number 0-9 that the image features |


* **Source of training data**: Kaggle
* **How training data was divided into training and validation data**: 80% training, 20% validation
* **Number of rows in training and validation data**:
  * Training rows: 33,600
  * Validation rows: 4,400

### Test Data
* **Source of test data**: Kaggle
* **Number of rows in test data**: 28,000
* **State any differences in columns between training and test data**: Test data does not contain label information

### Model details
* **Columns used as inputs in the final model**: 'Image'
* **Column(s) used as target(s) in the final model**: 'Label'
* **Type of model**: Convolutional Neural Network 
* **Software used to implement the model**: Python, Keras, Tensorflow
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
| 0.9972 | 0.9898  | 0.9898* |

(*Test Accuracy taken from https://www.kaggle.com/competitions/digit-recognizer/submissions)

Describe potential negative impacts of using your model:
■ Math or software problems
■ Real-world risks: who, what, when or how
○ Describe potential uncertainties relating to the impacts of using your model:
■ Math or software problems
■ Real-world risks: who, what, when or how?
○ Describe any unexpected or results


