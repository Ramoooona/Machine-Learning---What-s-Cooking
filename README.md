# Machine-Learning---What-s-Cooking
Use recipe ingredients to categorize the cuisine
Source: https://www.kaggle.com/c/whats-cooking

## Introduction
Exposing to the local food is one of the most efficient and interesting way to transcend cultural boundaries and connect with local people and culture when travelling around. Some distinct ingredients of food gradually become synonymous with the country where they are most used. For example, tasting or even making different kinds of kimchi is top the list of things to do in Korea. Fish and chips with butter are prevailing on the menu of British restaurants. The combined smell of scallions, gingers, and garlic also makes Chinese food distinct. Based on the distinctive combination of ingredients in the cuisine in different places, we can to some extent predict the category of a dish’s cuisine referring to its list of ingredients. 

## Problem
Use recipe ingredients to categorize the cuisine

## Solution 1: Decision Tree
- Benchmark: all recipes in the TEST set are Italian food, since Italian food is the most popular type among all recipes in the TRAIN set
- Cleansing
  - convert characters to lower-case
  - allow the existence of dash, regular character, and space
- Create data frame for decision tree by constructing a simple document-term matrix for frequently occurring ingredients
- Remove sparse terms with frequency of occurrence is lower than 0.5%
- Split the newly created data as train and test sets to build model
- Accuracy 40.19%: the categories of cuisines are limited to Italian, Mexican, Chinese, Indian, and Southern US, which definitely not include all different kinds of cuisines existing in the TEST set

## Solution 2: Xgboost
- Advanced classification model with both linear programming solver and tree learning algorithms
- Set “dtm_train” as a matrix input of the model
  - Maximum depth of the tree = 25
  - Size of each boosting step = 0.3
  - Maximum number of iterations  = 200
  - Objective: softmax
  - Upper limit of the number of classes = 20
- Accuracy: 78.96%

## Solution 3: Logistic Regression
- The higher flexibility Linear SVC + lemmatization
- Return a proper word as lemma through vocabulary analysis to eliminate verbose inflectional endings, referring to WordNet
- Create corpus through “TfidVectorizer”
- Convert the corpus (train set) to a matrix of TF-IDF features
  - Set the stop_words as “English” to return the appropriate stop list when coming across a string and “English” is the only supported string value
  - Lower and upper limits of the range of n-values are both set as 1 to indicate that there can only be one value for different grams to be extracted
  - Proportion of documents = 0.57
  - No changes for non-zero data, and no sublinear programming
- Accuracy: 78.86%
