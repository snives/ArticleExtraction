# Article Extraction using Neural Network


The purpose of this notebook is to investigate the efficacy of using a neural network to separating the article body of a web page from the boilerplate, advertising, and ancillary content.  

This is an important preprocessing step to increase the quality of subsequent text processing.  There are various methods of doing this with varying degrees of success.  The question we wish to answer is whether a neural network can perform this process with higher accuracy than current state of the art processes.

I first start with some feature engineering and creating a training dataset, with various columns which I hypothesize will have statistical power to separate text elements into article and non-article classes.  This was performed prior to this notebook and provided in `training.csv`.  I then inspect the dataset and decide to transform certain columns to make their distributions more normal using Box-Cox, followed by standardization or normalization, where applicable.

Categorical features such as `Tag` are one-hot encoded, and the `AncestorTag`, which is a Bitvector of the most informative 32 ancestor tags of the given tag, are simply encoded as 32 separate boolean features.

The dependent variable `Output` is biased, that is its classification is imbalanced and so I employ a Synthetic Minority Over-Sampling Technique to equalize the classes.

I use Keras with a Tensorflow backend to define a 3 layer neural network, using ReLu activation function and RMSProp optimizer, training for 50 epochs with batches of 100.  The neural network achieves a 98% accuracy at predicting the correct classification of each tag in a html document.

- Author: Snives
- Project: http://github.com/snives/ArticleExtraction
