---
title: ROUGE and BLEU
draft: false
tags:
  - notes
---

### 1. **BLEU Score (Bilingual Evaluation Understudy)**

### **What is BLEU?**

- **BLEU** is a metric for evaluating the quality of text that has been machine-translated from one language to another.
- It measures how similar the machine-generated text is to one or more reference texts (usually human-written).

### **Why BLEU?**

- BLEU is often used in machine translation, text generation, and chatbot evaluation because it provides a way to compare the overlap of words and phrases between the generated text (bot response) and the reference text (ground truth).

### **How BLEU Works:**

- BLEU works by comparing **n-grams** (sequences of n words) between the generated text and the reference text.
- It calculates the **precision** of n-grams, i.e., how many n-grams in the generated text also appear in the reference text.
- BLEU typically uses **1-grams** (individual words), **2-grams** (pairs of words), and higher n-grams.
- As n-grams get longer, it becomes harder to match them exactly, so BLEU penalizes longer outputs that deviate from the reference (this is called **brevity penalty**).

### **BLEU Calculation in the Code:**

- In the code, BLEU is calculated using `sentence_bleu` from the **NLTK library**.
    
    `bleu_score = sentence_bleu([reference.split()], generated.split())`
    
    Here's a breakdown:
    
    - `reference.split()` splits the reference text into words.
    - `generated.split()` splits the generated text into words.
    - The `sentence_bleu` function then calculates the BLEU score by comparing the n-grams in the generated response with those in the reference response.
    
    **Output Scale**:
    
    - BLEU scores range from 0 to 1, where:
        - `1` means a perfect match between the generated text and the reference text.
        - `0` means no overlap at all.

### **Example BLEU Score Calculation**:

- **Generated text**: "the cat is on the mat"
    
- **Reference text**: "the cat is sitting on the mat"
    
    **1-gram precision**:
    
    - The words in both texts: `["the", "cat", "is", "on", "the", "mat"]` overlap.
    - The word "sitting" doesn't match, but most words match.
    
    **2-gram precision**:
    
    - Pairs like `["the cat", "cat is", "is on", "on the", "the mat"]` overlap, but the pair "is sitting" does not.
    
    BLEU scores are calculated for 1-grams, 2-grams, etc., and combined with brevity penalties for shorter responses.
    

---

### 2. **ROUGE Score (Recall-Oriented Understudy for Gisting Evaluation)**

### **What is ROUGE?**

- **ROUGE** is another popular metric for evaluating automated text generation, but it works a bit differently from BLEU. ROUGE stands for **Recall-Oriented** because it’s more focused on **how much of the reference text is captured by the generated text**, rather than precision.

### **Why ROUGE?**

- ROUGE is often used in tasks like summarization or chatbot evaluation because it measures **recall**—i.e., how much of the important information in the reference text is captured in the generated text.
- It also directly measures **n-gram overlaps** (like BLEU), but it emphasizes **recall** more than **precision**.

### **Different Types of ROUGE:**

- **ROUGE-1**: Measures overlap of **unigrams** (single words).
- **ROUGE-2**: Measures overlap of **bigrams** (two adjacent words).
- **ROUGE-L**: Measures overlap based on the **longest common subsequence (LCS)**. This measures the longest sequence of words that appear in both the generated and reference texts, which captures fluency better.

### **ROUGE Calculation in the Code:**

In the code, ROUGE scores are computed using the `rouge_scorer` from the **rouge-score** library. Here’s a detailed breakdown of how this is achieved:

1. **Initialization**:
    
    `rouge_scorer_instance = rouge_scorer.RougeScorer(['rouge1', 'rouge2', 'rougeL'], use_stemmer=True)`
    
    - This line creates an instance of the `RougeScorer` class, specifying which ROUGE metrics to compute: ROUGE-1, ROUGE-2, and ROUGE-L.
    - The `use_stemmer=True` argument indicates that stemming will be applied to the words before scoring. Stemming reduces words to their base or root form, which can help in matching words that have the same root but different inflections (e.g., "running" and "run").
2. **Scoring**:
    
    `rouge_scores = rouge_scorer_instance.score(reference, generated)`
    
    - This line computes the ROUGE scores using the `score` method, which takes two arguments: the reference text (the ground truth) and the generated text (the output from the model).
    - The `score` method returns a dictionary containing the ROUGE scores for the specified metrics (ROUGE-1, ROUGE-2, ROUGE-L), typically including precision, recall, and F1 scores for each metric.

### **Interpreting ROUGE Scores**:

