📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-10-18

---

# Decision Trees

Useful data structured used in data science and machine learning for data analysis process. 

Labels

When building decision trees, the less depth the better. That is, fewer rules.

# Usefulness


1. **Classification and Regression:** Decision trees can be used for both classification and regression tasks. In classification, decision trees help categorize data into different classes or categories, while in regression, they can predict a numeric value.
    
2. **Interpretability:** Decision trees are easy to interpret. They represent a series of binary decisions, which can be visualized graphically. This interpretability makes them valuable for explaining and communicating the reasoning behind a model's predictions.
    
3. **Feature Selection:** Decision trees can implicitly perform feature selection by giving importance to the most informative features at the top of the tree. This can help data scientists identify the most relevant features in a dataset.
    
5. **Handling Missing Data:** Decision trees can handle missing data without much preprocessing. They simply take alternative paths when a feature is missing, which can be advantageous when working with incomplete datasets.
    
7. **Scalability:** Decision trees are relatively computationally efficient and can handle both small and large datasets, making them suitable for a wide range of applications.
    
10. **Model Validation:** Decision trees are valuable for initial modeling and rapid prototyping. They can help data scientists quickly build models to understand the dataset and check if the data has any meaningful patterns.  

# Entropy

A measure how much information something provides. 
- Measured in bits
	- How many **bits** needed to communicate to you
- One bit of entropy is the amount of information it takes to encode a yes/no signal
	- e.g flip coins, it will take **one bit** to encode this information
	- e.g result of two flip coints, takes **two bits** (e.g 11, 10, 01, etc)

# A Formula to Entropy

A function that is:
- Continuous
- 1 if all events are equally likely (entropy maximized = 1)
- 0 if outcome is certain (entropy minimized = 0)
- Doubling the number of outcomes (one flip - 2 outcomes, two flips - 4 outcomes, three flips - 8 outcomes), entropy increase by one


if all events are equal probability: $$
E(X) = -lg(1/p)
$$
Otherwise:$$
H(X) = - \sum p_{x} * lg(1/p_{x})
$$
#### Example
For a fair coin flip, there are two equally likely outocmes: heads and tails
Result:$$
H(x) = -(\frac{1}{2} \log ( \frac{2}{1}) + \frac{1}{2} \log ( \frac{2}{1} ) = 1
$$
#### Summary
- **Entropy of 1: Maximum Uncertainty:** outcomes are equally likely, there's maximum unertainty or disorder. Takes a full bit to describe each outcome.
- Entropy Between 1 and 0: 




