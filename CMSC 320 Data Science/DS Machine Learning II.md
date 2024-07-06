# Final Exam Review

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-12-15

---

# 1.  Experimental Design

The process of planning a study to meet specified objectives. In data science, it's about structuring an experiment to obtain data that can be analyzed to draw valid conclusions.

### 1.2    Optimization Criteria and Proxy Measures

- **Optimization Criteria**: Specific goals or objectives that an organization, project, or process seeks to achieve.
- **Proxy Mea
sures:** They are stand-ins for variables you can't directly measure. For example, in e-commerce, customer satisfaction might be indirectly measured through repeat purchase rates.
- **Goodhart's Law:** This law states that once a measure becomes a target, it ceases to be a good  measure. It warns against over-relying on specific metrics as targets, as they can lead to unintended consequences. If you create a **proxy measure** for the criteria you want to optimize, eventually that proxy measure will _become_ the thing you’re optimizing for
**Example:** Amazon
Optimization Criteria: Maximize product sales.
Proxy Variable/Measure: Number of products sold
Goodhart's Law: Sellers might prioritize selling low-quality or irrelevant products to increase the proxy measure (products sold) rather than focusing on actual customer satisfaction or revenue.

- **Confounding Variable:** variables that can influence the relationship between the independent variable (IV) and the dependent variable (DV) in a research study.
**Case Example 1: Smoking and Lung Cancer**
- Research Question: Does smoking cigarettes cause lung cancer?
- Confounding Variable: Age
- IV: Smoking
- DV: Cancer
In this case, age is a confounding variable. Older individuals are more likely to have smoked for a longer duration compared to younger individuals. Lung cancer incidence also increases with age. Without accounting for age as a confounder, it might falsely appear that smoking causes lung cancer when, in reality, age is the confounding variable influencing both smoking behavior and lung cancer risk.

### 1.3    Type of Experiments

#### Observational Studies

Measure members of sample without trying to affect them.
- **Cross-Sectional**: Observe data at a single point in time. For instance, a survey assessing dietary habits across different age groups.
- **Retrospective**: Past data is used to investigate outcomes. For example, examining patient records to study the effectiveness of a treatment.
- **Prospective**: Follow and observe group closely. A study tracking a group's exercise habits over a year is an example.

![](20231215010411.png)

#### Controlled Experiments

- **Structure**: Involves manipulating one variable to see its effect on another while keeping other variables constant. It typically includes treatment and control groups.
- **Importance of Control**: Helps in isolating the variable of interest and minimizing the impact of confounders.
- **Synthetic Data**: This is artificially generated data that mimics real data. It's useful when actual data is not available due to privacy or other constraints.

### 1.4    Designing an Experiment

