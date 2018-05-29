# Spooky Author Identification

This project uses the Kaggle competition information from the competition
https://www.kaggle.com/c/spooky-author-identification
to build a classifier.

The data are available in the data subdirectory (5 MB)

Ideas for features to start with:
* [x] Looking at word frequencies per author
* [ ] Look at TD-IDF weighted word frequencies per author
* [ ] Look at "parts of speech" classifier (e.g. does one author use more adjectives, etc)? Good resource for POS classification is [nltk](https://www.nltk.org/)
* [ ] Length of sentences?

We can also make multiple models, and then aggregating their predictions.

## Models attempted:

### Naive Bayes in `spooky_eda.ipynb`

In addition to looking at the author frequencies, a "hand-rolled" Naive Bayes model was made that determined the probability of a word getting used for each author. Even though the set of articles is unbalanced (40% EAP, 30% MWS, and 30% HPL) , we still used a flat prior. Performed simple tokenization, but no stemming or lemmatization.

Results:

| Model | Training set | Test set |
|---|---|---|
| NB on word frequency | 94% | 81% |

Further action:
* Try lemmatizing or stemming models
* Use parts of speech model instead of word model
* Look at bigrams

### SVMs in `spooky_lsa.ipynb`

Attempted to make a topic model with 10 topics, and then used k-means to cluster the results. Silhouette scores for the different number of clusters are very flat, hovering around 0.15 -- 0.17 as the number of clusters varies from 3 to 19. A plot of points in the 10-dimensional topic space doesn't show any discernable structure. Using a SVC in the topic space yields an accuracy of 52%.

Applying a SVC on the word matrix directly is a lot more accurate. Both SVCs use the radial basis function kernel.

| Model | Training set | Test set |
|---|---|---|
| SVC w/ RBF kernel in topic space | 51.0%  | -- |
| SVC w/ RBF kernel on word matrix | 78.6% | 80.7% |
 
