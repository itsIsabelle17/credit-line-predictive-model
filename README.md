# DNSC-6301-Group-Project

# Credit Line Increase Model Card

### Basic Information

* **Person or organization developing model**: Melis Diken 'midiken@gwu.edu', Andrea Ho 'andreaho@gwu.edu', Hyemin Park 'hyemin0918@gwu.edu', Chanmi Shin 'chanmishin@gwu.edu'
* **Model date**: August, 2021
* **Model version**: 1.0
* **License**: MIT
* **Model implementation code**: [DNSC_6301_Example_Project.ipynb](DNSC_6301_Example_Project.ipynb)

### Intended Use
* **Primary intended uses**: This model is an *example* probability of default classifier, with an *example* use case for determining eligibility for a credit line increase.
* **Primary intended users**: Students in GWU DNSC 6301 bootcamp.
* **Out-of-scope use cases**: Any use beyond an educational example is out-of-scope.

### Training Data

* Data dictionary: 

| Name | Modeling Role | Measurement Level| Description|
| ---- | ------------- | ---------------- | ---------- |
|**ID**| ID | int | unique row indentifier |
| **LIMIT_BAL** | input | float | amount of previously awarded credit |
| **SEX** | demographic information | int | 1 = male; 2 = female
| **RACE** | demographic information | int | 1 = hispanic; 2 = black; 3 = white; 4 = asian |
| **EDUCATION** | demographic information | int | 1 = graduate school; 2 = university; 3 = high school; 4 = others |
| **MARRIAGE** | demographic information | int | 1 = married; 2 = single; 3 = others |
| **AGE** | demographic information | int | age in years |
| **PAY_0, PAY_2 - PAY_6** | inputs | int | history of past payment; PAY_0 = the repayment status in September, 2005; PAY_2 = the repayment status in August, 2005; ...; PAY_6 = the repayment status in April, 2005. The measurement scale for the repayment status is: -1 = pay duly; 1 = payment delay for one month; 2 = payment delay for two months; ...; 8 = payment delay for eight months; 9 = payment delay for nine months and above |
| **BILL_AMT1 - BILL_AMT6** | inputs | float | amount of bill statement; BILL_AMNT1 = amount of bill statement in September, 2005; BILL_AMT2 = amount of bill statement in August, 2005; ...; BILL_AMT6 = amount of bill statement in April, 2005 |
| **PAY_AMT1 - PAY_AMT6** | inputs | float | amount of previous payment; PAY_AMT1 = amount paid in September, 2005; PAY_AMT2 = amount paid in August, 2005; ...; PAY_AMT6 = amount paid in April, 2005 |
| **DELINQ_NEXT**| target | int | whether a customer's next payment is delinquent (late), 1 = late; 0 = on-time |

* **Source of training data**: GWU Blackboard, email `jphall@gwu.edu` for more information
* **How training data was divided into training and validation data**: 50% training, 25% validation, 25% test
* **Number of rows in training and validation data**:
  * Training rows: 15,000
  * Validation rows: 7,500

### Test Data
* **Source of test data**: GWU Blackboard, email `jphall@gwu.edu` for more information
* **Number of rows in test data**: 7,500
* **State any differences in columns between training and test data**: None

### Model Details
* **Columns used as inputs in the final model**: 'LIMIT_BAL', 'PAY_0', 'PAY_2', 'PAY_3', 'PAY_4', 'PAY_5', 'PAY_6', 'BILL_AMT1', 'BILL_AMT2', 'BILL_AMT3', 'BILL_AMT4', 'BILL_AMT5', 'BILL_AMT6', 'PAY_AMT1', 'PAY_AMT2', 'PAY_AMT3', 'PAY_AMT4', 'PAY_AMT5', 'PAY_AMT6'

* **columns used as targets in the final model**: 'DELINQ_NEXT'
* **Type of model**: Decision Tree Model
* **Software used to implement the model**: Python on colab, library(sklearn)
* **Version of the modeling software**: Python 3.6.9
* **Hyperparameters or other settings of your model**: Training, Validation & Test AUC, Asian-to-White AIR, Black-to-White AIR, Female-to-Male AIR, Hispanic-to-White AIR

### Quantitative Analysis
* **Metrics used to evaluate your final model**:
  * Area Under Curve (AUC)
    * Area under the ROC curve, which is a graph showing the performance of a classification model with the true positive rate and false positive rate (the probability that the model ranks a random positive example more highly than a random negative example)
    * Assesses performance of binary classification models (indicates accuracy of the model)
    * Should be between 0.5 - 0.95, with higher values being better
    * Measured for the training data, validation data, and test data respectively

  * Adverse Impact Ratio (AIR)
    * The ratio of the acceptance rate of the protected group to the acceptance rate of the controlled group of the dataset
    * Assesses the reliability of the model in terms of its ability to e biases in the process of deriving results
    * Should be greater than 0.8 to consider the bias of the model insignificant enough to make the model reliable

  * Data Partition
    * Assigned the following ratio for each process, giving a sufficient proportion to validation and testing to build a rigorous modeling process 
      * Training Data 50%
      * Validation Data 25%
      * Test Data 25%


* **State the final values of the metrics for all data: training, validation, and test data**:
As per the Jupyter notebook, the results for test used for our evaluation are as follows: 
* Training AUC: 0.78
* Validation AUC: 0.75
* Test AUC: 0.74
* Asian-to-White AIR: 1.01
* Black-to-White AIR: 0.85
* Hispanic-to-White AIR: 0.83
* Female-to-Male AIR: 1.03

* **Provide any plots related to your data or final model**:

![image](https://user-images.githubusercontent.com/89415811/131252295-0152d6f9-0c1a-4a1b-bd40-92749bab7626.png)

  * As shown in the iteration plot, the Validation AUC is the highest when the depth of the tree is at 6
  * The AIR for the controlled group (‘White’, ‘Male’) and protected group (‘Hispanic’, ‘Black’, ‘Asian’, ‘Female’) are all in an acceptable range (0.5-0.95) at the tree depth 6


### Ethical Considerations

**Biases**

Although biases are considered in the training process and tested so that it is minimized, it is extremely difficult to completely eliminate biases in the model. A decision tree, by its nature, only allows nodes with binary choices that must be expressed in numbers. This also applies to variables that are not numerical or cannot be quantitatively measured (e.g., race, gender, etc.), which means that the model could be trained to give preferable outputs for a specific type of group. In other words, the model still contains the risk of producing biased and inaccurate outputs that has the potential of impacting the evaluation of individuals, eventually leading to incorrect decisions.

**Data Security**

Another potential ethical issue of the decision model can be on data security. While it is important for the user of the model to put significant effort on protecting personal data, it is challenging to control external attacks on the data or model. Such attacks could be data poisoning, backdoors and watermarks, model inversion, adversarial, impersonation, etc. The reason these attacks are threatening and uncontrollable is because of the uncertainty of their occurrences: you can never know who, what, how, or when the data will be attacked. Therefore, decision-makers should always consider the possibility of such risks and be prepared with a safety net to protect the data and model.


