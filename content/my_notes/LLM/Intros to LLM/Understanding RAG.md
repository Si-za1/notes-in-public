---
title: Understanding RAG
draft: true
tags:
  - complete
---
### **Everyone's Favorite Word: RAG**  
*(Because who doesn’t love stuffing LLMs with fresh knowledge?)*  

#### **Let’s Break Down the Buzzword**  
**RAG = Retrieval-Augmented Generation**  
- **Retriever**: The **"Google"** part. This is what searches external databases (like Wikipedia, your company docs, your internal documents) for relevant info.  
- **Augmented**: The **"upgrade"** part. Takes the **retrieved documents** and **combines them with the original query**.
   This is **not just "real-time data"**—it’s about dynamically conditioning the LLM on external evidence. The augmentation happens **before generation**, modifying the LLM’s input context (via prompt engineering or model architecture).
- **Generation**: The "GPT" part. - The LLM (e.g., GPT, BART, LLaMA) generates a response **conditioned on both the query and retrieved docs**. **Prompt engineering** helps, but advanced RAG systems (like in the original paper) train the retriever and generator **end-to-end**.- Pure GPT **hallucinates** from parametric memory; RAG **constrains outputs** to retrieved evidence.
---

### **Why RAG? (The LLM ER Doctor)**  
LLMs are brilliant but flawed. RAG fixes their biggest issues:  
Retrieval-Augmented Generation (RAG) emerged as a critical fix for large language models (LLMs) like GPT, which—despite their brilliance—suffer from three fatal flaws: **hallucinations, outdated knowledge, and opaque answers**. As I went deeper into research this is where I came across the story of why RAG became indispensable:
#### **Origins: The Birth of RAG**

The concept of combining retrieval with generation isn’t new—it traces back to early question-answering systems like IBM’s Watson (2011) and even 1970s NLP prototypes. However, the term "RAG" was coined in 2020 by Meta AI researchers (Lewis et al.) in a landmark paper. Their breakthrough? A **general-purpose framework** that dynamically retrieves documents (e.g., Wikipedia) and feeds them to LLMs like BART to ground responses in evidence.

#### **When RAG Became Non-Negotiable**

By 2023–2024, RAG transitioned from a research novelty to a **must-have** for enterprises, driven by:

- **High-profile LLM failures**: Google Bard’s $100B stock blunder (incorrect JWST facts) and lawyers citing fake cases (e.g., _Morgan & Morgan’s ChatGPT disaster_).
    
- **Exploding enterprise demand**: Companies realized static LLMs couldn’t handle internal docs or real-time data. RAG offered a **cost-effective alternative to retraining**.
    
- **Legal/medical compliance**: Fields like law and healthcare demanded traceable, up-to-date answers. RAG’s citations (e.g., "Per §2.1 of FDA guidelines...") made it the only viable option.

#### **How RAG Is Used Today**

To be honest, RAG didn’t just patch LLMs—it reinvented how AI interacts with knowledge, making it the **ER doctor** for generative AI’s chronic flaws. 

**Popular Uses**:  
- - **Customer service bots** (e.g., IBM’s Watsonx) that pull from internal FAQs/knowledge bases.
- **Legal research tools** (e.g., Harvey AI) to prevent hallucinated case law.
- **Medical diagnostics** (e.g., retrieving the latest NIH studies for doctors).
- **Enterprise "knowledge engines"** (e.g., NVIDIA’s NeMo Retriever) for employees querying internal data

RAG is evolving into **multimodal systems** (text + images) and **self-improving agents** (e.g., AWS’s Bedrock with real-time API calls). Its adoption is now table stakes—Gartner’s 2024 Hype Cycle urged enterprises to "prioritize RAG investments" or risk obsolete.
_Key Sources_:

- Meta’s 2020 RAG paper
- IBM’s enterprise RAG guide
- McKinsey’s legal/healthcare case studies
- NVIDIA’s blueprint for real-time retrieval

