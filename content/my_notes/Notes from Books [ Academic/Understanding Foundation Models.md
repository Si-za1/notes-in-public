---
title: Understanding Foundation Models
draft: false
tags:
  - in-progress
---
 

A model’s training process is often divided into pre- training and post-training. Pre-training makes a model capable, but not necessarily safe or easy to use. This is where post-training comes in. The goal of post-training is to align the model with human preferences.

Sampling is how a model chooses an output from all possible options.
If you want a model to improve on a certain task, you might want to include more data for that task in the training data.

Understanding Transformer architecture

seq2seq contains an encoder that processes inputs and a decoder that generates outputs. Both inputs and outputs are sequences of tokens, hence the name. In its most basic form, the encoder processes the input tokens sequentially, outputting the final hidden state that represents the input. The decoder then generates output tokens sequentially, conditioned on both the final hidden state of the input and the previously generated token.
Seq2seq uses RNNs (recurrent neural networks) as its encoder and decoder.

The attention mechanism allows the model to weigh the importance of differ‐ ent input tokens when generating each output token. This is like generating answers by referencing any page in the book.

The transformer architecture dispenses with RNNs entirely. With transformers, the input tokens can be processed in parallel, significantly speeding up input processing. While the transformer removes the sequential input bottleneck, transformer-based autoregressive language models still have the sequential output bottleneck.

