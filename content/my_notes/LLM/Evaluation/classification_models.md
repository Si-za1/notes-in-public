---
title: classification_models
draft: false
tags:
  - in-progress
---
Classification : [https://developers.google.com/machine-learning/intro-to-ml#types_of_ml_systems](https://developers.google.com/machine-learning/intro-to-ml#types_of_ml_systems)

# Classification model

A [**model**](https://developers.google.com/machine-learning/glossary#model) whose prediction is a [**class**](https://developers.google.com/machine-learning/glossary#class). For example, the following are all classification models:

- A model that predicts an input sentence's language (French? Spanish? Italian?).
- A model that predicts tree species (Maple? Oak? Baobab?).
- A model that predicts the positive or negative class for a particular medical condition.

Predict the likelihood that something belongs to a category.

classification models output a value that states whether or not something belongs to a particular category. For example, classification models are used to predict if an email is spam or if a photo contains a cat.

Classification models are divided into two groups:

_binary classification and multiclass classification._

Binary classification models output a value from a class that contains only two values, for example, a model that outputs either **`rain`** or **`no rain`**.

Multiclass classification models output a value from a class that contains more than two values, for example, a model that can output either **`rain`**, **`hail`**, **`snow`**, or **`sleet`**.

### Let's define the core values used in all metrics

These are derived from the **confusion matrix**:

- **TP (True Positive):** Model correctly predicted **positive** class
- **TN (True Negative):** Model correctly predicted **negative** class
- **FP (False Positive):** Model incorrectly predicted positive (Type I error)
- **FN (False Negative):** Model incorrectly predicted negative (Type II error)

### The metrics in a classification report

### 1. **Precision**

- **Formula:** `Precision = TP / (TP + FP)`
- **Relies on:** TP and FP
- **Meaning:** Out of all predicted positives, how many were actually correct?
- **Interpretation:** High precision means **few false positives**. Useful when the **cost of false positives is high** (e.g., spam filters flagging non-spam).

### 2. **Recall** (a.k.a. Sensitivity or True Positive Rate)

- **Formula:** `Recall = TP / (TP + FN)`
- **Relies on:** TP and FN
- **Meaning:** Out of all actual positives, how many did the model correctly identify?
- **Interpretation:** High recall means **few false negatives**. Important in **medical diagnoses** or **fraud detection**.

### 3. **F1 Score**

- **Formula:** `F1 = 2 * (Precision * Recall) / (Precision + Recall)`
- **Relies on:** Both Precision and Recall
- **Meaning:** Harmonic mean of precision and recall
- **Interpretation:** Balances both false positives and false negatives. Useful when there's **class imbalance** or when **you need a balance between precision and recall**.

### 4. **Accuracy**

- **Formula:** `(TP + TN) / (TP + TN + FP + FN)`
- **Relies on:** All values from confusion matrix
- **Meaning:** Proportion of total predictions that are correct
- **Interpretation:** Can be **misleading** in imbalanced datasets (e.g., predicting "no disease" in 99% healthy population yields 99% accuracy with 0 recall on positives).

### What the actual value in the report tells you

Say you see this in the report for a class `Positive`:

```
              precision    recall  f1-score   support
     Positive     0.91        0.80     0.85       100

```

- **Precision 0.91**: Out of all predictions of "Positive", 91% were correct.
- **Recall 0.80**: Out of all actual "Positive" cases, 80% were identified correctly.
- **F1-score 0.85**: Balanced score showing good, but not perfect, performance.
- **Support = 100**: There were 100 actual instances of the "Positive" class.