# Classifiying Clinical Notes into Medical Domains 

## Problem Statement
Machine Learning algorithms in Natural Language Processing (NLP) are widely used in the Health Care and Life Sciences domain to extract information from unstructured text data. One application of NLP in healthcare is automated document classification. Several methods such as term frequency-inverse document frequency (TF-IDF), LDA Topic Modeling, Keyword Extraction, Convolutional Neural Networks have been proposed to tackle text classification for clinical documents. I will be exploring 2 different approaches to classify medical notes into clincal domains. 

## Data

I will be using the medical transcriptions dataset from kaggle: https://www.kaggle.com/tboyle10/medicaltranscriptions 

Although the dataset contains samples from 40 medical domains, I will only be using samples from 5 medical specialties: Gastroenterology, Neurology, Orthopedic, Radiology and Urology. The final data set has 1239 samples. 

## Data Preparation/Cleaning

Clean the text of the transcription and medical_specialties column:

- Remove punctuation/special character
- Remove numbers
- Lowercase text
- Lemmatization of text (not done currently) 

## Model Training and Selection 

### 1. TF-IDF -> Classification Model 

4 Classification models were evaluated : Multinomial Naive Bayes, Support Vector Machine (SVM), Random Forest, Logistic Regression. 

For training the models, raw documents (transcriptions) were converted to a matrix of TF-IDF features.

Here are the classification accuracies:

- Naive Bayes: 0.47
- SVM: 0.697
- Random Forest: 0.54
- Logistic Regression: 0.725

We see that Naive bayes gives us an accuracy of less than 50%. This is probably because Naive bayes does not work well with features that are highly correlated. It classifies most of the notes as 'Orthopedic'. Same is true for random forest. 

**TO-DO: Hyper Parameter tuning**

### 2. (Keyword Extraction + Entity Linking) -> TF-IDF -> Classification Model 

In this iteration of model training, I used the following approach to create the TF-IDF features:

- Extract Entities (Keywords) from transcription text using ScispaCy
- Use EntityLinker provided by ScispaCy to map these medical entites (keywords) to the Unified Medical Language System knowledge base. 
- Each transcript is converted to a list of keywords. This list of keyword is then converted into a matrix of TF-IDF features.

Here are the classification accuracies: 

- SVM: 0.7016
- Random Forest: 0.50
- Logistic Regression: 0.7016

There are a lot of keywords that are common between domains. Maybe filtering these keywords to retain only the ones that describe the domain best would improve the accuracy. Balancing the dataset may also help. 
