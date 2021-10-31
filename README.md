# Honours Thesis
The data for this project is confidential and has not been included in this repository. Only the output of the Jupyter notebook has been added. As well as the final thesis paper.

The intention of this study is to create a more accurate version of the current pipeline that aims to
bridge topic modelling with classification through the use of document analysis and labelling.
Through the comparison of a variety of topic modelling techniques, this study aims to identify
the most impactful technique for topic modelling for the given data set, and use that technique as
the input for a text classifier with the most adequate parameters to provide the highest degree of
accuracy, and ease of implementation.

Topic Modelling (through the implementation of Latent Dirichlet Allocation) was used on a dataset of interviewer notes to attempt to classify whether or not the interviewer, followed best practice and was deemed 'Bar Raising'.

## Methodology
* Drop columns (features) that are not necessary for training
* Run a word TF-IDF Vectorizer, as well as a character TF-IDF Vectorizer, and then utilise the hstack() function to combine the two arrays in order
* Built in capability for multi-feature classification, however used one feature to run XGBoost on the inital dataset with minimal pre-processing to return results
  * This allowed me to baseline the test (**AUC score of 0.79**)
* Remove stopwrods and convert to lowercase
* Transform the data into a format to be used as input into the LDA model. First convert the documents into a Bag of Words, then convert the list of feedback into lists of vectors with length equal to the vocabulary. Plot the most frequent words.

![image](https://user-images.githubusercontent.com/16728800/139604536-84f3b4d0-463a-452f-980c-9acffe31cebb.png)

* Ran a number of tests, both using TF-IDF and without, as well as varying the number of topics and words per topic hyperparameters for the tuning of the model. 
* Created an sklearn Pipeline with two stages, first the vectorization, second the LDA algorithm.
* Determined the confusion matrix and started tweaking further hyperparameters

![image](https://user-images.githubusercontent.com/16728800/139604658-2515a390-ddfd-4d0c-923f-158413db6378.png)

* The best score was actually without using LDA, however, there were a few reasons as to why. Predominantly the bias of the dataset, as, only restrospectively, I determined that the number of incorrect data samples, heavily outweight the correct data samples. Techniques such as SMOTE or GAN could have been used to remedy this.

## Topic Distribution for 30 topics using 30 Salient Terms
![image](https://user-images.githubusercontent.com/16728800/139604239-aa93f538-19d9-49ea-af05-bbf25fe1b60a.png)

## Topic Distribution for 10 topics using 30 Salient Terms
![image](https://user-images.githubusercontent.com/16728800/139604271-65cece09-aec5-41db-abff-d635d1328b65.png)

## Topic Distribution for 5 topics using 30 Salient Terms
![image](https://user-images.githubusercontent.com/16728800/139604283-8cbbcb7b-f1fa-465d-837b-a932c340a810.png)

Reference: https://github.com/cpsievert/LDAvis
