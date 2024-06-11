# Sentiment-Analysis

## Summary

This project performs sentiment analysis in Python on recipe reviews using the Natural Language Toolkit (NLTK) VADER model and the Huggingface RoBERTa model, and compares the results to derive key insights.

## How To Run

**Input:**
- sentiment_analysis.ipynb
- sentiment_analysis_data_input.csv

**Output:**
- Pairwise plots and analysis at the bottom of sentiment_analysis.ipynb that compare the sentiment scores from the VADER model and the RoBERTa model

**Running The Code:**
1. Download all the files from the repository
2. Open sentiment_analysis.ipynb in Jupyter notebook and click run

## About The Project

**Problem Statement**

Businesses need to be able to interpret customer feedback to see both what customers like and dislike, and how customers perceive their brand. Understanding customer feedback is crucial for businesses to be able to shape their strategy to better fit what customers are looking for, helping them boost customer satisfaction and develop loyalty.

**Sentiment Analysis**

Sentiment analysis refers to the process of computationally and systematically determining the emotion behind a statement, and assessing the degree to which it is positive, negative, and netural.

**VADER Model**

VADER stands for **V**alence **A**ware **D**ictionary and S**e**ntiment **R**easoner. It works as follows:
- The model uses a predefined lexicon of words, where each word in the dictionary is assigned a valence score between -4 and 4.
- The model first splits the statement into tokens
- For each token, if the token is in the predefined lexicon, the model assigns it the corresponding valence score
- After this, the model adjusts the scores based on context cues, like punctuation and capitalization, which we call the adjusted valence score

The model calculates four different types of scores, where the first three are in the range [0, 1] and the compound score is in the range [-1, 1]:
- Positive score = sum of scores > 0 divided by the sum of the absolute value of all scores in the statement
- Negative score = sum of scores < 0 divided by the sum of the absolute value of all scores in the statement
- Neutral score = number of tokens with neutral scores divided by the sum of the absolute value of all scores in the statement
- Compound score = sum of the adjusted valence scores, then normalized to range in [-1, 1]

With the VADER model using a predefined lexicon, and with its ability to be sensitive to context cues and handle informal language, the model is both efficient and nuanced. However, since it uses a predefined lexicon, it a) may not adapt well to newer words or modern slang, since those words have to be manually added to the lexicon, and b) the words in the statement that aren't found in the lexicon won't be assigned a valence score, which can result in a more inaccurate overall sentiment score. Along with this, while the VADER model considers the sentiments of the individual words, it does not consider the relationships between the words, which results in the VADER model being a weaker natural language processing model than RoBERTa.

**RoBERTa Model**

RoBERTa stands for Robustly Optimized BERT Pretraining Approach, where BERT stands for Bidirectional Encoders Representations from Transformers. It works as follows:
- The model is pretrained on a large corpus of data, allowing it to learn complex language patterns
- The model first splits the statements into tokens, and adds in its own special tokens
- Each token is converted into an embedding that captures its semantic meaning
- Each embedded token is passed through a transformer, where the model evaluates the relationship between the current token and other tokens in the statement
- The finalized embedding is mapped to sentiment categories like positive, negative, and neutral

This model calculates scores in terms of probabilities. 
- For each of the finalized embeddings, the raw scores for the positive, negative, and neutral sentiments are converted into probabilities
- The final score is in the form [x, y, z] for [negative, neutral, positive] where x, y, and z are the probabilities in [0, 1]. This represents that the RoBERTa model is (x * 100%) confident that the sentiment of the statement is negative, (y * 100%) confident that the sentiment of the statement is neutral, and (z * 100%) confident that the sentiment of the statement is positive.

With the RoBERTa model being trained on such large, diverse datasets, and with the training of these datasets being more rigorous, RoBERTa is able to have a rich, developed understanding of language. Since it considers the context of the text and understands the relationships between the tokens, it is able to provide a highly accurate insight into the sentiment of a statement. However, RoBERTa is more complex than VADER to implement, and requires more resources to train and run than VADER, which can increase time and costs.
