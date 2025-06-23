---
title: Where Facts in LLMs Live
draft: false
tags:
  - in-progress
---
### Where Facts in LLMs Live

- If LLMs can complete "Michael Jordan plays the sport of ___" with "basketball", that shows **factual knowledge is stored** somewhere in the model.
    
- DeepMind researchers explored where these facts live — result: **facts live mostly in the MLPs (multi-layer perceptrons)**, not attention blocks.
    
- So when we query something like “Michael Jordan basketball”, the MLPs help produce the right output.


### How Transformers Process Text (Quick Recap)

- Text → broken into tokens → each token becomes a **high-dimensional vector**.
    
- Each vector flows through:
    
    - **Attention blocks** (context sharing)
        
    - **MLP blocks** (where most of the parameters live)
        
    - **Normalization** steps
        
- Goal: Every token vector gets enriched with both **contextual info** and **general knowledge**, to predict the next token.




**### High-Dimensional Space

- Vectors live in a high-dimensional space.
    
- Directions can encode **features** like gender, role, or meaning.
    
    - e.g., `woman - man + uncle ≈ aunt`
        
- These features aren't just for words — they're for **context-rich representations**.
    
- MLPs help **store and add meaningful directions** like “basketball” when "Michael Jordan" is detected.**


### How MLPs Might Store Facts

- MLP = simple 2-step feedforward network with:
    
    1. **Matrix multiply (W_up) + bias → ReLU activation**
        
    2. **Second matrix (W_down) + bias → added back to original vector**
        
- example:  
    Suppose a vector encodes:
    
    - dot product with "Michael" direction = 1
        
    - dot product with "Jordan" direction = 1  
        → Then, MLP block activates a "Michael Jordan" neuron.
        
- That neuron adds a **"basketball" direction** back to the vector → output now encodes: Michael + Jordan + basketball.
- This process takes place in parallel which means
*linear + ReLU + linear = output + first linear [ the original matrix added here]*

### uperposition Hypothesis

- Real models don’t use one neuron per fact.
    
- Instead, they use **superposition**: many features share neurons.
    
- In high-dimensional space, many directions can be nearly perpendicular.
    
    - This allows **many features to coexist** in one space.
        
    - It scales better and stores more info compactly.
        
    - Supported by math (e.g., Johnson-Lindenstrauss lemma)


Summary,
-- Attention handles **context**
    
- **MLPs store factual knowledge**
    
- Each vector carries rich, blended meaning — words + context + world knowledge
    
- Transformers scale because they can **compress and store lots of overlapping facts** using high-dimensional geometry and superposition.

This is my take from the video : [link](https://www.youtube.com/watch?v=9-Jl0dxWQs8&list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi&index=10&ab_channel=3Blue1Brown) 
there a whole lot of mathematics going on, seems like the next thing i need to understand will be dot products, matrices, terms like bias, neurons and much more... 

