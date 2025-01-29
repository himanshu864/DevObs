#ml #ai #dev 

# Introduction

**AI** application: is something that can produce results without human interaction.

**ML**: is basically **training** **model** to produce **predictions** or generate content.

**Model**: a mathematical relationship derived from input training data to make predictions.

**Supervised Learning**: models find relationship to create output by training on lots of correct inputs and outputs.

**Regression**: predicts a numeric value. Eg: Chances of rain fall. $33\%$

**Classification**: predicts if something belongs to a category. Eg: Rain or no rain.

**Multi-class**: classes are mutually exclusive.
- instance can only be $a$, $b$ or $c$.
- Example: NB, kNN, DT, Logistic.

**Binary**:
- One-vs-Rest: {$a$} or {not $a$}
- If apply *one-vs-rest* for pairs, Classes may overlap i.e. from both $a$ and $b$. And may not fall under any category (middle).

![[Screenshot 2025-01-25 at 9.32.32 PM.png | 300]]

**Unsupervised Learning**: makes predictions makes on given data without any correct result. It finds patterns. Commonly using **clustering**. Here we don't define categories, but might name clusters.

**Reinforcement Learning**: by rewarding or punishing model based on prediction.

**Generative AI**: Take input to create output based by training on lots of output related to input. Usually unsupervised then reinforced. Ex: text-to-text. Image-to-text. text-video, etc.

---
# Supervised Learning

Tasks are well-defined.
Related data stored is called **dataset**.

Dataset is made up of individual **examples** that contains **features** and **label**. The feature refers to the values that the models uses to predict the label.

Good dataset is large and highly diverse.

The model derives mathematical relationship by feeding input features and predicting output. It trains itself to modify relationship based on the difference between it's prediction and correct output (**loss**).

**Evaluation**: We check how well the trained ML model learnt by feeding it features and comparing its predictions with labels. If shit results, back to training.

**Inference**: Once satisfied with evaluation, we use models to make predictions on unlabeled examples.

---

# Prerequisites

1. [[NumPy]]
2. [[Pandas]]

