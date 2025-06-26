---
title: Encoders and Decoders
draft: false
tags:
  - complete
---
## Encoders and Decoders

In Transformer models, these are distinct components. The **encoder** processes the input text, converting it into numerical values known as embeddings. The **decoder** then uses these embeddings to generate output text.

### Decoding Strategies

- **Greedy Decoding** - Picks the most likely next word at each step. Efficient but can lead to suboptimal sequences.
- **Beam Search** - Tracks a number of possible sequences (beam width) to find a better sequence of words. It balances between the best local and overall choices.
- **Top-K Sampling** - Randomly picks the next word from the top K most likely candidates, introducing randomness and diversity.
- **Top-P (Nucleus) Sampling**: Chooses words from a set whose cumulative probability exceeds a threshold, focusing on high-probability options.

![reflects how the decoding process takes the encoder output as its input, vectorizes it for embeddings and other mechanisms that so it can generate the required output.](https://video.udacity-data.com/topher/2023/December/6571e984_screen-shot-2023-12-07-at-10.49.03-am/screen-shot-2023-12-07-at-10.49.03-am.jpeg)

**The Decoding Process**

#### Temperature Setting

This model setting controls the randomness of token predictions. A higher temperature leads to more randomness, while a lower temperature makes the model more confident (less random) in its predictions.