---
title: RAGAS
draft: false
tags:
  - notes
  - in-progress
---
 Context Precision is a metric that measures the proportion of relevant chunks in the `retrieved_contexts`.

`LLMContextPrecisionWithReference` metric is can be used when you have both retrieved contexts and also reference answer associated with a `user_input`. To estimate if a retrieved contexts is relevant or not this method uses the LLM to compare each of the retrieved context or chunk present in `retrieved_contexts` with `reference`.

`LLMContextPrecisionWithReference` metric is can be used when you have both retrieved contexts and also reference answer associated with a `user_input`. To estimate if a retrieved contexts is relevant or not this method uses the LLM to compare each of the retrieved context or chunk present in `retrieved_contexts` with `reference`.

`LLMContextRecall` is computed using `user_input`, `reference` and the `retrieved_contexts`, and the values range between 0 and 1, with higher values indicating better performance. This metric uses `reference` as a proxy to `reference_contexts` which also makes it easier to use as annotating reference contexts can be very time consuming.

`ResponseRelevancy` metric focuses on assessing how pertinent the generated answer is to the given prompt. A lower score is assigned to answers that are incomplete or contain redundant information and higher scores indicate better relevancy.

This metric is computed using the `user_input`, the `retrived_contexts` and the `response`.

`Faithfulness` metric measures the factual consistency of the generated answer against the given context. It is calculated from answer and retrieved context. The answer is scaled to (0,1) range. Higher the better.

---

context precision: it measures the proportion of relevant chunks in the retrieved contexts

whether all the ground-truth relevant items are present in the contexts are ranked higher or not.

eg: where is france and it’s capital?

gt: france is in WEU and its capital is paris

high context precision: france is in wester europe, it encompasses medieval cities, .. paris its capital is famed for its fashion hub.

low context precision: the country is is renowned for its wine, cuisine. France in western eruope, encompasses cities. Paris its capital , is famed for its hubs for fashion.

---

Context Recall : It measures how many pof the relevant documents or information were successfully retrieved. It is about whether or not anything important is missing?

High recall means fewer relevant documents were left out.

High value high performance. It computes using user_input, reference and retrieved contexts

eg: where is eiffel tower located?

gt: its located in paris

reference: its located in pairs

retrieved contexts: paris is capital of france.

lower recall for this scenario

---

Faithful measures the factual consistency of generated response against the retrieved contexts. If all the claims that are maid in the answer can be inferred from the given context then the response is considered to be faithful else not.

---

Answer relevance for ragas: a low score means answers are incomplete and contains redundant information

**Faithfulness:** This measures the factual consistency of the generated response against the retrieved contexts. If all the claims made in the answer can be inferred from the given context, then the response is considered faithful; otherwise, it is not.

**Context Precision:** This measures the proportion of relevant chunks in the retrieved contexts. It assesses whether all the ground-truth relevant items are present and ranked higher in the contexts.

_Example:_ Where is France and what is its capital?

- **Ground Truth (GT):** France is in Western Europe, and its capital is Paris.
- **High Context Precision:** "France is in Western Europe; it encompasses medieval cities. Paris, its capital, is famed for its fashion hub."
- **Low Context Precision:** "The country is renowned for its wine and cuisine. France is in Western Europe and encompasses cities. Paris, its capital, is famed for its hubs for fashion."

**Context Recall:** This measures how many relevant documents or pieces of information were successfully retrieved. It assesses whether any important information is missing. High recall indicates that fewer relevant documents were left out, leading to higher performance. It is computed using user input, reference, and retrieved contexts.

_Example:_ Where is the Eiffel Tower located?

- **Ground Truth (GT):** It is located in Paris.
- **Reference:** It is located in Paris.
- **Retrieved Contexts:** Paris is the capital of France.

In this scenario, the recall would be lower.
