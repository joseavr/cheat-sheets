📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-10-09

---

# Introduction

Frequently we get our data without any more information and we have to process the data ourself. All we have is a CSV and no guide, no label, nothing else.

# Exploratory Data Analysis

`df.columns` lists all columns
`df.dtypes` tells datatypes of each column

Start by identifying important columns like revenue, engament, survival. How other variables relate to that. Identify indenpendent and dependent columns, what columns relates and contribute to other ones.

`df["column"].describe()` gives count, mean, std, min, ...

`df["column"].value_counts()` tells how variables are distributed

`df["column"].hist()` display histogram chart, works with continuous variable


# Pearson's Correlation Coefficient

`df.corr()` gives the pearson's correlation coefficient. Used to know if two variables has a relationship. 1 if variables are perfectly correlated. -1 if perfectly anti-correlated. 0 otherwise

![](20231009172052.png)