- The output from the `rouge_scorer` will generally contain:
    - **Precision**: The proportion of n-grams in the generated text that are also in the reference text.
    - **Recall**: The proportion of n-grams in the reference text that are also in the generated text.
    - **F1 Score**: The harmonic mean of precision and recall, providing a balanced measure that accounts for both metrics.

For example, for each ROUGE metric, you might see output like this:

```python
{
    'rouge1': {'fmeasure': 0.45, 'recall': 0.5, 'precision': 0.4},
    'rouge2': {'fmeasure': 0.3, 'recall': 0.35, 'precision': 0.25},
    'rougeL': {'fmeasure': 0.4, 'recall': 0.45, 'precision': 0.35}
}
```

---

### The Code Explanation

1. **Plotting Scores**:
    
    ```python
    plt.plot(x, results_df['rougeL_f1'], label='ROUGE-L')
    plt.xlabel('Response Index')
    plt.ylabel('Score')
    plt.title('Scores Across All Responses')
    plt.legend()
    plt.tight_layout()
    plt.show()
    ```
    
    - This section of code is responsible for visualizing the performance of the responses based on the ROUGE-L score.
    - `plt.plot(x, results_df['rougeL_f1'], label='ROUGE-L')` plots ROUGE-L scores against the response index, where `x` represents the indices of the responses (presumably a sequence of integers representing each response).
    - The x-axis is labeled as 'Response Index', and the y-axis is labeled as 'Score', providing a clear indication of what is being plotted.
    - The title of the plot is set to 'Scores Across All Responses', and the legend helps distinguish different score lines if there are multiple plotted.
    - `plt.tight_layout()` adjusts the plot to ensure that everything fits without overlapping, and `plt.show()` displays the plot.
2. **Printing Summary Statistics**:
    
    ```python
    print("\\nAverage Scores:")
    print(f"BLEU Score: {avg_scores['bleu']:.4f}")
    print(f"ROUGE-1 F1: {avg_scores['rouge1_f1']:.4f}")
    print(f"ROUGE-2 F1: {avg_scores['rouge2_f1']:.4f}")
    print(f"ROUGE-L F1: {avg_scores['rougeL_f1']:.4f}")
    ```
    
    - This section prints out the average scores for different evaluation metrics: BLEU and ROUGE scores (ROUGE-1, ROUGE-2, and ROUGE-L).
    - The average scores are formatted to four decimal places for clarity, and the use of formatted strings (`f"..."`) makes the code clean and readable.
3. **Saving Detailed Results**:
    
    ```python
    output_path = '/content/drive/MyDrive/ColabNotebooks/score_test_results.csv'
    results_df.to_csv(output_path, index=False)
    print(f"\\nDetailed results saved to: {output_path}")
    ```
    
    - The results are saved to a CSV file for further analysis or record-keeping. The `to_csv` method from the pandas DataFrame (`results_df`) is used to store the detailed evaluation results.
    - The file path is specified, and `index=False` ensures that the DataFrame index is not saved in the CSV file, keeping the output clean.
    - A confirmation message is printed, indicating where the results have been saved.
4. **Running Evaluation in Google Colab**:
    
    ```python
    if __name__ == "__main__":
        file_path = '/content/drive/MyDrive/ColabNotebooks/score_test.csv'
        results = evaluate_responses(file_path)
    ```
    
    - This block checks if the script is being run as the main program (as opposed to being imported as a module). If it is, it sets the path to the input CSV file containing the responses to be evaluated and calls the `evaluate_responses` function to start the evaluation process.

---

### NLTK Library and Its Use in NLP

**NLTK (Natural Language Toolkit)** is a powerful Python library for working with human language data (text). Here are some reasons why NLTK is commonly used:

- **Comprehensive Toolkit**: NLTK provides a wide array of tools for text processing, including tokenization, stemming, lemmatization, tagging, parsing, and semantic reasoning.
- **Ease of Use**: It is user-friendly and well-documented, making it accessible for beginners in NLP.
- **Educational Resource**: NLTK is widely used in academic settings for teaching NLP concepts and methods.
- **Data Sets**: The library includes several corpora and lexical resources, such as WordNet, which can be used for various NLP tasks.
- **Community Support**: Being one of the oldest libraries in the field, it has a large community, which means ample resources, tutorials, and forums for help.

### Other Libraries for NLP

While NLTK is a great tool, there are several other libraries available for natural language processing:

1. **spaCy**:
    - **Efficiency**: Known for its speed and efficiency, spaCy is designed for production use, focusing on providing strong performance.
    - **Pre-trained Models**: Offers pre-trained models for various languages, making it easy to get started with tasks like named entity recognition (NER) and part-of-speech (POS) tagging.
