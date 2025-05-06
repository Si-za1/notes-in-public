---
title: Working with BERT score
draft: false
tags:
  - notes
---
# The working mechanism

We use contextual embeddings to represent the tokens in the input sentences x and ˆx, which means it can generate different vector representations for the same word in different sentences depending on the surrounding words, which form the context of the target word.

The complete score matches each token in x to a token in ˆx to compute recall, and each token in ˆx to a token in x to compute precision. Because we use pre-normalized vectors, our computed scores have the same numerical range of cosine similarity (between −1 and 1).

And also, we use contextual embeddings, which capture the specific use of a token in a sentence, and potentially capture sequence information. We do not use external tools to generate linguistic structures, which makes our approach relatively simple and portable to new languages.

The core idea behind BERTScore is that it doesn't just match words or phrases directly; instead, it compares their meanings in the context of the entire sentence or passage, as understood by the BERT model. To do this:

1. **BERT embeddings**: Each word in the reference and hypothesis is mapped to its contextualized embedding (vector) using BERT.
2. **Cosine similarity**: BERTScore then computes the cosine similarity between the embeddings of the corresponding tokens in both texts. Higher cosine similarity means the words or phrases are more semantically similar.
3. **Precision, recall, and F1 score**: BERTScore can be used to calculate three different scores:
    - **Precision**: How much of the hypothesis is semantically similar to the reference.
    - **Recall**: How much of the reference is semantically similar to the hypothesis.
    - **F1 score**: The harmonic mean of precision and recall.

BERTScore is seen as a more effective measure of semantic similarity than traditional word-overlap based metrics like BLEU, ROUGE, or METEOR, because it better captures the meanings of words in context.

## The scoring system

**Precision, recall, and F1 score**: BERTScore can be used to calculate three different scores:

- **Precision**: How much of the hypothesis is semantically similar to the reference.
- **Recall**: How much of the reference is semantically similar to the hypothesis.
- **F1 score**: The harmonic mean of precision and recall.

### The score meaning

They are indicators of how well the model-generated text (the "hypothesis") semantically aligns with the reference text. For instance, let’s take a look at one of the example mentioned below:

### 1. **Precision (0.4743)**

- **What it means**: Precision measures how much of the hypothesis (the model-generated text) is semantically similar to the reference (the ideal text). A precision score of **0.4743** means that about **47.43%** of the tokens in the hypothesis are relevant and match the reference in terms of meaning, based on the BERT embeddings.
- **Interpretation**: The precision score is relatively low, suggesting that a significant portion of the tokens in the hypothesis are not capturing the meaning of the reference text, or that there is a fair amount of "noise" (irrelevant or unrelated content) in the generated text.

### 2. **Recall (0.7653)**

- **What it means**: Recall measures how much of the reference is covered by the hypothesis in terms of semantic similarity. A recall score of **0.7653** means that about **76.53%** of the tokens in the reference text are represented in the hypothesis in terms of meaning.
- **Interpretation**: The recall score is quite high, which indicates that the generated text covers a good portion of the relevant content from the reference. This suggests that the model is fairly good at including key concepts from the reference text.

### 3. **F1 Score (0.5857)**

- **What it means**: The F1 score is the harmonic mean of precision and recall, balancing the two metrics. An F1 score of **0.5857** means the model's performance on both precision and recall is moderate. This score reflects the trade-off between how much of the hypothesis matches the reference (precision) and how much of the reference is captured (recall).
- **Interpretation**: An F1 score of 0.5857 is generally considered a **moderate performance**. It indicates that the model is doing okay, but there’s room for improvement, particularly in terms of precision (which is a bit low).

### Overall Interpretation:

- The high **recall** score suggests that the generated text is quite comprehensive in terms of covering the relevant content from the reference, but the **low precision** score indicates that some of the content in the generated text might not align well with the reference in terms of meaning.
- The **moderate F1 score** indicates that, overall, the model has a balanced but imperfect performance. The content it generates is somewhat relevant, but there is room for improvement in both relevance and accuracy.

### Why the harmonic mean?

To explain, consider for example, what the average of 30mph and 40mph is? if you drive for 1 hour at each speed, the average speed over the 2 hours is indeed the arithmetic average, 35mph.

However if you drive for the same distance at each speed -- say 10 miles -- then the average speed over 20 miles is the harmonic mean of 30 and 40, about 34.3mph.

The reason is that for the average to be valid, you really need the values to be in the same scaled units. Miles per hour need to be compared over the same number of hours; to compare over the same number of miles you need to average hours per mile instead, which is exactly what the harmonic mean does.

Precision and recall both have true positives in the numerator, and different denominators. To average them it really only makes sense to average their reciprocals, thus the harmonic mean.

# How is it different than the word embedding approach?

Both the process of **finding similarity based on word embeddings** (like using **Word2Vec**, **GloVe**, or **fastText**) and **BERTScore** involve comparing word or sentence-level meanings using embeddings and computing a similarity score, typically **cosine similarity**. However, there are important differences in the **approach** and **underlying mechanisms** that set **BERTScore** apart. Let's break down the key differences:

### 1. **Contextual vs. Static Embeddings**:

### Word Embeddings (e.g., Word2Vec, GloVe):

- **Word2Vec**, **GloVe**, and other traditional word embeddings are **static** embeddings.
- This means that each word is represented by a **fixed vector** regardless of the context in which it appears. For example, the word "bank" will have the same vector whether it's used in the context of a financial institution or the side of a river.
- The **similarity** between words is computed by comparing the vectors of individual words. This works well for many tasks, but can lead to ambiguity issues when words appear in different contexts with different meanings.

### BERTScore:

