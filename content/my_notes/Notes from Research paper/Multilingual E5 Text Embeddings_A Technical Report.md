---
title: Multilingual E5 Text Embeddings_A Technical Report
draft: false
tags:
  - notes
---
 Link: 1. [https://arxiv.org/pdf/2402.05672](https://arxiv.org/pdf/2402.05672)
 
Text embeddings serve as fundamental components in information retrieval systems and retrievalaugmented language models. Despite their significance, most existing embedding models are trained exclusively on English text.

we present the multilingual E5 text embedding models (mE5-{small / base / large}), which extend the English E5 models (Wang et al., 2022). The training procedure

The training procedure adheres to the **original two-stage methodology:** _weakly-supervised contrastive pre-training on billions of text pairs, followed by supervised finetuning on small quantity of high-quality labeled data._

Most source seems to be normal random conversation, and almost most covers the structured formatted language.

**Weakly supervised contrastive pre-training model :**

continually pre-train our model on a diverse mixture of multilingual text pairs obtained from various sources as listed in Table 1. The models are trained with a large batch size 32k for a total of 30k steps, which approximately goes over ∼ 1 billion text pairs.

**Supervised Fine-tuning**

In the second stage, we fine-tune the models from the previous stage on a combination of high-quality labeled datasets.

How is the model trained and is checked upon the performance for the English and multilingual benchmark?

Multilingual retrieval on the development set of the **MIRACL benchmark.** Numbers are averaged over 16 languages.

**Multilingual and English-only models on the MTEB benchmark** (Muennighoff et al., 2023). Our best mE5 model surpasses the previous state-of-the-art multilingual model Cohere multilingual-v3, by **0.4 points** and outperforms a strong **English-only model, BGElarge-en-v1.5, by 0.2 points**

Bitext Mining is a cross-lingual similarity search task that requires the matching of two sentences with little lexical overlap.

Bitext mining in models refers to **the process of finding parallel (translated) sentence pairs in monolingual corpora to create pseudo-parallel corpora for machine translation (MT) from unaligned text.**

This technique involves using multilingual BERT to create source and target sentence embeddings for nearest-neighbor search and adapting the model via self-training.

_The goal is to improve unsupervised translation performance by supplementing existing models with mined pseudo-parallel text, which can boost BLEU scores on tasks like WMT'14 French-English and WMT'16 German-English._

Lexical similarity is **a measure of the degree to which the word sets of two given languages are similar**.

practitioners can leverage these models for information retrieval, semantic similarity, and clustering tasks across a diverse range of languages
