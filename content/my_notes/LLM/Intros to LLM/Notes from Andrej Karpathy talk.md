---
title: Notes from Andrea Karpathy video
draft: false
tags:
  - complete
---
 
# Notes on Andrej Karpathy's Talk: Building ChatGPT, Transformers, nanoGPT, and Shakespeare

## What is ChatGPT and How It Works

- ChatGPT is a language model that generates text from left to right, one token at a time.
    
- It's a probabilistic system: the same prompt can produce different responses.
    
- Examples include haikus, breaking news about a falling leaf, jokes, fictional news articles, etc.
    
- It is fundamentally a **language model**, meaning it learns how tokens (words/characters) follow each other.
    
- Its job is to complete sequences of text based on given input.
    

## The Architecture Behind ChatGPT

- GPT stands for **Generative Pretrained Transformer**.
    
- The backbone of GPT is the **Transformer architecture** introduced in the 2017 paper "Attention is All You Need".
    
- Originally used for machine translation, the Transformer became foundational to modern AI.
    
- The model was pretrained on large-scale internet data and then fine-tuned.
    

## Building a Mini ChatGPT from Scratch

- Karpathy proposes we train a **character-level language model**.
    
- Dataset: **tiny Shakespeare** (~1MB) with all of Shakespeare's works in a single text file.
    
- We aim to predict the next character based on previous ones.
    
- Final goal: generate Shakespeare-like text character by character.
    

## Tokenization

- The text is tokenized at the **character level**.
    
- 65 unique characters form the vocabulary.
    
- Simple encoding/decoding: map chars to ints and vice versa.
    
- GPT uses a more complex subword tokenizer (e.g., byte pair encoding, tiktoken).
    
- Tradeoff: simple character-level tokenization → long sequences, easy code.
    

## Data Preparation

- Entire text turned into a single long sequence of integers.
    
- Data split into **90% training** and **10% validation**.
    

## Feeding Data to the Model

- We use **chunks** (aka blocks) of text instead of full sequences to train.
    
- Define a `block_size` (e.g., 8), which defines the context window.
    
- Each block of length `block_size + 1` gives us `block_size` training examples.
    
- We generate X (input) and y (target) pairs for every chunk.
    
- This helps model learn to predict next character at each position.
    

## Batch Dimension

- Instead of training on one chunk, we train on **batches** (multiple chunks at once).
    
- This improves efficiency and GPU utilization.
    
- Batches are processed independently; they do not interact.
    

## First Model: Bigram Language Model

- Start with the simplest neural model: bigram model.
    
- Embedding table maps each input token to a vector.
    
- Logits are computed directly from embeddings.
    
- Cross-entropy loss is used to evaluate performance.
    

## Generating Text from Bigram Model

- Uses the `generate` function to extend a sequence by predicting tokens one by one.
    
- Starts with an initial token (e.g., newline = 0).
    
- At first, output is random (untrained model).
    
- Generation looks silly at first, but improves with training.
    

## Training the Model

- Optimizer: **Adam** (better than SGD for this task).
    
- Trains using mini-batches sampled randomly from training set.
    
- Training loop: sample batch, compute loss, backpropagate, update weights.
    
- After enough iterations, model loss improves, and generated text becomes more coherent.
    

## Turning Notebook into Script

- Converted notebook code into a standalone script.
    
- Added:
    
    - GPU support (if available).
        
    - Smoothed loss reporting using multiple evaluation batches.
        
    - Separation of train/eval mode.
        
    - `torch.no_grad()` for evaluation to save memory.
        

## From Bigram to Transformer: Self-Attention

- Bigram model only considers one character — we want context.
    
- Goal: allow **tokens to communicate** based on history.
    

### Naive Communication (Version 1)

- Average all previous tokens to create a new vector at each time step.
    
- Inefficient: uses for-loops over time.
    
- Very lossy: doesn't preserve structure.
    

### Matrix Multiply for Aggregation (Version 2)

- Used lower-triangular matrix to ensure only past tokens contribute.
    
- Allows efficient aggregation using **batched matrix multiplication**.
    

### Softmax-Based Attention (Version 3)

- Use `torch.tril()` to mask future tokens (causal mask).
    
- Apply softmax to turn affinities into probabilities.
    
- Enables **weighted sum** instead of uniform average.
    

## The Self-Attention Mechanism (Version 4)

- Each token emits:
    
    - **Query**: what it's looking for.
        
    - **Key**: what it offers.
        
    - **Value**: what it shares if selected.
        
- Attention weights = dot product of query and key.
    
- Use softmax on attention weights → probabilities.
    
- Final result = weighted sum of **values**, not raw inputs.
    

## Important Notes on Self-Attention

1. **Attention = Communication**
    
    - Tokens form a directed graph, passing weighted information.
        
    - In our case: token i can only attend to tokens before it.
        
2. **No Spatial Bias**
    
    - Attention operates over **sets**, not grids.
        
    - We add **positional encodings** to inform the model of order.
        
3. **No Batch Communication**
    
    - Each batch is processed independently.
        
    - Matrix multiplications are batched but isolated.
        
4. **Decoder vs Encoder Blocks**
    
    - Decoder blocks (like in GPT): future tokens **masked**.
        
    - Encoder blocks: full attention (used in BERT, etc.).
        
5. **Self vs Cross Attention**
    
    - Self-attention: queries, keys, values from same input.
        
    - Cross-attention: queries come from one source; keys/values from another (e.g., in encoder-decoder setups).
        
6. **Scaled Dot Product Attention**
    
    - We divide dot product by sqrt(head size) to normalize variance.
        
    - Prevents softmax from becoming too "peaky" at init.
        

Self-attention lets tokens look back at others and decide which ones are important. That’s how context builds up.
