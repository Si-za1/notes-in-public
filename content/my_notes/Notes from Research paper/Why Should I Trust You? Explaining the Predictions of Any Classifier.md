---
title: Why Should I Trust You? Explaining the Predictions of Any Classifier
draft: false
tags:
  - in-progress
---
 

Notes taken for my understanding from the paper titled: 
**Why Should I Trust You? Explaining the Predictions of Any Classifier**: 

**My understanding for the title would be:**
It means, when we use a certain model to determine certain predictions, we use certain metric to validate or come to conclusion for determining the considered prediction. this is the case when we are trying to see that whether or not we do understand the model's behavior and take the result for any sort of decision making.

**Notes from the paper:**

==The gist of the paper: Why was this started?==

If one plans to take action based on a  prediction, or when choosing whether to deploy a new model.  Such understanding also provides insights into the model,  
which can be used to transform an untrustworthy model or  prediction into a trustworthy one.

==And what was done to satisfy the above-mentioned why?==

Proposed **LIME**, a novel explanation technique that explains the predictions of any classifier in an interpretable and faithful manner, by learning an interpretable model locally around the prediction. We also propose a method to explain models by presenting representative individual predictions and their explanations in a non-redundant  way, framing the task as a sub modular optimization problem.

We demonstrate the flexibility of these methods by explaining different models for text (e.g. random forests) and image classification (e.g. neural networks)

**INTRODUCTION:**
