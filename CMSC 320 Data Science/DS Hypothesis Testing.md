📚Class: CMSC 320

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-10-08

---

# Hypthosis Testing

A method used to make informed decisions based on sample data (e.g subset of population data). 

### Key concepts:

**Outliers** is a data points that is very extreme compare to the rest of data points (e.g A billionare with high income while the majority data points has moderate income)

**Mean** is the average of data. Sensitive to outliers (e.g extreme values in data (very high income or very low incomes) can disproportionately influence the mean)

**Median** is middle value when data arranged ascending or descending order. Robust to outliers (not affected by extremes values). It provides a better representation of a "typical"  value when there are outliers.

**Standard Deviation** how spread out the values are from the mean (average) of the data

**Mode** is a value that appears more frequently in a dataset. Number witht the heighest frequency (e.g most common category such as eye color in a population)


# State Hypothesis

Hypothesis is a premise we want to test. 
A statetment about one or more populations.

```Example
The hospital admin wants to test avg length of patient in hospital is 5 days
```

#### Null Hypothesis

A statement to be tested with no effects (Ho)

#### Alternative Hyposthesis

A statement adopted with new strong and empirical data, so Ho is rejected.
A statement contradicting null hypthesis (Ha), suggesting there is a significant change.

```Example
I believe machine makes 5 gram in weight chocolate bars. A worker says they no longer make 5 gram bar. Write Ho and Ha.

Null Hypothesis Ho: u = 5 gram
Alternative Hypothesis Ha: u != 5 gram
```

**Testing help to determine that the data you have statistically significant enough to reject this null hypothesis or not**


# Statistical Significance

How confident are with our decision? Use `C` variable
The **significance level (alpha)** describes when to reject the null hypothesis



**Level of significance**: 

```
alpha = 1 - C
```

**Example**

```Example
if level confidence = 95% -> C = 0.95
Alpha = 1 - C 
      = 1 - 0.95 
      = 0.05
```

# Type I and Type II Errors

`Type I Error`: when rejecting a true Null Hypothesis (false positive)

`Type II Error`: when fail to reject a false Null Hypothesis (false negative)

#### Example

```Example
Testing wether a new drug is effective in reducing blood pressure

Ho: drug has no effect on blood pressure.
H1: drug reduces blood pressure.
```

`Type I error`: concluding drug is effective at reducing blood pressure when reality has no effect (assuming null hypthesis is true, rejecting leads to an error of Type I)

`Type II error`: failing to detect drug is effective when, in fact, it does reduce blood pressure (assuming null hypothesis is false, failing to reject this is a Type II)


# Region Representation

If test falls in middle, null hypothesis is accepted and the alternative hypothesis is rejected
if test falls in critical points (corner), the null hypthesis is rejected, Ha is accepted

![](20231008225225.png)


# P-Values

Finding critical values are hard. Commonly done by computers. Alternative, P-values

Determine the significance of an observed effect in a hypothesis test. It helps answer the question: "How likely is the observed result to occur under the null hypothesis?"

The null hypothesis typically represents the idea that there is no significant effect or difference in the data

A small p-value is often interpreted as an indication of statistical significance. Meaning, in favor of alternative hypothesis

`p-value`: probability null hypothesis is correct

if `p-value <= alpha`, reject Ho
if `p-value > alpha`, fail to reject Ho

#### Example

```Example
Suppose testing the following hypothesis at significance level (alpha) 5% and got p-value, and sample statistic x = 25
```

P-value is 3% < alpha, so we reject the null hypthesis

# Tests Types

A method used to decide whether data sufficiently support an hypothesis

**Knowing for data help us!** If we have enough data to make an estimate, we can perform tests like z-test to give more accurate results.

### Z-test

Used for **LARGE SAMPLE SIZE** (n > 30) and know the population **STANDARD DEVIATION**
Use if data is normally distributed and large number of samples
### T-test

Used for **SMARLLER SAMPLE SIZE** (n < 30) and when don't know standard deviation, and must estimate from sample.
Use if data is normally distributed and have small number of samples

### One sample T-test 
Compares mean of a sample with population mean

### Two sample T-test
Compares mean of two different samples

### Paired test
Use when follow specific population members through time

```example
Aliens monitor humans, run half of them thru a machine to make them smarter. Then, they wanna know if machine worked.
```

Ho: The machine did nothing
Ha: machine came from different distribution
## Chi-square test

Estimes if two sets of categorical data come from same distribution

Ho: These two observations came from places with the same birds
Ha: The two locations have different underlying bird populations

### Anova

Used for comparing **MEANs** of different groups (more than two) to see differences among them. It only indicates that the difference exists in the group

Ho: There is no difference between any of the groups
Ha: There is difference between at least one of the groups

### Post Hoc

Post Hoc shows which groups differ from another, while Anova shows that the difference exist. 
Used to indentify which specific groups are different from each other when there are more than two groups and multiple comparisons.

```example
a study to compare test scores of students from three different schools: School A, School B, School C
```

Apply Anova: results in finding p-value
Apply Tukey's HSD Post Hoc: using p-value to find if has significant difference. 
if p-value < 0.05, considered significant different. Otherwise, no significant difference

### Kruskal-Wallis Test

Extension of ANOVA test
Compares medians of >2 independent groups - when data dont meet assumptions of normality required for ANOVA

### Mann-Whitney U Test

Used to compare two independent groups - when data dont meet normality assumptios require for T-test

### Wilcoxon Signed-Rank Test

Used to compare two related or paired groups - when data dont meet  normality assumptions required for a paired t-test

# Choosing Appropiate Test

`Discrete/Categorical`: Chi-squared Test

`Continuous`: 
- `Comparing Mean`:
	- `1 sample`:
		- `n < 30`: T-test
		- `n > 30`: Z-test
	- `2 sample`
		- `independent data`: T-test
		- `paired data`: Paired T-test
	- `>2 sample`: ANOVA

- `Comparing Median`:
	- `1 sample`: Wilcoxon or Sign
	- `2 samples`: Whitney Test
	- `>2 samples`
		- `outliers`: Mood's median test
		- `no outliers`: Kruskal-Wallis Test
