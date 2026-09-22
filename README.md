# Cyberbullying Detection Using Machine Learning

This project investigates cyberbullying detection using textual and contextual features from online conversations.

## Project Overview

Three machine learning classifiers are evaluated:

* Logistic Regression
* Linear Support Vector Machine (SVM)
* Random Forest

Each classifier is tested using three feature configurations: text-only, context-only, and combined text and context.

## Methodology

Conversation messages are extracted from JSON-formatted data. Text is represented using TF-IDF with unigrams and bigrams. Contextual features include conversation-level information and participant attributes.

The models are evaluated on separate training, validation, and test sets, with particular attention to precision, recall, and F1-score for the cyberbullying class.

## Notebook

The experiment is available in [`cyberbullyingmodel.ipynb`](cyberbullyingmodel.ipynb).

## Results

The highest recorded cyberbullying F1-score is **0.696**, achieved by the context-only Random Forest model.

Combining textual and contextual features improves the Linear SVM F1-score from **0.444 to 0.662**, although combining features does not improve every classifier.

## Data and Privacy

The dataset is not included in this repository. The notebook should be reviewed for sensitive data, participant identifiers, credentials, and saved outputs before the repository is made public.

## Research Status

This repository contains the experimental code supporting an ongoing research paper on machine learning-based cyberbullying detection.
