# Week 0 – Introduction to Machine Learning

## Why I Started

Although I already had a strong programming background — including completing several software projects and Harvard's CS50 Web Programming with Python and JavaScript course, where I built applications using technologies such as Django—I decided not to spend time revising Python before starting this specialization.

I had limited experience with libraries such as NumPy and Matplotlib, but I was eager to begin learning machine learning. My goal was to build a solid understanding of the fundamentals first and learn the supporting tools along the way.

---

## What is Machine Learning?

The course began by introducing the idea of machine learning using Arthur Samuel's checkers program. Rather than being explicitly programmed with the best moves to make, the program learned from playing many games and gradually identified positions that increased its chances of winning.

From my understanding:

> Machine learning is the field of computing in which we allow computers to perform tasks without giving them explicit instructions on how to perform those tasks. Instead, the computer figures out how to perform those tasks through being trained.

---

## Types of Machine Learning

There are two main types of machine learning introduced in this course:

- Supervised Learning
- Unsupervised Learning

### Supervised Learning

In supervised learning, we provide the computer with examples consisting of:

- **Inputs**, called **features**
- **Correct outputs**, called **target values**

The goal is to train the computer to figure out how the inputs map to the correct outputs.

For example, suppose we have data containing the sizes of houses and the prices at which they were sold. We can train a machine learning model to learn the relationship between a house's size and its selling price. Once trained, the model can predict the selling price of a house given only its size.

---

## Types of Supervised Learning Problems

There are two main types of supervised learning problems.

### Regression

A regression problem is one in which we try to predict a numerical value.

Using the house example, the target value is the selling price of the house. Since a price can be one of infinitely many possible numerical values, this is considered a regression problem.

### Classification

A classification problem is one in which we try to predict a category.

Unlike regression, where the output is a number, classification predicts a target value from a small, finite set of possible categories.

For example, determining whether an email is **spam** or **not spam** is a classification problem.

### Univariate Linear Regression (One variable Linear Regression)

For predicting target values where we only have one input features. For instance, predicting price of a house based on a single input feature, size of the house in square feet.

Given a dataset for houses sizes in square feet and the prices at which they were sold for, we can plot the data with prices on the y axis and sizes on the x axis just to visualise the data. This helps to gain some insight into how the two variables are related.



