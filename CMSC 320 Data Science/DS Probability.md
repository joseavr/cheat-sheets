📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2023-10-09

---

# Introduction

Probability is the likelihood an event occurs

# Bayes Rule


# Distribution Types

Statistical functions that give probability of a given outcome from an experiment

#### Uniform Distribution

Outcomes equally likely. e.g rolling a fair die

#### Normal Distribution (Gaussian)

A bell shape, most values in the center region, with highest point (mean) at center.

![](20231009234137.png)

#### Poisson

Independent events happening at random in a interval of time or space.

```example
Number of bankruptcies declared per week
```


#### Zero-Inflated Poisson Distribution

A spike at 0. That is, zero counts for an determine event.

```example
Number of fish caught per day for each person (not all participants fish)
```
Not all participants fish, so decent numbe of participants will end up with 0 fist for some day.

#### Bernoulli trial

A process that has two outcomes: "success" or "failure". Denoted as 1 for success or 0 for failure. Each trial is independent, that is, outcome of one trial does not affect another trial

```example
whether an email is a spam (1 if it is, 0 if not)
flipping coin and getting heads (1 if heads, 0 if not)
```

#### Binomial Distribution

Shows the probability of many set of outcomes from Bernoulli Trials

```example
flipping once gets Bernoulli. Flipping twice or more gets Binomial Distribution
```

# Central Limit Theorem

Fundamental theorem of stats. 
Takes an annoying distribution to convert to a normal distribution