*Sources: 
[GitHub Blog](https://github.blog/ai-and-ml/generative-ai/what-is-retrieval-augmented-generation-and-what-does-it-do-for-generative-ai/),  
[IBM Research](http://research.ibm.com/blog/retrieval-augmented-generation-RAG),  
[Wikipedia - RAG](https://en.wikipedia.org/wiki/Retrieval-augmented_generation),  
[IBM Think](https://www.ibm.com/think/topics/retrieval-augmented-generation),  
[GitHub Topics - RAG](https://github.com/topics/retrieval-augmented-generation),  
[IBM Architectures - RAG](https://www.ibm.com/architectures/hybrid/genai-rag)
[Cost-effectiveness, real-time updates](https://aws.amazon.com/what-is/retrieval-augmented-generation/)

---
So, this was the overview I gathered from most of the blogs, articles, and tutorials I explored.

-----
### Beginning

In the meantime, during a visit to Wikipedia, I came across a paper titled _["Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks" (Lewis et al., 2020)](https://arxiv.org/abs/2005.11401)_. It turned out to be well worth my time for a thorough read.

I didn’t approach the paper with the goal of gaining a deep, technical understanding right away. Instead, I focused on grasping the core ideas and key takeaways, and I made notes accordingly.

The foundational paper introduces RAG as a sequence-to-sequence model with a retriever-generator setup. Key takeaways:
#### **The Two-Part Engine**

The paper frames RAG as a **retriever-generator duo**, each with specialized roles:

- **Dense Passage Retriever (DPR)**:
    
    - Works like a "semantic detective":
        
        - Encodes queries/documents into **dense vectors** (think: numerical fingerprints).
            
        - Uses **Maximum Inner Product Search (MIPS)** over a FAISS index for lightning-fast lookups.
            
    - `Point`: It’s **trained end-to-end** with the generator (not a separate module).
        
- **Generator (BART)**:
    
    - The "storyteller": Takes retrieved docs + query, produces fluent answers.
        
    - Unlike raw BART, it’s **conditioned on external evidence**—like a student citing sources.
        

Something: The retriever isn’t just fetching random docs—it learns to retrieve what **maximizes the generator’s confidence** in correct answers.

- **Training**: Jointly optimizes retrieval and generation via marginalization over retrieved documents.
    
- **Results**: Outperforms pure generative models in open-domain QA tasks (e.g., Natural Questions, WebQuestions).
    
- **Flexibility**: The retriever can access dynamic/updated corpora, unlike static LLMs.

- In short:
    
    1. **Dense Passage Retriever (DPR)**: Uses dense embeddings to fetch top-k relevant passages.
        
    2. **Generator**: A pre-trained seq2seq transformer (BART) conditioned on retrieved documents.


**How did they train ?**

 The retriever and generator are trained **jointly**, not separately. The model learns to retrieve documents that help generation (via marginal likelihood). Contrast this with older "retrieve-then-read" systems where retrieval was fixed.

- **Joint optimization**: The model doesn’t just train the generator—it **backpropagates through retrieval choices**.
- **Marginalization**: For each query, it considers multiple possible documents (not just the top-1), making it robust to noisy retrievals.
- **No fine-tuning needed**: The retriever and generator start from **pre-trained** DPR and BART, saving compute costs.
#### **Retrieval Mechanism**:

- **Query Encoding**: Converts user queries into vectors using a pre-trained BERT model.
- **Document Indexing**: Wikipedia articles are pre-encoded into a vector database (FAISS) for fast similarity search.
#### **Generation**:

- The generator (BART) synthesizes responses by integrating retrieved documents and its parametric knowledge

#### **Why It Outperformed Pure LLMs**

The paper tested RAG on **open-domain QA** (Natural Questions, WebQuestions):

- **GPT-3**: RAG scored higher because it could **cite up-to-date docs** (GPT-3’s knowledge was frozen in training).
    
- **Retrieve-then-Read systems**: RAG’s **end-to-end training** meant retrieval improved generation (older systems treated them as separate steps).

_Example from the paper_:

- **Query**: "When was the first electric car invented?"
    
- **Retriever fetches**: A Wikipedia passage about 19th-century prototypes.
    
- **Generator outputs**: "The first practical electric car was built by Thomas Parker in 1884, per Wikipedia." _(Note: traceable + factual!)_


`Flexibility` 

- **Dynamic knowledge**: Swap the document corpus anytime—no model retraining needed.
    
- **Two modes**:
    
    - **RAG-Sequence**: Uses one doc per output (good for focused answers).
        
    - **RAG-Token**: Can switch docs mid-generation (better for multi-fact queries).


**This wasn’t just another model—it **redefined how LLMs access knowledge**:

- Proved retrieval + generation could be **jointly trained** (not pipelined).
    
- Inspired later work like **REPLUG, Atlas**, and enterprise RAG systems.

### **Experiments and Results**

#### **Datasets**:

- Evaluated on **open-domain QA tasks**: Natural Questions (NQ), WebQuestions (WQ), and CuratedTREC.
    
- Compared against:
    - **Parametric-only models** (e.g., BART, T5).
    - **Retrieve-and-extract models** (e.g., ORQA, REALM)

#### **Key Findings**:

- **State-of-the-art Performance**: RAG outperformed pure generative models and task-specific architectures on QA tasks.
- **Factual Accuracy**: Reduced hallucinations by grounding responses in retrieved evidence.
- **Diversity**: Generated more specific and varied responses compared to parametric-only models.

##### **Limitations Noticed**

- **Retrieval bottlenecks**: Speed/accuracy depends on the document corpus quality.
- **Noisy documents**: Irrelevant retrievals can mislead the generator.