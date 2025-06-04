---
title: mood_catcher
draft: false
tags:
  - complete
  - 30daysai
---
### A little on what's today's project is all about 
# Building a Mood Catcher from Journal Entries Using VADER and OpenAI

Analyzing how you feel based on your personal journal entries. In this guide, we'll create a simple Python program that:

1. Accepts daily journal entries in JSON format, for now we assume that the journal entries are stored after receiving from somewhere in the JSON format.
2. Analyzes the sentiment of each entry using VADER
3. Assigns a mood label (Positive, Neutral, Negative)
4. Uses OpenAI's GPT model to generate a natural-language explanation of your mood on a selected date

#### A little on the libraries explored  
## TextBlob
TextBlob is a Python library used for **[Natural Language Processing (NLP)](https://www.analyticsvidhya.com/blog/2017/01/ultimate-guide-to-understand-implement-natural-language-processing-codes-in-python/)**. It relies on NLTK (Natural Language Toolkit). When you give it a sentence, it gives back two things: polarity and subjectivity.

The polarity score ranges from -1 to 1. A score of -1 means the words are super negative, like “disgusting” or “awful.” A score of 1 means the words are super positive, like “excellent” or “best.”

Subjectivity score, on the other hand, goes from 0 to 1. If it’s close to 1, it means the sentence has a lot of personal opinion instead of just facts.


## VADER (Valence Aware Dictionary and Sentiment Reasoner)

VADER, like TextBlob, is a lexicon-based sentiment analyzer with predefined rules for words or lexicons. However, what sets VADER apart is its ability to not only classify words as positive, negative, or neutral but also evaluate the overall sentiment of a sentence.

The output from VADER is presented in a **[Python](https://www.analyticsvidhya.com/blog/2016/01/complete-tutorial-learn-data-science-python-scratch-2/)** dictionary format, consisting of four keys: ‘neg’ for negative, ‘neu’ for neutral, ‘pos’ for positive, and ‘compound’. The compound score is particularly noteworthy as it represents the overall sentiment of the sentence by normalizing the other three scores (negative, neutral, and positive) between -1 and +1.

## VADER is Better than TextBlob for Sentiment Analysis ?
Well, it depends upon the users and their requirements. While TextBlob struggled with negative sentences, **[VADER](https://www.analyticsvidhya.com/blog/2021/01/sentiment-analysis-vader-or-textblob/)** outperformed in detecting negative polarity. However, VADER isn’t universally superior; its strength lies in negative sentiment classification. Ultimately, the choice between the two depends on specific project needs, highlighting the importance of understanding algorithm capabilities for effective sentiment analysis.


#### A little on the code side
## The Journal Data

We use a list of dictionary entries, each containing a `date` and a `entry` field:


`journal_entry = [
`{`         
`"date": "2025-06-01",`         
`"entry": "Today was amazing! I finished my project early and went for a walk. The sunset was beautiful."`     
`},     ... ]`

---

## Sentiment Analysis with VADER

We use VADER to compute the **compound sentiment score** for each journal entry and label the mood:
Each entry contains a `compound_score` and a corresponding `mood` label.

---

## Fetching Mood by Date

To allow querying by date, we define a function that finds the corresponding entry

---

## Generating a Mood Summary Using OpenAI

We use OpenAI's `ChatCompletion` endpoint to summarize the user's mood in natural language, as this function returns a human-friendly reflection on how the user may have felt.

---
#### to err is to be human 
## Common Errors  and their fixes

### Error 1: Accessing list with string index

`text = journal_entry['entry']`

**Issue:** `journal_entry` is a list of dictionaries. You can't access it with a string index.

**Fix:** Use a loop to iterate:

`for entry in journal_entry:     text = entry['entry']`

---

### Error 2: Incorrect `if __name__` check
 %% how dumb i felt here ><
                    == %%
`if __name__ == "main":`

**Issue:** Python checks for `"__main__"` (with double underscores on both sides), not `"main"`

`if __name__ == "__main__":`

---

### Error 3: Misusing OpenAI API response

`return response['choices'][0]['message']['content']`
**Issue:** In OpenAI SDK v1.x, the `response` is an object, not a dictionary.

**Fix:**
`return response.choices[0].message.content`

later found out change in the API response structure of the openai.

---
**References:**
- [Sentiment Analysis with TextBlob and VADER – Analytics Vidhya](https://www.analyticsvidhya.com/blog/2021/10/sentiment-analysis-with-textblob-and-vader/)
- [Why TextBlob Might Not Be Enough – Medium](https://medium.com/data-science/my-absolute-go-to-for-sentiment-analysis-textblob-3ac3a11d524)

## Code Reference

- [GitHub – python_for_beginners (30 Days AI - Day 2)](https://github.com/Si-za1/python_for_beginners/blob/30daysai/30daysAI/day2.py)

