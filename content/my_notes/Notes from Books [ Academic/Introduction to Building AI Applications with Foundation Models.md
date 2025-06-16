---
title: Introduction to Building AI Applications with Foundation Models
draft: false
tags: []
---
AI engineering - the process of building applications on top of readily available models—into one of the fastest- growing engineering disciplines.

Language models

A language model encodes statistical information about one or more languages.

The basic unit of a language model is token. A token can be a character, a word, or a part of a word (like -tion), depending on the model.

The process of breaking the original text into tokens is called tokenization. For GPT-4, an average token is approximately 3⁄4 the length of a word. So, 100 tokens are approximately 75 words.

Why do language models use token as their unit instead of word or character? There are three main reasons:

1. *Compared to characters, tokens allow the model to break words into meaningful components*. For example, “cooking” can be broken into “cook” and “ing”, with both components carrying some meaning of the original word.
    
2. *Because there are fewer unique tokens than unique words, this reduces the model’s vocabulary size, making the model more efficient*.
    
3. *Tokens also help the model process unknown words.* For instance, a made-up word like “chatgpting” could be split into “chatgpt” and “ing”, helping the model understand its struc‐ ture. Tokens balance having fewer units than words while retaining more meaning than individual characters.

There are two different types of language models based on what information they can use to predict a token 
1. Masked language model

A masked language model is trained to predict missing tokens anywhere in a sequence, using the context from both before and after the missing tokens. masked language models are commonly used for non-generative tasks such as sentiment analysis and text classification.

2. Autoregressive language model

An autoregressive language model is trained to predict the next token in a sequence, using only the preceding tokens. autoregressive language models are the models of choice for text generation. 

What is Generative AI?
A model that can generate open-ended outputs is called generative, hence the term generative AI.
Open ended outputs mean - finite vocabulary to construct infinite possible outputs.

**Supervision** refers to the process of training ML algorithms using labeled data, which can be expensive and slow to obtain. Self- supervision helps overcome this data labeling bottleneck to create larger datasets for models to learn from, effectively allowing models to scale up.

**Self-supervision** helps overcome the data labeling bottleneck. In self-supervision, instead of requiring explicit labels, the model can infer labels from the input data. Language modeling is self-supervised because each input sequence provides both the labels (tokens to be predicted) and the contexts the model can use to predict these labels.

A model’s size is typically measured by its number of parameters. A parameter is a vari‐ able within an ML model that is updated through the training process.

![[Pasted image 20250616212900.png]]