- **BERTScore** uses **contextual embeddings** generated by models like **BERT** (Bidirectional Encoder Representations from Transformers). This means that the **vector representation of a word** changes depending on the words around it in the sentence.
- For example, the word "bank" in "I went to the bank to deposit money" will have a different embedding from the word "bank" in "The river bank was flooded." The context of each sentence is taken into account, making BERTScore much more flexible and accurate in capturing nuanced meaning.
- BERTScore leverages the entire sentence (or context) when computing embeddings for individual words, which is a major improvement over traditional, context-independent models.

### 2. **Sentence-Level vs. Token-Level Similarity**:

### Word Embeddings (e.g., Word2Vec, GloVe):

- In traditional word embeddings, the focus is typically on **word-level similarity**. To calculate sentence-level similarity, you'd often take an **average** or **sum** of the individual word vectors to represent the entire sentence. This approach doesn't account for word order or sentence structure.
- While averaging word embeddings may work well in some cases, it can fail to capture the meaning of sentences that rely heavily on word order, syntactic structure, or context.

### BERTScore:

- **BERTScore** compares **token-level embeddings** and computes similarity between each token in the candidate (e.g., a generated sentence) and the reference sentence.
- It doesn't just treat the whole sentence as a bag of words but takes into account the **contextual relationships** between words in a sentence. It directly computes similarity between corresponding tokens in both sentences based on their contextualized embeddings.
- This approach is **sensitive to word order** and **syntax**, making it more effective at capturing **semantic meaning** in context, which is often critical for tasks like text generation or summarization.

### 3. **Cosine Similarity vs. BERTScore's Precision, Recall, and F1**:

### Word Embeddings (e.g., Word2Vec, GloVe):

- The typical approach when comparing embeddings (whether word or sentence embeddings) is to use **cosine similarity**, which measures the angle between two vectors: \[ \text{cosine similarity} = \frac{A \cdot B}{\|A\| \|B\|} \] This measures how similar two vectors are in terms of direction, with values closer to 1 indicating more similarity.
- In the case of word embeddings, you would compute cosine similarity between each word vector in the candidate and reference. For sentence-level tasks, you might average the cosine similarity across all word pairs.

### BERTScore:

- **BERTScore**, on the other hand, still uses **cosine similarity**, but it computes it at the **token level** (each word/token's contextualized embedding) rather than at the word or sentence level.
    
- In addition to cosine similarity, **BERTScore** introduces a more nuanced evaluation by calculating **Precision**, **Recall**, and **F1 scores**:
    
    - **Precision**: How much of the generated sentence is semantically similar to the reference.
    - **Recall**: How much of the reference sentence is covered by the generated sentence.
    - **F1 Score**: The harmonic mean of Precision and Recall.
    
    These metrics help balance the importance of both the coverage (recall) and correctness (precision) of the generated sentence in relation to the reference.
    

### 4. **Handling of Multiple Token Matches**:

### Word Embeddings (e.g., Word2Vec, GloVe):

- In traditional word embeddings, the comparison is often done at the word level, and if there is a **partial match** (e.g., synonyms or related words), the model would not necessarily capture that well. Additionally, traditional embeddings can struggle with **out-of-vocabulary** words or rare words.

### BERTScore:

- **BERTScore** is much better at handling **contextual meaning**, so it can capture semantic relationships more effectively. For instance, BERTScore can recognize that "good" and "great" are semantically similar in a given context, even though their word embeddings may not be exactly the same.
- It also makes use of **subword tokenization** (like WordPiece) to break down words into smaller parts, which helps with words that are rare or out of vocabulary.

### 5. **Task-Specific Sensitivity**:

### Word Embeddings (e.g., Word2Vec, GloVe):

- Traditional embeddings might be fine for tasks like **semantic similarity** between words or basic clustering tasks, but they are less effective for tasks that involve understanding complex sentence structure, word order, and context.

### BERTScore:

- BERTScore is specifically **designed for text generation tasks**, such as **summarization**, **machine translation**, and **text generation**, where the output (candidate text) should closely resemble the reference in meaning.
- Since BERTScore captures **contextualized word embeddings**, it is much more robust for tasks involving **syntactic structure**, **word order**, and **long-range dependencies** in the text.

---

### Key Differences Between BERTScore and Traditional Word Embedding Similarity:

|Aspect|**Traditional Word Embeddings** (e.g., Word2Vec, GloVe)|**BERTScore**|
|---|---|---|
|**Embedding Type**|Static embeddings (same vector for a word in all contexts)|Contextual embeddings (word vectors change depending on context)|
|**Comparison Level**|Word-level comparison (may aggregate for sentences)|Token-level comparison (preserves word order and syntax)|
|**Contextual Awareness**|Limited, doesn’t account for word meaning in different contexts|Fully contextualized (captures meaning based on surrounding words)|
|**Evaluation Metrics**|Cosine similarity between word vectors|Precision, Recall, F1 score using cosine similarity for token pairs|
|**Task Sensitivity**|Suitable for basic semantic similarity tasks|Tailored for text generation tasks, sensitive to syntax and meaning|
|**Handling of Rare Words/OOV**|Can struggle with rare or out-of-vocabulary words|Can handle rare words using subword tokenization (e.g., WordPiece)|

---

### In Summary:

- **BERTScore** goes beyond traditional word embeddings by leveraging **contextualized word embeddings** from models like BERT. This allows it to capture the **nuances of meaning** in context, rather than relying on static, context-independent word vectors.
- Unlike traditional word embedding-based similarity, which works at the **word level**, BERTScore evaluates **semantic similarity at the token level** and incorporates **Precision**, **Recall**, and **F1** to offer a more balanced evaluation.
- **BERTScore** is thus more accurate and robust for tasks where word order, sentence structure, and nuanced context are important, such as in **text generation**, **summarization**, and **machine translation**.
