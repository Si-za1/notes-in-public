---
title: Regression and related terms
draft: false
tags:
  - complete
reference: https://developers.google.com/machine-learning/crash-course/linear-regression
---
 
[**Linear regression**](https://developers.google.com/machine-learning/glossary#linear-regression) is a statistical technique used to find the relationship between variables. In an ML context, linear regression finds the relationship between [**features**](https://developers.google.com/machine-learning/glossary#feature) and a [**label**](https://developers.google.com/machine-learning/glossary#label).

For example, suppose we want to predict a car's fuel efficiency in miles per gallon based on how heavy the car is, and we have the following dataset:

|Pounds in 1000s (feature)|Miles per gallon (label)|
|---|---|
|3.5|18|
|3.69|15|
|3.44|18|
|3.43|16|
|4.34|15|
|4.42|14|
|2.37|24|

If we plotted these points, we'd get the following graph:

![Figure 1. Data points showing downward-sloping trend from left to right.](https://developers.google.com/static/machine-learning/crash-course/linear-regression/images/car-data-points.png)

**Figure 1**. Car heaviness (in pounds) versus miles per gallon rating. As a car gets heavier, its miles per gallon rating generally decreases.

We could create our own model by drawing a best fit line through the points:

![Figure 2. Data points with a best fit line drawn through them representing the model.](https://developers.google.com/static/machine-learning/crash-course/linear-regression/images/car-data-points-with-model.png)

**Figure 2**. A best fit line drawn through the data from the previous figure.

## Linear regression equation

In algebraic terms, the model would be defined as , where

-  is miles per gallon—the value we want to predict.
-  is the slope of the line.
-  is pounds—our input value.
-  is the y-intercept.

In ML, we write the equation for a linear regression model as follows:

where:

-  is the predicted label—the output.
-  is the [**bias**](https://developers.google.com/machine-learning/glossary#bias-math-or-bias-term) of the model. Bias is the same concept as the y-intercept in the algebraic equation for a line. In ML, bias is sometimes referred to as . Bias is a [**parameter**](https://developers.google.com/machine-learning/glossary#parameter) of the model and is calculated during training.
-  is the [**weight**](https://developers.google.com/machine-learning/glossary#weight) of the feature. Weight is the same concept as the slope  in the algebraic equation for a line. Weight is a [**parameter**](https://developers.google.com/machine-learning/glossary#parameter) of the model and is calculated during training.
-  is a [**feature**](https://developers.google.com/machine-learning/glossary#feature)—the input.

During training, the model calculates the weight and bias that produce the best model.

![Figure 3. The equation y' = b + w1x1, with each component annotated with its purpose.](https://developers.google.com/static/machine-learning/crash-course/linear-regression/images/equation.png)

**Figure 3**. Mathematical representation of a linear model.

In our example, we'd calculate the weight and bias from the line we drew. The bias is 34 (where the line intersects the y-axis), and the weight is –4.6 (the slope of the line). The model would be defined as , and we could use it to make predictions. For instance, using this model, a 4,000-pound car would have a predicted fuel efficiency of 15.6 miles per gallon.

![Figure 4. Same graph as Figure 2, with the point (4, 15.6) highlighted.](https://developers.google.com/static/machine-learning/crash-course/linear-regression/images/model-prediction.png)

**Figure 4**. Using the model, a 4,000-pound car has a predicted fuel efficiency of 15.6 miles per gallon.

### Models with multiple features

Although the example in this section uses only one feature—the heaviness of the car—a more sophisticated model might rely on multiple features, each having a separate weight (, , etc.). For example, a model that relies on five features would be written as follows:

For example, a model that predicts gas mileage could additionally use features such as the following:

- Engine displacement
- Acceleration
- Number of cylinders
- Horsepower

This model would be written as follows:

![Figure 5. Linear regression equation with five features.](https://developers.google.com/static/machine-learning/crash-course/linear-regression/images/equation-multiple-features.png)


**Key terms:**

**Bias:** 
An intercept or offset from an origin. Bias is a parameter in machine learning models, which is symbolized by either of the following:

- _b_
- _w0_

For example, bias is the _b_ in the following formula:

In a simple two-dimensional line, bias just means "y-intercept." For example, the bias of the line in the following illustration is 2.

![The plot of a line with a slope of 0.5 and a bias (y-intercept) of 2.](https://developers.google.com/static/machine-learning/glossary/images/bias.png)

Bias exists because not all models start from the origin (0,0). For example, suppose an amusement park costs 2 Euros to enter and an additional 0.5 Euro for every hour a customer stays. Therefore, a model mapping the total cost has a bias of 2 because the lowest cost is 2 Euros.

## feature

**feature** is an **input variable** used to help a machine learning model make predictions.

For example, if you're building a **spam detection model**, the **features** could be things like:

- The number of links in the message
- Whether the message contains certain keywords (like “win” or “free”)
- The length of the message    
- Sender’s email reputation

**Feature** = Input variable (used to predict)

These features are **used by the model** to decide whether the message is **spam or not spam**.
The following table shows three examples, each of which contains three features and one label:

| Features    |          |          | Label      |
| ----------- | -------- | -------- | ---------- |
| Temperature | Humidity | Pressure | Test score |
| 15          | 47       | 998      | 92         |
| 19          | 34       | 1020     | 84         |
| 18          | 92       | 1012     | 87         |
|             |          |          |            |
|             |          |          |            |

## label

In [**supervised machine learning**](https://developers.google.com/machine-learning/glossary#supervised_machine_learning), the "answer" or "result" portion of an [**example**](https://developers.google.com/machine-learning/glossary#example).

Each [**labeled example**](https://developers.google.com/machine-learning/glossary#labeled_example) consists of one or more [**features**](https://developers.google.com/machine-learning/glossary#feature) and a label. For example, in a spam detection dataset, the label would probably be either "spam" or "not spam." In a rainfall dataset, the label might be the amount of rain that fell during a certain period.

**Label (or target)** = What you’re trying to predict (e.g., spam or not spam)


## parameter

The [**weights**](https://developers.google.com/machine-learning/glossary#weight) and [**biases**](https://developers.google.com/machine-learning/glossary#bias) that a model learns during [**training**](https://developers.google.com/machine-learning/glossary#training). For example, in a [**linear regression**](https://developers.google.com/machine-learning/glossary#linear_regression) model, the parameters consist of the bias (_b_) and all the weights (_w1_, _w2_, and so on) in the following formula:


![Figure 5. Linear regression equation with five features.](https://developers.google.com/static/machine-learning/crash-course/linear-regression/images/equation-multiple-features.png)
## weight

A value that a model multiplies by another value. [**Training**](https://developers.google.com/machine-learning/glossary#training) is the process of determining a model's ideal weights; [**inference**](https://developers.google.com/machine-learning/glossary#inference) is the process of using those learned weights to make predictions.

