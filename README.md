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
  * Training rows: 15,000
  * Validation rows: 7,500

### Test Data
* **Source of test data**: Kaggle
* **Number of rows in test data**: 7,500
* **State any differences in columns between training and test data**: None

### Model details
* **Columns used as inputs in the final model**: 'Image'
* **Column(s) used as target(s) in the final model**: 'Label'
* **Type of model**: Convolutional Neural Network 
* **Software used to implement the model**: Python, Keras, Tensorflow
* **Version of the modeling software**: tensorflow 2.18.0
* **Hyperparameters or other settings of your model**: 
```
KerasClassifier(epochs=10, batch_size=64,verbose=0)

Model Architecture: ![image](https://github.com/user-attachments/assets/a178cfbd-1d7a-449c-b82a-0f5019436b68)

```
### Quantitative Analysis

* Models were assessed with AUC: 

| Train AUC | Validation AUC | Test AUC |
| ------ | ------- | -------- |
| 0.3456 | 0.7891  | 0.7687* |


(*Test AUC taken from https://github.com/jphall663/GWU_rml/blob/master/assignments/model_eval_2023_06_21_12_52_47.csv)


