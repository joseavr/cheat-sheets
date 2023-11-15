📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-10-09

---

# Introduction

Frequently data will be messy. E.g values are missing, columns neeed to be combined, tables needs to be joined. So we clean them

# Data Typing

`df["column"].astype(someType)` to change types

# Duplicated Records

`df.drop_duplicates()` will drop duplicates records/data that are exactly the same.
For records that are slightly similar, keep the true ones and drop the rest.

# Outlier Detection, z-score

Outlier is data/data point that is very extreme.
Only remove outlier if affects our goal. 

# Data Missing

May happen because non-response on a survey, some malfunction, or forgot to enter it.
Data is missing for random circumstances or sometimes not random. (e.g a GPA survey, students with lower GPA may choose not to answer)

### Missing at Random

For categorical data is fine. 
e.g if category is major, we could have ['Computer Science', 'Philoshophy', 'Did not answer]

For numerical data, drop it. `df.dropna()`


# Different Types of Imputation

### At Random

`Mean Imputation`: Set the missing value to the mean (e.g height is missing, fill 5' 5")

`Mode Imputation`:  Set the missing value with the most frequent value. (e.g filling Computer Science)

`Hot-Deck Imputation`: Finding a row similar to the missing value and fill up

`Bayesian Imputation`: For categorical data

```
p(possibe_value | features) = 
		p(features | possible value) * p(possible value) / p(features)
```
### Not at Random




# Incorrect Data

Types of incorrect data:
- People lied
- instrument broke
- Recording wrong metrics
- Illegal values

# Detect Incorrect Data

Here are some tips:
- **Discontuinity or attractor**. e.g legalized weed from being illegal
- **Data outside bounds.** e.g people who played games for millions hours
- **Modes nonsense.** e.g many people living at the sea
- **Boundary conditions**

# Boundary Conditions

Occurs when
- Instruments have a maximum measurement
- Database has only certain measurements.
- Survey values only go up til certain amount

Signs of boundary conditions:
- data has a discontuinity at certain value, after which there is nothing

