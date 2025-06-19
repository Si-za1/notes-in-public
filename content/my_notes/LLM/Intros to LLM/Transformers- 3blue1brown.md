---
title: Transformers- 3blue1brown
draft: false
tags:
  - complete
---
 
Video 5 - 
Takeaway from the video

Google , in 2017, introduced transformers. 

**GPT : Generative Pretrained Transformer.**

- **Generative**: Creates new text.
    
- **Pretrained**: Learned from a large dataset before fine-tuning.
    
- **Transformer**: A type of neural network model at the heart of modern AI.

## **Inside a Transformer**

- **High-level overview**:
    
    - Input is split into **tokens**: pieces of words or characters.
        
    - Each token is assigned a **vector**: list of numbers representing meaning.
        
- **Vector space**:
    
    - Similar meanings = vectors close in space.
        
    - Vectors go through:
        
        1. **Attention block**: vectors communicate and update based on context.
            
            - Example: "model" in "machine learning model" ≠ "fashion model".
                
        2. **Feedforward block (MLP)**: each vector updated independently.
            
- Operations involve **matrix multiplications**.
    
- Process repeats: alternating attention and feedforward blocks.
    
- Final output: a probability distribution over possible next tokens.
    
- **Training**:
    
    - Use of **system prompt** to simulate user-AI interaction.
        
    - Predict next response based on user input.

## **The Premise of Deep Learning**

- **Machine Learning (ML)**: Uses data to determine model behavior.
    
- Instead of hard-coding, ML models:
    
    - Use flexible structures with **parameters** (knobs and dials).
        
    - Learn by adjusting these parameters to mimic desired behavior.
        
- **Example**: Linear regression


## **Word Embeddings**

- **First step**: Turn words/tokens into vectors using **embedding matrix** (`W_E`).
    
    - Embedding: represents words as coordinates in high-dimensional space.
        
- **Embedding properties**:
    
    - Similar words = similar vectors.
        
    - Example: `king - man + woman ≈ queen`.
        
- **Dimensions**:
    
    - GPT-3: 50,257 tokens, embedding size 12,288.
        
    - Total embedding weights = ~617 million.
        
- **Meaning in directions**:
    
    - Vectors encode semantics:
        
        - Gender, nationality, food, family, etc.
            
    - Dot product measures similarity (alignment of directions).
        
    - Plurality and number encoded in vector directions.

Embeddings do not only represent the vectors, but also, - **Position** of word in sequence. **Contextual meaning** (updated throughout network).

**Context size**:

- GPT-3: 2048 tokens.
- Limits how much text can be considered in predictions.


## **Unembedding**

- **Goal**: Produce a probability distribution of next token.
    
- Steps:
    
    1. Use **unembedding matrix** (`W_U`) to map last vector to 50,000 values (logits).
        
    2. Apply **softmax** to convert logits into probabilities.
        
- **Why only last vector?**
    
    - Training efficiency: each vector in final layer predicts its own next token.
        
- `W_U` matrix:
    
    - Rows = tokens, columns = embedding dimensions.
        
    - Another 617 million parameters.

## **Softmax with Temperature**

- **Softmax**:
    
    - Converts logits (unnormalized values) to probabilities.
        
    - Formula:
        
        - `softmax(x_i) = e^(x_i) / Σ e^(x_j)`
            
        - Ensures outputs are all positive and sum to 1.
            
- **Temperature (T)**:
    
    - Controls randomness.
        
    - High T → more uniform (creative/random).
        
    - Low T → sharper focus on max value (predictable).
        
    - T = 0 → always picks the highest probability.
        
- **Sampling example**:
    
    - T = 0 → story becomes repetitive (e.g., Goldilocks).
        
    - T = high → starts original, may become nonsensical.
        
- **Logits**: Raw output values before softmax.

**Attention : heart of the transformer** 
For example, the meaning of the word model in the phrase "a machine learning
model" is different from its meaning in the phrase "a fashion model".
The attention block is what's responsible for figuring out which
words in context are relevant to updating the meanings of which other words,
and how exactly those meanings should be updated.