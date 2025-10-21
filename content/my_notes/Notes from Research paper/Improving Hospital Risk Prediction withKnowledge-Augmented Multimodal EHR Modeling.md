---
title: 
draft: false
tags:
  - in-progress
---
 The summary 
 **Paper:** _Improving Hospital Risk Prediction with Knowledge-Augmented Multimodal EHR Modeling [KAMELEON](https://arxiv.org/pdf/2508.01970)  
 
**Goal:** Predict 30-day readmission and in-hospital mortality using a combination of structured EHR data and unstructured clinical notes, enhanced by external biomedical knowledge (PubMed, UMLS).

**Core Idea:**  
They propose **KAMELEON**, a **two-stage framework**:

1. **M1 (Unstructured model):** fine-tuned LLM that extracts reasoning and predictions from clinical notes, supported by a biomedical knowledge graph.
    
2. **M2 (Structured model):** uses structured EHR data (vitals, labs, demographics) _plus_ embeddings and reasoning from M1 for final prediction.
    

This combination of _LLM reasoning + structured machine learning_ outperforms existing baselines like Llama-Med, MedGemma, and traditional logistic regression or LSTMs.

From paper:
To the best of our knowledge, this is one of the first frameworks for healthcare prediction which enhances the power of an LLM-based graph-guided knowledge retrieval method by combining it with structured data for improved clinical outcome prediction.

The methodology : 

|Component|Role|Why it matters|
|---|---|---|
|**LLM fine-tuning (M1)**|Extracts contextual reasoning from physician notes and enriches them with PubMed knowledge graphs|Helps ground the LLM in biomedical facts, reducing hallucinations|
|**Knowledge Graph**|Uses PubMed + UMLS to build structured connections between medical concepts|Adds domain grounding beyond raw text|
|**Structured Model (M2)**|Integrates all structured EHR features + embeddings from LLM reasoning|Enables multimodal learning|
|**Reasoning Embedding**|LLM generates “rationale text”; they embed that for the second stage|Novel — bridges symbolic reasoning with numerical learning|

Prompt - In zero-shot setting , with reasoning 


Critical Log :
-- As per the given gist, did it actually helped in improving any sort of clinical outcome, or was it resulted to the just improving the metrics?

-- And, why the two stage? What would have happened if it would have trained as an end - to - end multimodal model

--  What happens if they replace the LLM with a smaller medical transformer (like ClinicalBERT)?

-- Could the reasoning ever be factually wrong but still predictive?

-- What about the medical data from non-US healthcare systems/clinics/hospitals? 

-- The LLM’s reasoning text improves performance — but how reliable is that reasoning? Can clinicians trust it?

About [SHAP analysis](https://www.datacamp.com/tutorial/introduction-to-shap-values-machine-learning-interpretability) 

The paper and the highlights : 

KAMELEON Framework

We propose a hybrid framework, KAMELEON, that integrates multimodal EHR data, including structured clinical components and unstructured physician notes (we will provide more details in **Section 2.1), and external biomedical knowledge to predict two key clinical outcomes: in-hospital mortality and 30-day read- mission.** As shown in Figure 1, KAMELEON **consists of two components**: (1) an **unstructured encoder** M1 (Section 4.2.1) *that processes clinical notes and retrieves relevant biomedical knowledge using a PubMed- derived graph and knowledge-augmented reasoning, and outputs a prediction, along with its reasoning;* and (2) **a structured encoder** M2 (Section 4.2.2) *that combines multiple time-series corresponding to vitals and tabular datasets (labs, medications, etc), along with the outputs from M1 (i.e., both the prediction and the embedding associated with the reasoning it produces) with static features for downstream prediction.*


This work underscores the significant potential of knowledge-augmented multimodal EHR modeling to enhance early intervention, optimize resource allocation, and improve patient care in complex clinical settings. While LLMs, including medical LLMs trained on specialized data, have a number of limitations in terms of accuracy and hallucinations, their reasoning outputs provide valuable predictive power.

we use PubMed literature parsed into knowledge triples (subject–relation–object) via an LLM-based extraction pipeline.

----
