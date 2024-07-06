# Data Science Machine Learning

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-11-12

---

# 1.  Intro to Machine Learning (ML)

Machine learning is a subset of AI focused on a system that can learn from and make decisions, based on data. 

ML learn from past experiences (data) and improve performance over time by itself (no programmed). 

Core Components of ML:
- **Data:** Foundation of any ML model. `Labeled` (for supervised learning) or `Unlabeled` (for unsupervise learning). 
- **Algorithms:** Common ML algorithms includes linear regression, decision trees, neural networks, etc.
- **Model:** Outcome of training process. Takes input (data) and output (predictions or decisions)
- **Training:** Feeding data into algorithm to create a model.
- Inference: 

# 2.  General Process Behind Training a Model

What is a model? A model is a mathematical object that takes training data, learns a function mapping data to labels, and then is able to take in unlabeled data and assign them a label.

1. **Data Collection:** Gather relevant data from several sources.
2. **Data Preprocessing:** Data cleaning for analysis. 
3. **Feature Selection/Extraction:** Choose relevant features for the model.
4. **Model Selection:** Choose various algorithms for the model
5. **Training:** Train model with data to learn patterns btw input & output.
6. **Model Evaluation:** Testing model's performance with separate dataset.
7. **Hyperparameter Tuning:** Adjusting hyperparameters to optimize model perforance.
8. **Deployment:** Deploy model into production in a real-world application.
9. **Maintenance:** Regular updates and adjustments to enhance perforamnce over time.
 
# 3.  Supervised Learning

Supervised learning is a type of ML, where algorithms learn patterns from ***labeled data*** to make predictions or decisions. 

ML uses input-output pairs to train models, enabling them to predict outcomes based on new, unseen data. 

