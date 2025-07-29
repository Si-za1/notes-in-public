---
title: LLM evaluation
draft: false
tags:
  - in-progress
---
 
**What Are LLM-Evaluators?**

- **LLM‑evaluators** (or **LLM‑as‑a‑Judge**) are large language models used to assess the quality of outputs from other LLMs—for tasks like summarization, translation, or dialogue.
    
- They have risen in popularity because traditional automatic metrics (like BLEU or ROUGE) often fail on open-ended, semantic-heavy tasks.
    
- As a scalable alternative to human annotation, LLM‑evaluators offer deeper understanding but introduce trade‑offs in interpretability and cost

**Key Considerations Before Using an LLM-Evaluator**

- **Baseline comparison**: Are you evaluating against human labels or a fine-tuned classifier? Matching human-level alignment is easier than competing with a specialized model.
    
- **Cost and latency**: LLM-evaluators typically cost more and have higher latency than smaller finetuned models, especially if generating chain-of-thought working.
    
- **Task trade-offs**: Determine whether you're using _direct scoring_ (e.g., “rate from 1 to 5”) or _pairwise comparison_ (e.g., “which is better?”), and whether you're evaluating via classification or correlation metrics.