2. **Transformers (by Hugging Face)**:
    - **State-of-the-Art Models**: This library provides access to numerous pre-trained transformer models (like BERT, GPT, RoBERTa, etc.) that are state-of-the-art for a variety of NLP tasks including text classification, summarization, translation, and question-answering.
    - **Easy Integration**: It has an easy-to-use API that allows for quick implementation of complex models, making it suitable for both beginners and advanced users.
    - **Community and Support**: Hugging Face has built a strong community around its tools, offering tutorials, model sharing, and collaborative features.
3. **Gensim**:
    - **Topic Modeling**: Gensim is particularly strong in unsupervised topic modeling and document similarity analysis, often used for tasks like LDA (Latent Dirichlet Allocation) and word embeddings.
    - **Streaming Data**: It is designed to handle large text corpora efficiently, allowing for the processing of data that doesn’t fit into memory.
    - **Word Embeddings**: Gensim provides functionality for training and using word embeddings, such as Word2Vec and FastText.
4. **TextBlob**:
    - **Simplicity**: TextBlob is built on top of NLTK and provides a simple API for common NLP tasks, making it very beginner-friendly.
    - **Sentiment Analysis**: It includes built-in functionality for sentiment analysis, translation, and part-of-speech tagging.
    - **Easy to Use**: Its intuitive interface allows users to perform complex NLP tasks with just a few lines of code.
5. **StanfordNLP**:
    - **Stanford CoreNLP**: This library provides tools developed by the Stanford NLP Group. It includes features for dependency parsing, named entity recognition, and sentiment analysis.
    - **Multilingual Support**: It supports multiple languages and offers pre-trained models for various NLP tasks.
    - **Robustness**: Known for its accuracy in linguistic tasks due to its extensive research background.
6. **Flair**:
    - **Contextualized Word Embeddings**: Flair allows users to use state-of-the-art contextual string embeddings, which can boost performance on many NLP tasks.
    - **Easy to Use**: It has a simple API that makes it easy to work with various NLP tasks including NER, text classification, and part-of-speech tagging.
    - **Multi-Task Learning**: Flair supports training models on multiple tasks, leveraging the same embeddings for efficiency.
7. **OpenNLP**:
    - **Apache Project**: OpenNLP is an Apache project that provides machine learning-based libraries for NLP tasks.
    - **Wide Range of Tools**: It includes tools for tokenization, sentence splitting, part-of-speech tagging, named entity recognition, and parsing.
8. **Tidytext**:
    - **Integration with Tidyverse**: This library is designed for text mining in R and works seamlessly with the Tidyverse ecosystem, making it a great choice for data scientists familiar with R.
    - **Text Data Manipulation**: It allows for easy manipulation and analysis of text data in a tidy format.

# **NLT Alternatives for BLEU and ROGUE**

Based on the provided search results, here are some alternative libraries that can be used instead of NLTK for measuring BLEU and ROUGE scores:

1. **evaluate**: A Python library developed by Hugging Face, which provides a simple and efficient way to compute various evaluation metrics, including BLEU and ROUGE scores. You can install it using `pip install evaluate`.
2. **sacreBLEU**: A Python library for computing BLEU scores, developed by Matthew Peters. It provides a more accurate and robust implementation of the BLEU algorithm compared to NLTK’s `sentence_bleu`. You can install it using `pip install sacrebleu`.
3. **rouge_score**: A Python library specifically designed for computing ROUGE scores, developed by the University of Maryland. It provides a comprehensive implementation of various ROUGE variants, including ROUGE-1, ROUGE-2, and ROUGE-L. You can install it using `pip install rouge-score`.
4. **pyrouge**: Another Python library for computing ROUGE scores, developed by the University of California, Berkeley. It provides a simple and efficient implementation of ROUGE-1 and ROUGE-L. You can install it using `pip install pyrouge`.

### Choosing the Right Library

The choice of an NLP library often depends on several factors:

- **Task Requirements**: Depending on whether you need to perform simple tasks like tokenization and sentiment analysis or complex tasks like building a conversational AI, different libraries may be more suitable.
- **Performance Needs**: Libraries like spaCy and Hugging Face Transformers are optimized for speed and efficiency, making them ideal for production environments.
- **Ease of Use**: For beginners, libraries like TextBlob and NLTK provide a gentler learning curve with straightforward APIs.
- **Community and Support**: A library with strong community support can make learning and troubleshooting easier.