- Classification (categorizing data): Predicting discrete labels (e.g., spam or not spam).  
- Regression: Predicting continuous numerical values (e.g., house prices).
![](https://lh7-us.googleusercontent.com/LQRI_SHQPNIJ_TVxPeWpyoAddT6ZiXOAKg_gUnvuNej1zU1Or03kaKpltFNcNFqOrdIvC64S3VCgclU5J7dIGzvplBD8KsQOyyvRclglidLsZ-VStLc9ETUnFXtPtMBvnGVwYHFq9_iQiH0vXt9EMWo)

# 4.  K-Nearest Neighbors (KNN)

KNN's simple, non-parametric, lazy learning algo. used for ***classification*** and ***regression***. 
KNN identifies the `k` nearest data points to from a query point (input) to predict its label or value based on these neighbors. 

- Supervised Learning model, means the training data ***has labels***
	- i.e "Whether or not people paid back their loans"
	- deciding between categories called ***classification***
- KNN is an ***instance based model***, means requires stored training data to work.
- A ***hyperparameter*** is an argument to the model to tell how must behave


![](20231112182333.png)
#### Algorithm
- Find nearest `k` point to our new data
- Take weighted average of their labels based on euclidean distance
- Assign label
#### Strength
- Simple & Intuitive: Easy to implement & grasp classification algorithms
- Versatility: Useful for both ***classification*** and ***regression*** tasks.
- Non-parametric: Makes no assumption about underlying data distribution (versatil accross various types of datasets)
- No Traininig Period: KNN is lazy learner so no explicit training period involved. All traininig datasets are already stored, which enables instant learning.
#### Weakness
- Computationally Expensive: Poor performance on large datasets
- Sensitive to Outliers: Irrelevant features or outliers can influence KNN algo. bad, leading to misclassification
- Choosing Optimal K-Value: Selecting the right `k` value is challenging

## 4.1    Weighted KNN

Standard KNN treats all neighbors equally.
Weighted KNN assigns weight, closer neighbors will have greater influence on the output than those farther away
## 4.2    How to Choose K

Small `k` may lead to noise influencing result.
Large `k` may introduce bias towards the majority class.
Cross-validation techniques often used to choose best `k` for the dataset. 

- What if k=1? 
	- Model will be memorizing things (it'll just say whatever is closest). Model will lose ability to generalize.
- What if k=N? 
	- Soon, more and more irrelevant ponts will contribute, then we will just predict the mode of the data (frequent value).
- Try multiple Ks and get error rates. Pick the lowest! 
## 4.3    Different Distances Functions

- `Euclidean Distance`: Most common. Used for continuous variables. 
![](https://lh7-us.googleusercontent.com/84jo_GVSGu4HohpK3TGo8xvHHrGL26gXyRWaR8TXqJ6NagCZTs9bZFrsjWeqBOTeS9FOry1NOSdG9FMo0ZDMQPFzzHmBDFyVQxoFKj3-6qRwgY2dl7-S7bweLOZkSzZHSIElHZ2rBis-hXBiVGQJCEM)

- `Manhattan Distance`: Sum of absolute differences. Used for grid-like data.
![](https://lh7-us.googleusercontent.com/ZFxyOrjvR5si82QjP56WbEJTCI4QqRuFmXCuF7Doos1oSCcmT96hRVxHEBfsykfNc_7i154cRJvk7uM0B5o-6SagQqjjswB104jLRzPhdlQpjBaWNDAbp-3hnqB3r6xefHPz7SKxQ0-kBAZMutu4fdY)

- `Hamming Distance`: Given two binary strings. Counts the number of different bits. Used for strings. 
![](https://lh7-us.googleusercontent.com/h3NSQaM_fNAcL6-opbQJMB0X9dWj7VNTK1HKu11VvV7onOHsF8wizojexRDgmEVf00MVnxYIDLNxnSLNeXIBrHSCSnBy6XLQXJOgAB_JhgxABsxNjnyzk8xLCGOJfnfP928Mz318XN6J1WHaisAHUqk)

- `Minkwoski Distance`: Generalization of Euclidean and Manhattan distances.


## 4.4    Spherical K-Nearest Neighbors (SKNN)

Variation of KNN algorithm. Designed for datasets where underlying data distribution is spherical shape. SKNN attempts to find the smallest hypersphere that contains the K-nearest neihbor.

- Predefine spheres and let everything within the spheres "vote" 
- Save the trouble of searching all the points

![](20231112234342.png)

# 5.  Decision Trees
Decision Trees are ***supervised learning*** algorithm used for both classification and regression tasks (commonly for classification). Outdated but one of strongest algorithms, very simple, and not very good.

Structure of a Decision Tree:
- Root Node: Represents entire dataset
- Splitting: Process of splitting a node into "sub-nodes"
- Decision Node: After splitting a node, sub-node is called "decision node"
- Leaf: No further splitting nodes
- Pruning: Process of removing a sub-node from the tree

![](https://lh7-us.googleusercontent.com/xbNpU2MdMASzpACWmDfXifiPjxG_gTdD2kVDXlN2uyjJS2AlvtRS1sJiun6dBkbpPUg20jDC5baq2KM8KBwyA2A8wet6IMpzbY0KPSYpDHqIG5h9YZrz91m5q9SBSo4k2L5iLVlEukHe2f3Qorzy0CA)

### Strengths:
- Interpretability: Easy to understand and interpret, even for non-experts.
- Handling Non-Linear Relationships: Capture complex relationships between features.
- Classification and Regression: Used for both classification and regression tasks. In classification, decision trees help categorize data into different classes or categories, while in regression, they can predict a numeric value.
- Model Validation: initial modeling and rapid prototyping. Quickly build models to understand the dataset and check if the data has any meaningful patterns.
### Weaknesses:
- Overfitting: Prone to overfitting when complex trees
- Instability: Small changes in data can lead to a different tree
- Biased Trees
- Not Ideal for Continuous Variables

## 5.1    Decision Tree Training Algorithm 

1. Start at Root: Begin with all training examples at the root node 
2. Select Attribute: Identify the best attribute that best splits the data 
3. Create Branches: for each possible value of this attribute
4. Split data: Split dataset into subset, each containing data with the same value for the attribute
5. Recursive Processing
6. Stopping condition: when all nodes have the same instance, no remainig attributes, or no instances are left.

In decision trees, smaller is better:
- Fewer rules: More generalization
- Many rules: More specificity
- We want to use as few rules as possible to classify our data.

To use a decision tree:
- First, go thru ***training phase*** where tree decides on all its possible splits
- Use training for ***classification***, where model takes ***unlabeled data*** and provides label for it

When to use decision trees:
- When want to explain ML to someone
- When want a general sense of your data

When to NOT use decision trees:
- When have actual problem to be solve. 
- In other worlds, do not use for real world scenarios

## 5.2     Entropy

Entropy is a measure of the randomness or impurity in the dataset.
Higher entropy means less predictable, more information.
Lower entropy means more predictable, less information.

Entropy and Information Gain are used to determine which feature/attribute gives the best split at each step.
- Entropy Calculation: Entropy quantifies the impurity or randomness in the data
- Information Gain measures the quality of a split:
	1. Calculate entropy for entire dataset (before split)
	2. For each split, calculate entropy of each group formed by the split and calculate the weighted sum of these entropies.
	3. Substract weighted entropy (after split) from original entropy (before split) to get `information gain`

The attribute with the highest information gain is chosen for the split at each node in the tree.

![](https://lh7-us.googleusercontent.com/AF6JHJ9FYru_pgXRsb7__jc2vzyLRReVxkroJGgwv5sBCQqX00ZG4mbm8Y0bzcSwqRNECWbpZp6gVOUwVr5tN9uk0WqCdoObFSZ1F_0LOCxJqWPsVdGjYLnF0vU6j0YGKsDOoYAjFvIxTcLo_vER2Co)



# 6.  Feature Engineering

Process of creating, modifying, or selecting columns (features) in the dataset to enhance the perfomance of ML models.

Generally, models don't like categorical data and don't do well. So feature engineering produce new features with the goal of simplifying data for ML models.

## 6.1     One-Hot Encoding

Technique that converts categorial variables into numerical format, binary (0 or 1) vectors, so ML can work with more efficiently.

Each categorical column becomes a binary column, where `1` indicates presence and `0` abscence

**Example**:
Column with categorical data has different colors (red, blue, green).
One-hot encoding a binary column for this category
- Red: [1,0,0]
- Blue: [0,1,0]
- Green: [0,0,1]

![](https://lh7-us.googleusercontent.com/NX8YRIvA4zauY119Lq5AcifTbiwbI2fBjAhw2ztX8-KMg19fRBQEQsfcIr7dDa8xZ9xCvglsV3mTCVWWMMD9lW-SswW_Jcp1wjoq5qf0J2AkLHTFz7WnIoC9FWP7LR4GjKDJpxAttBTAWWW72kAuCls)

#### Upside & Downsides
- Upside: Enables the use of categorical variables in ML models.
- Downsides: Can lead to high-dimensional dataset if many categories.

## 6.2    Transformation

Sometimes, we create a new column by applying a function over a column!
Transforms can be ***linear*** or ***non-linear***. 

There are 3 types:

#### Normalization: 
- Rescales the data to a range of 0 to 1 (values fall within this range), making ML algorithms to work easier with data

![](https://lh7-us.googleusercontent.com/UnENipz7iaE6kKB4sDnkFiEQH5JuwXucY2B04z_sgDP2EUhMkh1X1MYdcAKkbmeWi0tbzRMaVGbbS6YE-yF7U_ye8OSNeA_cbT17l7vzGvG3Ff_MMrggcoKAGgbOtUBpxvcXZzydH5ZXd08m_Q36jEI)

#### **Standardization:** 
- Transforms data to have mean of `0` and Standard Deviation of `1`.
- Center the data around 0, easier to compare different features.
- Less sensitive with outliers, preferable than normalization
- Useful when distribution of the data is unknown

![](https://lh7-us.googleusercontent.com/E0LSYCbzOyTaiAYTn1BVKzAZh75MCIbebglyxLwHPFFMadxAoz13qKwNHKtjim9Q-06TNdy3xyXEubEYngndUI5KnvU86o9SMW-Ce-DvF_xUo_8uzdzTyafwplJcvb_TLb6sQElCn1ap2jFAmRAKTiE)

#### Log Transforms:
- Used to reduce skewness in a distribution, making data more symmetrical.
- Make data more suitable for analysis techniques that assume normal distribution

![](https://lh7-us.googleusercontent.com/yH0-Jn2ywYNNHFeQ2Qy3BZSrLqtQzx9invWzmHl9ndEIrudJmORVCV7-21qp1druxUCIZhPoJwQ6bBjw1yQhNrb36KCZmErozigoA2cPgTO5EIz-qStA9KLjDgfSpdy0OzEM3LJbtXJRrXrsMZE25Kk)

## 6.3    Principal Component Analysis (PCA)

PCA is a dimensionality reduction techinique used in ML and statistics.
**PCA is effective for reducing the dimensionality of large datasets while retaining as much variance as possible.**

#### Covariance: 
- It's a measure of the joint variability of two random variables. In PCA, covariance between different variables in the dataset is calculated to identify the relationships among them.

#### Purpose:
- PCA is ***employed to reduce the number of dimenssions or features in a dataset while preserving its key characteristics.***

#### Upsides: 
- **Dimension Reduction:** PCA reduce the number of features, retains essential info.
- **Noise Reduction**
- **Visualization:** PCA simplifies into 2D or 3D for better visual understanding
- **Feature Transformation:** transform features to orthogonal comp., reveals hidden patterns
- **Feature Selection:** PCA ranks principal components, helping feature selection

#### Downsides:
- **Linearity**: PCA assumes straight-line relationships (no always the case).
- **Interpretability:** Hard to Interpret principal components
- **Loss of Information:** Loss of information since PCA prioritizes variance
- **No Feature Learning:** PCA doesnt create new features; works with what's already there

## 6.4    K-Means

An ***unsupervised learning*** algorithm.

Aimed to partition of `K` cluster, minimizing the sum of squared distances between data points and their assigned cluster centroids.

The goal is to group similar data points together and discover underlying patterns. To achieve this objective, K-means looks for a fixed number (k) of clusters in a dataset.

![](https://lh7-us.googleusercontent.com/5p7L0YtI_GOmRT0lmsfrurq91sXrvUCpXAf0l72rDqnBfVY40UoZt212EREd9eGYIWDi70GzCNC7T7fJUWBS4NGgRbPcwjsEzxuZ2DhqtOdTTNpTEGlVO3T6ER2632Q9fW12gfzUnQJYLbXX00FRtNw)


![](https://lh7-us.googleusercontent.com/ufRCwDBvIoidDGKNV5KPcjWCkiqUbK6wipnOUigq7LvRrDLyo0nUiqUfHFN31xk4WqT5gqik9GYlofukYfgllo41d9p4Y8cIT_0SQ1wuFvdVfNOuToXWiTJHfCLw-DdrPx2r8nz41aoYuGX7ugVLrCw)

## 6.5    Binning

Binning takes a continuous feature and introduces a column that categorize it.
Used when there are boundaries in the data that are not obvious, or to simplify the representation of continuous variables.

![](https://lh7-us.googleusercontent.com/2M8f-0oQDjWbwOryZ83PDoWsj_D0ufKfSKh3Qlif8Y7ooBlATabgBOsqJXz84zJ8xIGGD0PIIytGmYT-FX4oORhNW9g9jfMcsZcEWjjtwrw7A-_rl23qNsAYy3g16vvmFxcfoLvYfnE0yhHveavCS2Y)

![](https://lh7-us.googleusercontent.com/Ptp1JAXNfXA4OhVTSQE6anEJgWZ9Pi306TVvlKlh-8ZFZ-BjWzNvsrF47npdS95UavbCf_zkq4ffhOyedfCxxdR3t3EV0T3vDNx8Znz8vyaXjyrwc5W-bbBhmvlzJOgXWrLqydg0Mc-ISgoJ2Y29H44)

# 7.  Classification

***Supervised learning*** task where model is trained to categorize data points into predefined categories

Goal is to predict discrete labels (e.g whether email is spam or not)
## 7.1   Overfitting

When the model becomes too tuned on the training set that becomes unable to ***generalize*** (not effective on new unseen data).

**Example:** "Taking a practice exam over and over and doing really well because you've already taken it."
- An overfit model will have a high accuracy on the training data, but low accuracy in real life
## 7.2   Underfitting

When model becomes too ***general***. Model memorized one rule and is applying it everywhere. Unable to capture the underlying pattern data and performs poorly on both training and new data.

Happens when model does not have enough parameters or complexity to learn from data.

**Example:** "College admission process only looking at GPA."
## 7.3    Naive Bayes

Naive Bayes relies on Baye's theorem and used for classification tasks in Natural Language Processing (NLP), specifically text categorization, spam filtering, sentiment analysis, and recommendation systems. 

Aims to assign the most likely class label to a particular instance by calculating the prob. of that label given the input features.  Calculates the prob. of a class given the features, assuming all features are conditionally independent, hence the term "naive".

![](20231113153755.png)

## 7.4    Support Vector Machine (SVM)

SVM is a ***supervised learning*** algorithm used for classification and regression tasks.

Aims to find the decision boundary (hyperplane) that best separates data points into different classes. 

Popular in various fields, such as text classification, image recognition, and biometrics due to their capability to handle complex data distributions. 
#### Upsides: 
- Effective in high-dimensional spaces
- Versatile due to different kernel functions that help capture complex relationships in the data.

#### Downsides:
- Computationally intensive for large datasets.
- Choosing the right kernel function and tuning its parameters can be challeging.

![](20231113160220.png)

## 7.5    Random Forest

Random Forest is an ensemble learning method based on decision trees. Effective for classification.

Creates multiple decision trees and merges their predictions to improve accuracy and avoid overfitting. (it does not handle missing data).

Random forest used in medicine for disease prediction, finance for stock market forecasts, marketing for customer behavior analysis, environmental science for species identification, image, speech recognition
#### Upsides: 
- Handles overfitting well
- High accuracy and robustness
- Good performance on many problems, including non-linear

#### Downsides:
- Computationally intensive with large number of trees
- Does not handle missing data

![](20231113163905.png)

# 8.  Evaluation

Evaluation in ML involves assessing the performance of a model, understanding its effectiveness and applicatiblity to real-wolrd scenarios.

## 8.1     Precision

Measures ***how many of the things we classified as positive were actually positive***.
We use precision when we only care about being correct on things we identify as positive.

**Example:** "Google does not care if lay off 1000 good enginers; Google just wants to make sure the ones it hires are good enough."

![](https://lh7-us.googleusercontent.com/WXs31v_etmIctYGY0iGTgSWqwqoqXCXZHqhiOYW0odO4zYQXYxF_DMj-zSWaNVg0FSflMyCtsxeRiMVlJ8cuZCJe5TTyY0QG_Y7jwGUEopsBDzYOHSJaBKjr3WDxYAWt5xqKhmAXWDTw502biSevCWA)


## 8.2    Recall

A metric used in ML to evaluate the perfomance of a classification model.
Recall measures the ability of the model to find all relevant instances within a dataset.
It's the proportion of actual positives that are correctly identified.

***Use Recall when want to make sure we don't miss anything. Situations where missing any actual positive case can be critical.***

**Example:** 
- "Identifying people contagious with a deadly super plague" 

![](https://lh7-us.googleusercontent.com/w2RCcNTz33CnEkrZzGhQ60XHO2TF3CAxzMg_DNyqRMPN4P_FJMlrMyRJeLQPfxNRJycjO7toUVCKI-nfCR0wkh5x-vlpon4iC25DgrBFeqLk-fdX5zXxZ-oPAQBnstIALmStPUxhCbtsxbdTbFlHkYs)

![](https://lh7-us.googleusercontent.com/dv4-2M69dOrSE6Eh9kpPCqeiGBHT0v8jdl5oDZrU2xZMm-zgx_YfGSgVuQnqNIl-TtgQPRJuPBXAuORekrMFvJabg6Nrt_DmyFBsVdLx7HDVcP05IyvDOnq7W6XKhFDMjVn9d3ln6MVdteBhVamOz88)

**Key Notes:** 
- **True Positive (TP):** Instances that are correctly predicted as positive.
	- "A diagnostic model predicting a ***sick*** person ***DOES have disease***. True, hence true positive"
- **True Negative (TN):** Instances that are correctly predicted as negative.
	- "A diagnostic model predicting a ***healthy*** person ***DOES NOT have a disease***. true, hence True negative"
- **False Positive (FP):** Instances that are incorrectly predicted as positive (false alarm).
	- "A diagnostic model predicting a healthy person DOES have a disease. Person is not sick, hence false positive"
- **False Negative (FN):** Instances that are incorrectly predicted as negative (missed detection).
	- "A diagnostic model predicting a person DOES NOT have a disease. Person is sick, hence false negative"

## 8.3    Confusion Matrix

A confusion matrix is a table used to summarize performance of a classification model on a test dataset. 

4 different outcomes: true positive (TP), false positive (FP), true negative (TN), false negative(FN).

![](20231113174616.png)


## 8.4    Overfitting vs Underfitting

![](20231113180412.png)

## 8.5    Log Loss

A measure of accuracy that penalizes overconfidence.
![](https://lh7-us.googleusercontent.com/FfGvjeSpMzkJXMctJaXnOGPV8KFCQ9YGDAoswiN_DWIMrtxfeU3UP6g-3Vc-vMMHC4TmTI-Lv5cHuzYAiknC08WJQWAHeJMqaHtIRxmxoFh5Gqb0pP24WgXDibBiaMjfC2gYuyH5dE8I0YdjNDSNZio)


# 9.  Regression

A branch of ***supervised learning*** distinct from classification.


**Regression vs Classification:** 
- Classification predicts what category a datapoint belongs to.
- Regression takes input data and predicts a real valued feature.
![](20231113183113.png)

## 9.1    Linear Regression

One of the most important algorithms in ML.
A ***supervised learning*** task where the model is trained to find relationships between one or more variables (independent) vs one dependet variable by establishing a “best fit” line through the data.

It measures the relationships between one or more independent (input) variables and a dependent (outcome) variable.

**Why find that line?**
- **Best Fit:** line accurately fits the data
- **Minimizes the error:** “predicted values” and “actual values” differences are reduced.    
- **Captures relationships:** shows relationships between variables for accurate predictions

**Example:** 
- "Using years of experience to predict salary"
- "Area size to predict house price"

## 9.1.1       Loss Function

The Loss Function goal in Linear Regression is to find the **line that minimizes the average distance from each data point to the line.**

## 9.1.2      Mean Squared Error (MSE)

MSE quantifies the total error between the predicted and observed values across all data points.

By minimizing the MSE, ***the linear regression algorithm can determine the optimal coefficients (slopes and intercepts) for the line, leading to “best fit” possible.***

## 9.1.3      R-Squared (R^2)

R-squared is a statistical measure that determines the “goodness” of our regression model.

![](https://lh7-us.googleusercontent.com/9FmRjw_u2ls0ulX_nEcQyf-rXTNe_Faf4AHvDSy_U_TFiqg2RSjaoLlprg0kuk-SQYa52d64l4Sm5B4_qWCZKiFwYtriTHMFjkbggkNoGZNW0rEZbq8mTNDV-Du5-Z4lI9L0QAAH_7XUCDurxItw6vs)


Typically ranges between 0 and 1. Shows how well our line fits the data. 
Higher R-squared value indicates a better fit of the model to the data.

![](https://lh7-us.googleusercontent.com/nvkLkLXuBFztfTr9ASx4Axntx2l30LWzGXovyKrZ1yjbhrYLtgUtsMJdkmFCx-UK6JP8cy1R4hyiUqf1alI6mWSnpvm1WKP7LWsHK4xbv0SkvyGx-5zopPCZnCOFJBg6Pnh3IgEkLmBOS4oa43dkPMY)

# 10.  Neural Networks

Neural networks are computational models in AI; mimic the brain's interconnected structure.

Consist of interconnected nodes or neurons arranged in layers.

![](20231113202346.png)

They process data (input) and make predictions or decisions (output) by learning from the data.

## 10.1     Building Blocks: Neurons

Basic Unit: 
- Neuron is the basic unit of a neural network. 
- It can take multiple signals and produces output

Functionality:
- Each input is mutiplied by a weight
- Weigthed inputs are sum together
- Sum is passed thru activation function

Activation function:
$$
y = f(x_{1} * w_{1} + x_{2} * w_{2} + b)
$$

![](20231113203248.png)



## 10.2    Neural Network Structures

Neural networks are made up of nodes (units) connected by links. Typically, includes one or more hidden layers (layers between input and output layer).

In most deep neural networks, the flow of data is unidirectional (one direction), from input to output.

![](20231113203816.png)


## 10.3    Perceptron Algorithm

Perceptron is one the earliest neural network models (1950s), set up for image processing.
Unidirectional single-layer neural network (no hidden layer).

Perceptron algorithm uses a linear classifier that takes a multi-dimensional, real valued input `X`, and learns a series of weights, `w`.

$$
w_{1} x_{1} + w_{2} x_{2} + \dots + w_{n} x_{n} + bias > 0
$$

Key notes:
- `Weight` represents the strength of connections between neurons in different layers
- Activation classifies the input as positive or negative based on the `summation and bias`

![](20231113205425.png)


## 10.4    Backpropagation

Backpropagation is the algorithm by which neural networks are trained.
Adjust each weight in the network based on its contribution to the error in the output.

**Forward Pass:**
- Input data is passed forward through the network, producing an output prediction

**Calculating Error:**
- The predicted output is compared to the actual expected output, 
- Calculates the error or loss

**Backward Pass:**
- Error is propagated backward through the network.
- Adjustment are made to the network's internal parameters (weights and biased) based on the calculated error
- Aims to minimize the difference between the predicted and actual ouput

![](20231113210301.png)


# 11.  Image Processing

A colorful image has 3 channels: red, green, blue
The image is divided into pixeles
A pixel represents one color

## 11.1      Convolutional Neural Networks (CNN or ConvNet) 

CNN are a class of neural networks that specializes in processing data with grid-like structures, such as images (pixeles x pixeles)

A CNN typically has three layers: convolutional layer, pooling layer, fully connected layer.

#### Hidden Layers

Hidden Layers are those that exist between the input and output layers.
It can include: convolutional layer, pooling layer, fully connected layer.

#### Convolution Layer

Fundamental component of CNNS.
It extracts features by applying a set of learnable filters (kernel) to the input data

![Intuitively Understanding Convolutions for Deep Learning | by Irhum Shafkat  | Towards Data Science](https://miro.medium.com/v2/resize:fit:1358/1*Fw-ehcNBR9byHtho-Rxbtw.gif)

Performs a dot product between two matrices. 
The kernel is spatially smaller than an image but is more in-depth.

![](20231113224725.png)



#### Kernel

Kernel is a matrix, which is slid across the image multiplied by the input, so ouput is enhanced in a desirable manner.

![](20231113225506.png)

*As kernel moves accross the image data, it covers different regions, allowing to extra features and info within the input*

![](20231113225144.png)


#### Activation Map (Output)

Produced by the movement of the kernel, representing the response at each spatial position.

![](20231113225506.png)

#### Stride

Refers to the step size the kernel moves across the input, affecting the coverage and overlap in convolution.

![](20231113230316.png)

#### Rectified Linear Unit (ReLu) Function

Added after the convolutional layer in CNN.

Introduces non-linearity to the network, essential for learning complex patters and relationships within the data.

Simple linear function (output equals input for positive values, 0 for negative values) allows the network to model non-linear relationships in the data.

![](20231114005631.png)

#### Pooling Layers

Pooling layers is a component in CNN that follows convolutional layers. 

**Purpose:**
- Its goal is to downsample the spatial dimension of the feature maps, 
- reducing computational load, and 
- extracting dominant features effectively.

**Types of Pooling:** 
- Max Pooling (retains max value in each region)
- Average Pooling (calculates the average value)
- Sum Pooling (finds the sum of values in each region)

![](20231114010801.png)

#### Final Layer

Fully connected layer (dense layers) and an output layer that perform the final classification decission. They take the high-level features learned by earlier layers and make predictions about the input.

![](20231114011008.png)

#### The NN Architecture

![](20231114011415.png)

#### Training Process
- Show the NN `n` pictures (`n` is your batch size)
	- batch size too big, NN will underfit
	- Too small will overfit
- Use the backpropagation algorithm
- Repeat until NN loss stops decreasing

#### Use in Data Science

Generally, we don't design/train own Neural Network.
As a DS, we use either predefined models, or **transfer learning**

Transfer learning uses an already pre-trained NN to learn to do a novel image classification problem.