Steps:
1. Define the problem and objectives.    
2. Design the experiment (determine variables, groups, methods).
3. Identify potential problems and errors.
4. Collect and analyze data.
5. Controlling for Variables: Essential to minimize the effects of external factors. Methods include blinding (where subjects don't know which group they are in) and using placebos.

- **Randomization**: Random assignment of subjects to groups helps in reducing bias and ensuring each group is similar.
- **Replication**: Conducting the experiment multiple times to verify results.


# 2.  Hypothesis Testing

A method used to make informed decisions based on sample data (e.g subset of population data). 

### Key concepts:

- **Outliers:** is a data points that is very extreme compare to the rest of data points (e.g A billionare with high income while the majority data points has moderate income)
- **Mean:** is the average of data. Sensitive to outliers (e.g extreme values in data (very high income or very low incomes) can disproportionately influence the mean)
- **Median:** is middle value when data arranged ascending or descending order. Robust to outliers (not affected by extremes values). It provides a better representation of a "typical"  value when there are outliers.
- **Standard Deviation:** how spread out the values are from the mean (average) of the data
-  **Mode:** is a value that appears more frequently in a dataset. Number witht the heighest frequency (e.g most common category such as eye color in a population)


- **Null Hypothesis:** A statement to be tested with no effects (Ho)
- **Alternative Hyposthesis:** A statement to adopt in the situation in which evidence(data) is strong so H0 is rejected (there is significant difference).
```Example
"Medical Research on Blood Presure"

Null Hypothesis Ho: There is no significant difference in blood pressure between the group that takes Medication A and the group that takes a placebo

Alternative Hypothesis Ha: There is a significant difference in blood pressure between the groups ...
```

- **P-Values:** A small p-value is often interpreted as an indication of statistical significance. Meaning, in favor of alternative hypothesis

- **True Positive (TP):** Instances that are correctly predicted as positive.
	- "A diagnostic model predicting a ***sick*** person ***DOES have disease***. True, hence true positive"
- **True Negative (TN):** Instances that are correctly predicted as negative.
	- "A diagnostic model predicting a ***healthy*** person ***DOES NOT have a disease***. true, hence True negative"
- **False Positive (FP):** Instances that are incorrectly predicted as positive (false alarm).
	- "A diagnostic model predicting a healthy person DOES have a disease. Person is not sick, hence false positive"
- **False Negative (FN):** Instances that are incorrectly predicted as negative (missed detection).
	- "A diagnostic model predicting a person DOES NOT have a disease. Person is sick, hence false negative"

### 2.2    Type I and Type II Errors

**Type I Error (false positive):** Rejecting a true Null Hypothesis
**Type II Error (False Negative):** Fail to reject a false Null Hypothesis

#### Example
```
Testing wether a new drug is effective in reducing blood pressure

Ho: drug has no effect on blood pressure.
H1: drug reduces blood pressure.
```
**Type I error**: concluding drug is effective at reducing blood pressure when reality has no effect (assuming null hypthesis is true, rejecting leads to an error of Type I).
**Type II error**: failing to detect drug is effective when, in fact, it does reduce blood pressure (assuming null hypothesis is false, failing to reject this is a Type II).

### 2.3    Tests Types

- **T-test:** Used for **SMARLLER SAMPLE SIZE** (n < 30). Don't know standard deviation. Use if data is normally distributed and have small number of samples
- **Z-test:** Used for **LARGE SAMPLE SIZE** (n > 30) and know the population **STANDARD DEVIATION**. Use if data is normally distributed and large number of samples.
- **Chi-Squared Test For Independence**: Data Type Categorical. Appropiate when both variables are categorical. Used to test independence between two categorical variables
- **Anova:** Used for comparing **MEANs** of different groups (more than two) to see differences among them. It only indicates that the difference exists in the group


# 3.  Intro to Machine Learning (ML)

Machine learning is a subset of AI focused on a system that can learn from and make decisions, based on data. 

ML learn from past experiences (data) and improve performance over time by itself (no programmed). 

Core Components of ML:
- **Data:** Foundation of any ML model. `Labeled` (for supervised learning) or `Unlabeled` (for unsupervise learning). 
- **Algorithms:** Common ML algorithms includes linear regression, decision trees, neural networks, etc.
- **Model:** Outcome of training process. Takes input (data) and output (predictions or decisions)
- **Training:** Feeding data into algorithm to create a model.
- Inference: 

### 3.1    General Process Behind Training a Model

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
 
### 3.2  Supervised Learning

Supervised learning is a type of ML, where algorithms learn patterns from ***labeled data*** to make predictions or decisions. 

ML uses input-output pairs to train models, enabling them to predict outcomes based on new, unseen data. 

- Classification (categorizing data): Predicting discrete labels (e.g., spam or not spam).  
- Regression: Predicting continuous numerical values (e.g., house prices).
![](https://lh7-us.googleusercontent.com/LQRI_SHQPNIJ_TVxPeWpyoAddT6ZiXOAKg_gUnvuNej1zU1Or03kaKpltFNcNFqOrdIvC64S3VCgclU5J7dIGzvplBD8KsQOyyvRclglidLsZ-VStLc9ETUnFXtPtMBvnGVwYHFq9_iQiH0vXt9EMWo)

### 3.3    K-Nearest Neighbors (KNN)

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

#### Weighted KNN

Standard KNN treats all neighbors equally.
Weighted KNN assigns weight, closer neighbors will have greater influence on the output than those farther away
#### How to Choose K

Small `k` may lead to noise influencing result.
Large `k` may introduce bias towards the majority class.
Cross-validation techniques often used to choose best `k` for the dataset. 

- What if k=1? 
	- Model will be memorizing things (it'll just say whatever is closest). Model will lose ability to generalize.
- What if k=N? 
	- Soon, more and more irrelevant ponts will contribute, then we will just predict the mode of the data (frequent value).
- Try multiple Ks and get error rates. Pick the lowest! 
#### Different Distances Functions

- `Euclidean Distance`: Most common. Used for continuous variables. 
![](https://lh7-us.googleusercontent.com/84jo_GVSGu4HohpK3TGo8xvHHrGL26gXyRWaR8TXqJ6NagCZTs9bZFrsjWeqBOTeS9FOry1NOSdG9FMo0ZDMQPFzzHmBDFyVQxoFKj3-6qRwgY2dl7-S7bweLOZkSzZHSIElHZ2rBis-hXBiVGQJCEM)

- `Manhattan Distance`: Sum of absolute differences. Used for grid-like data.
![](https://lh7-us.googleusercontent.com/ZFxyOrjvR5si82QjP56WbEJTCI4QqRuFmXCuF7Doos1oSCcmT96hRVxHEBfsykfNc_7i154cRJvk7uM0B5o-6SagQqjjswB104jLRzPhdlQpjBaWNDAbp-3hnqB3r6xefHPz7SKxQ0-kBAZMutu4fdY)

- `Hamming Distance`: Given two binary strings. Counts the number of different bits. Used for strings. 
![](https://lh7-us.googleusercontent.com/h3NSQaM_fNAcL6-opbQJMB0X9dWj7VNTK1HKu11VvV7onOHsF8wizojexRDgmEVf00MVnxYIDLNxnSLNeXIBrHSCSnBy6XLQXJOgAB_JhgxABsxNjnyzk8xLCGOJfnfP928Mz318XN6J1WHaisAHUqk)

- `Minkwoski Distance`: Generalization of Euclidean and Manhattan distances.


### 3.4    Spherical K-Nearest Neighbors (SKNN)

Variation of KNN algorithm. Designed for datasets where underlying data distribution is spherical shape. SKNN attempts to find the smallest hypersphere that contains the K-nearest neihbor.

- Predefine spheres and let everything within the spheres "vote" 
- Save the trouble of searching all the points

![](20231112234342.png)

# 4.  Feature Engineering

Process of creating, modifying, or selecting columns (features) in the dataset to enhance the perfomance of ML models.

Generally, models don't like categorical data and don't do well. So feature engineering produce new features with the goal of simplifying data for ML models.

## 4.1     One-Hot Encoding

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

## 4.2    Transformation

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

## 4.3    Principal Component Analysis (PCA)

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

## 4.4    K-Means

An ***unsupervised learning*** algorithm
Aimed to partition of `K` cluster, minimizing the sum of squared distances between data points and their assigned cluster centroids.

![](https://lh7-us.googleusercontent.com/5p7L0YtI_GOmRT0lmsfrurq91sXrvUCpXAf0l72rDqnBfVY40UoZt212EREd9eGYIWDi70GzCNC7T7fJUWBS4NGgRbPcwjsEzxuZ2DhqtOdTTNpTEGlVO3T6ER2632Q9fW12gfzUnQJYLbXX00FRtNw)



# 5.  Evaluation

Evaluation in ML involves assessing the performance of a model, understanding its effectiveness and applicatiblity to real-wolrd scenarios.

## 5.1     Precision

Measures ***how many of the things we classified as positive were actually positive***.
We use precision when we only care about being correct on things we identify as positive.

**Example:** "Google does not care if lay off 1000 good enginers; Google just wants to make sure the ones it hires are good enough."

![](https://lh7-us.googleusercontent.com/WXs31v_etmIctYGY0iGTgSWqwqoqXCXZHqhiOYW0odO4zYQXYxF_DMj-zSWaNVg0FSflMyCtsxeRiMVlJ8cuZCJe5TTyY0QG_Y7jwGUEopsBDzYOHSJaBKjr3WDxYAWt5xqKhmAXWDTw502biSevCWA)


## 5.2    Recall

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

## 5.3    Confusion Matrix

A confusion matrix is a table used to summarize performance of a classification model on a test dataset. 

4 different outcomes: true positive (TP), false positive (FP), true negative (TN), false negative(FN).

![](20231113174616.png)


## 5.4    Overfitting vs Underfitting

![](20231113180412.png)

## 5.5    Log Loss

A measure of accuracy that penalizes overconfidence.
![](https://lh7-us.googleusercontent.com/FfGvjeSpMzkJXMctJaXnOGPV8KFCQ9YGDAoswiN_DWIMrtxfeU3UP6g-3Vc-vMMHC4TmTI-Lv5cHuzYAiknC08WJQWAHeJMqaHtIRxmxoFh5Gqb0pP24WgXDibBiaMjfC2gYuyH5dE8I0YdjNDSNZio)



# 6.  Classification

***Supervised learning*** task where model is trained to categorize data points into predefined categories

Goal is to predict discrete labels (e.g whether email is spam or not)
## 6.1   Overfitting

When the model becomes too tuned on the training set that becomes unable to ***generalize*** (not effective on new unseen data).

**Example:** "Taking a practice exam over and over and doing really well because you've already taken it."
- An overfit model will have a high accuracy on the training data, but low accuracy in real life
## 6.2   Underfitting

When model becomes too ***general***. Model memorized one rule and is applying it everywhere. Unable to capture the underlying pattern data and performs poorly on both training and new data.

Happens when model does not have enough parameters or complexity to learn from data.

**Example:** "College admission process only looking at GPA."
## 6.3    Naive Bayes

Naive Bayes relies on Baye's theorem and used for classification tasks in Natural Language Processing (NLP), specifically text categorization, spam filtering, sentiment analysis, and recommendation systems. 

Aims to assign the most likely class label to a particular instance by calculating the prob. of that label given the input features.  Calculates the prob. of a class given the features, assuming all features are conditionally independent, hence the term "naive".

![](20231113153755.png)

## 6.4    Support Vector Machine (SVM)

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

## 6.5    Random Forest

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


# 7.  Regression

A branch of ***supervised learning*** distinct from classification.

**Regression vs Classification:** 
- Classification predicts what category a datapoint belongs to.
- Regression takes input data and predicts a real valued feature.
![](20231113183113.png)

## 7.1    Linear Regression

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

## 7.1.1       Loss Function

The Loss Function goal in Linear Regression is to find the **line that minimizes the average distance from each data point to the line.**

## 7.1.2      Mean Squared Error (MSE)

MSE quantifies the total error between the predicted and observed values across all data points.

By minimizing the MSE, ***the linear regression algorithm can determine the optimal coefficients (slopes and intercepts) for the line, leading to “best fit” possible.***

## 7.1.3      R-Squared (R^2)

R-squared is a statistical measure that determines the “goodness” of our regression model.

![](https://lh7-us.googleusercontent.com/9FmRjw_u2ls0ulX_nEcQyf-rXTNe_Faf4AHvDSy_U_TFiqg2RSjaoLlprg0kuk-SQYa52d64l4Sm5B4_qWCZKiFwYtriTHMFjkbggkNoGZNW0rEZbq8mTNDV-Du5-Z4lI9L0QAAH_7XUCDurxItw6vs)


Typically ranges between 0 and 1. Shows how well our line fits the data. 
Higher R-squared value indicates a better fit of the model to the data.

![](https://lh7-us.googleusercontent.com/nvkLkLXuBFztfTr9ASx4Axntx2l30LWzGXovyKrZ1yjbhrYLtgUtsMJdkmFCx-UK6JP8cy1R4hyiUqf1alI6mWSnpvm1WKP7LWsHK4xbv0SkvyGx-5zopPCZnCOFJBg6Pnh3IgEkLmBOS4oa43dkPMY)



# 8.  NLP

NLP is a branch of artificial intelligence that deals with the interaction between computers and humans through natural language. The ultimate objective of NLP is to read, decipher, understand, and make sense of human languages in a valuable way.

### 8.1    Syntax vs. Semantics
- Syntax: Refers to the arrangement of words and phrases to create well-formed sentences in a language. It's about the structure of these statements.
- Semantics: Deals with the meaning that is conveyed by a text. It's about understanding the meaning and interpretation of words and how sentence meanings are built up.
- Example: "Colorless green ideas sleep furiously" is syntactically correct but semantically nonsensical.

### 8.2    Sentiment Analysis

- Concept: Involves analyzing text data to determine the sentiment expressed by it, typically classifying it as positive, negative, or neutral.    
- Example: Analyzing product reviews to determine customer satisfaction.

### 8.3    Topic Modeling
- Concept: A process of automatically identifying the themes or topics present in a text corpus.
- Example: Discovering common themes from a collection of news articles.

### 8.4    Vocabulary: Word, Document, Corpus
- Word: The smallest element that can be uttered in isolation with objective or practical meaning.
- Document: A collection of words that conveys a specific message.
- Corpus: A large and structured set of texts.
- 
### 8.5    Preprocessing and N-Grams
- Preprocessing: Involves steps like normalization (bringing text into a standard form), stemming, lemmatization, and removing stop words.
- N-Grams: Models that predict the occurrence of a word based on the occurrence of its N - 1 previous words.
- Unigrams and Bigrams: Unigrams are single words, and bigrams are two-word pairs. They help in understanding context and word sequence.

#### 8.6    Creating Vocabulary List and Applying N-Grams
- Process: Involves identifying all unique words and creating N-grams combinations to use in further analysis.
- Information Loss: When converting text to vectors or bag of words, the order of words and hence some aspect of context is lost.


### 8.7    Term Frequency (TF) and TF-IDF

- **TF:** Measures how frequently a term occurs in a document.   
- **DF:** How many docs contain that word
- **TF-IDF (Term Frequency-Inverse Document Frequency):** Reflects how important a word is to a document in a collection or corpus. It's a statistical measure used to evaluate the importance of a word to a document in a dataset.
- **TF-IDF Equation:** ( TF-IDF(t, d) = TF(t, d) \times IDF(t) )
- IDF = Log[(1+# Number of documents) / (1+Number of documents containing the word)]
- Application: Helps in converting text data into a more usable form for machine learning models.

![](https://lh7-us.googleusercontent.com/HgB8LrTN139HiAdZuXsnMrRsxzUbio-QS-wpUas_bIkF1eELKpAFPaHbfMplVAaNtJpiTK_CNPP8N4Zsr5i-bKqEfECF2qVWX6ffJa8h_L0Fe6y_zd1pn2wfycQmVt5dGCWUhXj3GbSGXF8Ug-ZHNfA)



![](https://lh7-us.googleusercontent.com/6rN5j8uWZGNcBmHjKPB1fHqVYnjbA6lJNoKgrPmaH58uqFRyWHPBc17gVqLJOn9C7miO_skwqq30gjkLtYyLGCkfOaJw-dRHRE6yQ47gQ0ef1vZpyL2nyKGnI_RfysMGYNZLb2pFz-PMpCQQctxvH08)


### 8.8    Cosine Similarity
A metric used to measure how similar the documents are irrespective of their size. It's measured by the cosine of the angle between two vectors.

- Cosine Similarity Equation: ![](https://lh7-us.googleusercontent.com/0_BM4LS0RlCuW6bCqzquElsNVQoKi8DA9rgoqY4caO_moVV04_cPDFrhvoh7i2lFz3SinGUzpjI_tPT6HhLGZ_UzcYXIKau_zGrQKSWCL9XrOA5hU-f1vzeWs5_ym5hOclmpFFwEZFpIn5doQ5ZiVvY)
- Usage: Cosine similarity is used to compare documents in various applications like plagiarism checks and document clustering.

### 8.9    Example Questions

1. Sentiment Analysis: Given a dataset of customer reviews, how would you implement a model to classify each review as positive, negative, or neutral?
2. Topic Modeling: How would you identify and differentiate the main topics being discussed in a collection of news articles?
3. TF-IDF Application: How would you use TF-IDF to transform a set of documents into a format that's suitable for clustering?

# 9.  Graphs 

 A set of objects (nodes or vertices) and the connections (edges) between them.

- **Directed Graph (Digraph):** edges have a direction (go from one node to another). A →B, doesn't necessarily mean there is an edge from B to A.
- **Undirected Graph:** edges have no direction; traverse the edge in either direction.
- **Weighted Graph:** Each edge is assigned a numerical value or weight, representing some measure such as distance, cost, or time.
- **In-degree :** count of incoming edges to a node.
- **Out-degree :** count of outgoing edges from a node.

![](20231215025647.png)

- **An adjacency matrix:** a 2D array of size V x V where V is the number of vertices in a graph. If there is an edge from vertex i to j, then the cell in the i-th row and j-th column is 1 (or the weight of the edge if it's a weighted graph), otherwise 0.

![](20231215030640.png)
- **Temporal Graph:** Edges can be added over time. Nodes and edges can be added over time. Nodes and edges can be added and removed over time.
- **Multi-graph:** allows **multiple edges (connections) between the same pair of nodes** and may also permit self-loops (edges connecting a node to itself).
- **Hypergraph:** generalization of a graph that **allows edges to connect more than two nodes.** Edges can join any number of vertices. Provides a more flexible representation for capturing relationships involving multiple elements. Hyperedge can **connect any number of nodes** (more than two).
### 9.1    Graph-Level, Node-Level, Edge-Level Tasks

- **Graph-Level Tasks**: Involve analyzing and making predictions about the entire graph (e.g., determining if a graph is a part of a particular class). Predict whether a given molecular structure has the necessary properties to be an effective and safe drug. 
- **Node-Level Tasks**: Focused on individual nodes within a graph (e.g., node classification). Predict whether an unlabeled node (person) in a social network smokes or not based on features like their social connections etc..
- **Edge-Level Tasks**: Revolve around the edges of a graph (e.g., predicting the formation or deletion of edges). Predict whether a connection (edge) should be established between a user and a specific video, indicating it as a recommendation for the user's next watch.

### 9.2    Link Predictions

- Concept: Predicting whether a link (edge) should exist between two nodes. This is a common problem in social networks, recommendation systems, and network analysis.

### 9.3    Node Level Features

- Features specific to nodes, such as in-degree, out-degree, centrality measures, and more.

### 9.4    Degree Centrality and Normalized Degree Centrality

- Degree Centrality: Measures the number of connections a node has. It is calculated as the degree of the node divided by the maximum possible degree in the graph.
  
- Equation:  
![](https://lh7-us.googleusercontent.com/QCT79UTUbvGn7sm4Q2zQE4Ff84PfzlMd-2yOuZpjSRh9_Bx_CK9ok3M9dEb1XIw07WswdS4ZzqJ55DhxOysVXgW9Page5bKPBg3GEjYalS3AG5fODApFKGGDvRreCpcJKVEB1OXHptPCU1FPoYEeUbc)

### 9.5    Closeness Centrality

- Concept: Measures how close a node is to all other nodes in the network. It indicates the average length of the shortest path from the node to all other nodes.
- Equation: It is calculated as the average of the shortest path length from the node to every other node in the network/graph.
  
![](https://lh7-us.googleusercontent.com/LCuc0SNhSaqFXWp1WQK3lvnFZ3AS7zHdlUeWb5CZDEWnlrS_VbB7tI0aa5WYenhXuPgohR_ZY9nZZ8UxdouueUTeChKTbWrkAQDdOM6UNDIpDJHp7z1rFJG_AtNiSMQpJHXAoFeDWpdzfzopie-L3m4)

### 9.6    Betweenness Centrality

- Concept: A measure of centrality in a graph based on shortest paths. It quantifies the number of times a node acts as a bridge along the shortest path between two other nodes.
- Equation: ( C_B(v) = \sum_{s,t \in V} \frac{\sigma(s, t|v)}{\sigma(s, t)} ) where ( \sigma(s, t) ) is the total number of shortest paths from node ( s ) to node ( t ) and ( \sigma(s, t|v) ) is the number of those paths that pass through ( v ).

### 9.7    Example Questions and Explained Answers

**Degree Centrality**: Given a graph with 5 nodes where node A is connected to all other nodes, calculate the degree centrality of node A.
- Answer: Node A's degree is 4. The maximum degree possible is 4 (since there are 5 nodes in total). So, the degree centrality of A is ( \frac{4}{4} = 1 ).

**Closeness Centrality:** In a graph with 4 nodes where each node is connected to all other nodes, what is the closeness centrality of any given node?
- Answer: Since each node is equidistant from all others, the sum of distances for any node is 3 (1 edge to each of the other 3 nodes). Therefore, the closeness centrality for any node is ( \frac{1}{3} ).

**Betweenness Centrality:** Consider a line graph with 4 nodes (A-B-C-D). What is the betweenness centrality of node B?  
- Answer: Node B is on the shortest path between A and C, and between A and D. Therefore, its betweenness centrality is calculated considering these paths. It's involved in 2 out of 3 shortest paths, so ( C_B(B) = \frac{2}{3} ).



# 10.  Recommendation Systems

Systems designed to recommend items to users based on various factors such as user preference, behavior, and similarity to other items or users.
- Challenges: Includes dealing with the cold start problem, popularity bias, varying user preferences, and ensuring diversity in recommendations.

### 10.1    Content-Based Filtering

Recommends items similar to what a user liked in the past based on item features.

- Strengths: Personalization to individual user's tastes, ability to recommend new and unpopular items.    
- Weaknesses: Difficulty in finding appropriate features, limited by user's past preferences, needs retraining for new items or changing preferences.

### 10.2    Collaborative Filtering

Makes recommendations based on the preferences of similar users.

***Types:***
- **User-Based Nearest-Neighbor:** Recommendations are made based on the preferences of users similar to the target user.
- **Item-Based:** Focuses on the similarities between items and recommends items similar to what the user has liked in the past.

### 10.3    User-Based Collaborative Filtering

***Overview of Steps:***
- Collect user data (ratings, likes, views).
- Create a User-Item Matrix.
- Measure similarity between users.
- Identify a neighborhood of similar users.
- Predict ratings for unseen items.
- Recommend items with high predicted ratings.

### 10.4    Similarity Measures

- Jaccard Coefficient/Similarity: Measures similarity between sets, but ignores the magnitude of ratings.


![](https://lh7-us.googleusercontent.com/7RB0V1O-4xLgaQTLcjHsRXvFWXasRJSjWn-3gIcIqIGUuiaYRhTVlQvukVh-jEMrNI7_Bw3g6YJeACtYZTR_rJl1HarLOpU9qgjHPmdPBPXHpj-iNEmKVHoZa_M5FgW055Yb9C2ALhy2w9tTCNcU5pQ)

sim(A,B) = |ra ∩ rb | / |ra∪ rb |
                =  1 / 5  
sim(A,C) = 2/4 

Just counts times when both rated something compared to total number of things rated between them, no account for ratings

- Cosine Similarity: Measures the cosine of the angle between two vectors in an n-dimensional space.
- Equation:     

![](https://lh7-us.googleusercontent.com/y54lCc4UTs5_REJdBgoWzmbXgEDjkEWkEXXwjMvp5Uq0H8v0KJ_I7FT6DPyhn3zmbElGpN9OdXkjI_9ppxiCIASDMB08i6ZZEHSfHYbpq-4L6dVmPq7q5H3YZemgGu_evl4ZV_T_bxWSabfqgOYsUHI)

- Centered Cosine (Pearson Correlation): Cosine similarity of centered (mean-subtracted) vectors.

- Equation: EX- new table    

![](https://lh7-us.googleusercontent.com/UoT7_Ell1Ap2cKlkAwPRm1U0EJGno9YGhf9wReTwuu46hMdqPiKDjqNiOBoqbI0vvbzfI0WRiogTqXFEx6UQNn-MW-MOJ1Z7g6jkf9bvLYjkARMkXbRL5D-uMRYGDxWrX6_m5o5ItZlYKVoOw8xcdag)

### 10.5    Predicting and Recommending

- Use the similarities to predict a user's interest in an item.
    
- Recommend items with highest predicted interest scores.
    

### 10.6    Evaluating Recommendation Systems

- Evaluation Metrics: Includes Mean Absolute Error (MAE), Precision at Top Ten, etc.
- MAE: Mean absolute error is the average of the difference between the value predicted by the recommender and the actual value given by the user. 
  
![](https://lh7-us.googleusercontent.com/wO3Ohg18FMkiTZ5nsv1Q4I6aj5PVGcdto_EkocDSXOrqdCfdbBRiZu_z5DQAQazQQWw4sYtsNK9FalXF-vbCaCV_WyfEvjLpVN-NmvTMA2QTrZbSHwLkhe9auYCwhd8rNgjMicaVrlnZKCabtU_bMwg) 

- Challenges in Evaluation: Handling missing ratings, balancing new and known items, user preference changes.

### 10.7    The Cold Start Problem

Difficulty in making recommendations for new users or items due to lack of data.
- Solutions: Using hybrid systems, asking new users to rate a set of items, using demographic data.

### 10.8    Choosing the Right Recommendation System

For a given scenario, determine which recommendation system (content-based or collaborative filtering) is more appropriate based on the available data and the specific requirements of the situation.

### 10.9    Example Questions and Explained Answers

Content-Based Filtering: How would you recommend a movie to a user who likes action movies?
- Answer: Analyze features of movies (like genre, director, cast) the user has rated highly. Recommend movies with similar features, particularly focusing on the action genre.

User-Based Collaborative Filtering: How would you recommend a book to a user based on the preferences of similar users?
- Answer: First, find users with similar reading tastes using similarity measures like cosine similarity. Then recommend books that these similar users have rated highly but the target user hasn't read.

Evaluating a Recommender System: What could be an effective way to measure the performance of your recommendation system?
- Answer: Use metrics like Mean Absolute Error, which calculates the average error between the system's predictions and the actual ratings by users. Lower MAE values indicate better performance.

Addressing the Cold Start Problem: A new user joins your platform, how do you recommend items to them?
- Answer: Initially, use demographic information or ask the user to rate a few items upon sign-up. You can also use a hybrid approach combining content-based and collaborative methods.

# 11.  Ethics

### 11.1    Major Areas of Concern in Data Ethics

**Data Collection:**
- Ethical sourcing of data and informed consent are crucial.
- Data should be collected for legitimate purposes and in a manner that respects the rights and privacy of individuals.

**Data Ownership:**
- Concerns who has the legal rights and control over data.
- Addresses issues like unauthorized data usage and ownership disputes.

**Data Privacy:**
- Protection of individuals' personal information.
- Ensures control over the collection, use, and disclosure of personal data.

**Data Anonymity:**
- The process of removing personally identifiable information from data sets.
- Ensures individuals cannot be unexpectedly identified from the data.

**Data Validity:**
- Ensures the integrity and accuracy of data.
- Data should accurately represent the phenomena or entities it is intended to measure.

**Algorithm and Statistics Fairness:**
- Addresses biases in algorithms and statistical models.
- Ensures that algorithms are fair and do not discriminate against any group.

### 11.2    Ethical Scenarios and Concerns

- For each scenario, identify the primary ethical concern based on the areas listed above.
- Example scenarios might include:
- A company collects user data without explicit consent (Data Collection).
- A social media platform uses personal data for advertising without user knowledge (Data Privacy).
- An AI system discriminates against certain groups in loan approvals (Algorithm and Statistics Fairness).

### 11.3 Applying Ethical Principles

- For a Given Scenario: Determine the ethical concern and discuss potential solutions or approaches to address it.
- Example Question and Answer:
- Scenario: A healthcare app collects patient data for analysis. Patients are unaware their data is being used for research.
- Ethical Concern: This scenario primarily involves issues of Data Privacy and Data Collection.
- Solution: Implement clear consent forms explaining data usage, ensure data anonymization, and establish transparent data policies.

#### Remember:

- Ethical considerations in data science are not just about legality but also about fairness, honesty, compassion, and respect for human dignity.
- Ethical dilemmas often involve navigating complex situations and making choices that consider the impact on privacy, fairness, and well-being.