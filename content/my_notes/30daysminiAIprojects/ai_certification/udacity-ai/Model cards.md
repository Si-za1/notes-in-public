---
title: Model cards
draft: false
tags:
  - complete
---
## Model Cards

A **model card** is a detailed document or report that provides critical information about a machine learning (ML)/AI model in a structured and accessible format. It's designed to offer transparency and governance for machine learning models, especially when they are deployed in real-world applications.

Key elements of a model card typically include:

1. **Model Overview** - a general description of the model, its purpose, the problem it's intended to solve, and the algorithm type it employs.
2. **Intended Use** - outlines the specific scenarios and applications for which the model is designed. It also mentions scenarios where the model should not be used, thus guiding responsible deployment and use.
3. **Risk Ratings** - the model is categorized based on the level of risk associated with its application, which can range from low to high. This helps in understanding the potential implications of the model's predictions and decisions.
4. **Training and Evaluation Details** - information about how the model was trained, the data it was trained on, the training environment, and the metrics used to evaluate its performance.
5. **Model Performance and Metrics** - specific performance metrics, observations from evaluations, and any relevant graphs or statistical data are documented here.
6. **Ethical Considerations and Recommendations** - any ethical concerns related to the model and recommendations for its use, including any limitations or biases that users should be aware of.
7. **Versioning** - model cards maintain a record of changes made to the model, ensuring that there is a transparent history of its development and modifications.
8. **Additional Information** - custom details, caveats, and any other relevant information that doesn't fit into the standard sections can be included here.

Model cards in Amazon SageMaker follow a JSON schema to standardize the format and make it easier to create, share, and update these documents.