### Conclusion

The field of NLP is enriched with a variety of libraries, each designed to tackle different aspects of language processing. The choice of which library to use can significantly impact both the development process and the performance of the resulting models. For comprehensive tasks or for those looking to engage with cutting-edge research, libraries like Hugging Face Transformers and spaCy are often recommended. For educational purposes or simpler projects, NLTK and TextBlob can provide an excellent starting point.

By understanding the strengths and applications of each library, practitioners can leverage the right tools for their specific NLP tasks, thereby enhancing their productivity and the quality of their outcomes.

---

### 1. **BLEU Score: 0.2278**

- **What it is**: BLEU (Bilingual Evaluation Understudy) is a metric for evaluating the quality of text that has been machine-translated from one language to another. In this context, it assesses how closely the generated response matches the reference response.
- **Scale**: BLEU scores range from 0 to 1, where 1 indicates a perfect match. A score of 0.2278 suggests a moderate level of overlap between the generated and reference responses, indicating that while there is some alignment, there is significant room for improvement.

### 2. **ROUGE-1 F1: 0.4134**

- **What it is**: ROUGE (Recall-Oriented Understudy for Gisting Evaluation) measures the overlap of n-grams (typically unigrams for ROUGE-1) between the generated and reference texts. The F1 score balances precision and recall, providing a single score that accounts for both.
- **Interpretation**: An F1 score of 0.4134 indicates a decent level of overlap in unigrams, meaning the generated responses share about 41% of the words (adjusted for precision and recall) with the reference responses.

### 3. **ROUGE-2 F1: 0.3013**

- **What it is**: ROUGE-2 measures the overlap of bigrams (two-word sequences) between the generated and reference texts. Similar to ROUGE-1, it provides an F1 score.
- **Interpretation**: A score of 0.3013 suggests a lower degree of overlap in bigrams, indicating that the generated responses are less aligned with the reference responses at this level of n-gram comparison.

### 4. **ROUGE-L F1: 0.3450**

- **What it is**: ROUGE-L measures the longest common subsequence (LCS) between the generated and reference texts. This metric captures the longest sequence of words that appear in both texts in the same order, regardless of gaps.
- **Interpretation**: An F1 score of 0.3450 indicates a moderate alignment in terms of the sequence of words, suggesting that there is some coherence and structure in the generated responses compared to the references.

### Overall Interpretation

The average scores indicate a mixed level of performance for the generated responses. The BLEU score shows some acceptable level of precision, while the ROUGE scores provide insights into the overlap and structural coherence of the responses. While there is some success in matching the reference texts, the scores indicate that there is considerable room for improvement, especially in ensuring that generated responses more closely mimic the reference in both content and structure.

---

### Current Metric Analysis

1. About the scores received:

The BLEU scores (1e-78 to 1e-155) are extremely low, as BLEU typically ranges from 0 to 1, where 1 is perfect BLEU scores during evaluation focuses more towards:

- adequacy
- fidelity
- fluency

The ROUGE scores are in more typical ranges, though on the lower end:

- ROUGE-1: 0.20-0.35 (measures unigram overlap)
- ROUGE-2: 0.04-0.09 (measures bigram overlap)
- ROUGE-L: 0.08-0.21 (measures longest common subsequence)

ROUGE scores during evaluation is inclined more toward:

- coherence
- conciseness
- grammaticality
- readability
- content

## Score Interpretation

### Current Performance

- The very low BLEU scores suggest the model's output has very few exact matches with reference text.
- The moderate ROUGE scores indicate:
    - Better performance at matching individual words (ROUGE-1)
    - Struggles with matching phrases (ROUGE-2)
    - Moderate success at capturing sequential content (ROUGE-L)

### What would Higher scores range indicate?

- Better alignment with human references
- More accurate content generation
- Better preservation of key information
- More fluent and coherent outputs

## Improvement Strategy

So how can we improve the scores to improve the output gained from the model?

### Phase 1: Data Improvements

- Ensure training data quality and relevance
- Increase training data size
- Clean and preprocess data thoroughly
- Ensure reference texts are well-aligned with inputs

### Phase 2: Model Enhancements

- Try more advanced architectures
- Experiment with different hyperparameters
- Implement better tokenization
- Use domain-specific pre-training

The F1 score is the harmonic mean of precision and recall:

1. **Precision**: The number of true positive results divided by the sum of true positives and false positives.
2. **Recall**: The number of true positive results divided by the sum of true positives and false negatives.

---

Understanding: Next 

context_precision context_recall faithfulness answer_relevancy