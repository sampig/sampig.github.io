---
layout: post
title: "A List of Java Machine Learning Tools or Libraries"
date: 2019-05-06 19:35:00 +0200
category: tutorial
tagline: ""
tags: [Java, Machine Learning]
abstract : "Learning Note: a list of Java machine learning tools or libraries."
---
{% include JB/setup %}

* [Introduction](#introduction)
* [Weka](#weka)
    - [WekaDeeplearning4j](#wekadeeplearning4j)
* [Deeplearning4j](#deeplearning4j)
* [Spark MLib](#spark-mlib)
* [References](#references)


## Introduction

Some tools or libraries for machine learning written in Java:

1. [Weka](https://www.cs.waikato.ac.nz/ml/weka/){:target="_blank"} is a collection of machine learning algorithms for data mining tasks. It contains tools for data preparation, classification, regression, clustering, association rules mining, and visualization. The algorithms can either be applied directly to a dataset or called from your own Java code. Weka provides 2 types of user interfaces: Java Swing and Command Line.
2. [Massive Online Analysis (MOA)](https://moa.cms.waikato.ac.nz/){:target="_blank"} is a popular open source framework for data stream mining, with a very active growing community (blog). It includes a collection of machine learning algorithms (classification, regression, clustering, outlier detection, concept drift detection and recommender systems) and tools for evaluation. Related to the WEKA project, MOA is also written in Java, while scaling to more demanding problems. MOA performs BIG DATA stream mining in real time, and large scale machine learning. MOA can be extended with new mining algorithms, and new stream generators or evaluation measures.
The goal of MOA is a benchmark framework for running experiments in the data stream mining context by proving: storable settings for data streams (real and synthetic) for repeatable experiments; a set of existing algorithms and measures form the literature for comparison; and an easily extendable framework for new streams, algorithms and evaluation methods.
3. [Deeplearning4j](https://deeplearning4j.org/){:target="_blank"} is an open-source, distributed, deep learning library for the JVM. It is written in Java and is compatible with any JVM language, such as Scala, Clojure or Kotlin. Deeplearning4j takes advantage of the latest distributed computing frameworks including Apache Spark and Hadoop to accelerate training. On multi-GPUs, it is equal to Caffe in performance.
Its Eclipse Deeplearning4j is the first commercial-grade, open-source, distributed deep-learning library written for Java and Scala. Integrated with Hadoop and Apache Spark, DL4J brings AI to business environments for use on distributed GPUs and CPUs. 
4. [MALLET](http://mallet.cs.umass.edu/){:target="_blank"} is a Java-based package for statistical natural language processing, document classification, clustering, topic modeling, information extraction, and other machine learning applications to text.
MALLET includes sophisticated tools for document classification: efficient routines for converting text to "features", a wide variety of algorithms (including Naïve Bayes, Maximum Entropy, and Decision Trees), and code for evaluating classifier performance using several commonly used metrics.
MALLET also includes tools for sequence tagging for applications such as named-entity extraction from text. Algorithms include Hidden Markov Models, Maximum Entropy Markov Models, and Conditional Random Fields.
The MALLET topic modeling toolkit contains efficient, sampling-based implementations of Latent Dirichlet Allocation, Pachinko Allocation, and Hierarchical LDA.
5. [Environment for Developing KDD-Applications Supported by Index-Structures (ELKI)](https://elki-project.github.io/){:target="_blank"} is an open source (AGPLv3) data mining software written in Java. The focus of ELKI is research in algorithms, with an emphasis on unsupervised methods in cluster analysis and outlier detection. In order to achieve high performance and scalability, ELKI offers data index structures such as the R*-tree that can provide major performance gains. ELKI is designed to be easy to extend for researchers and students in this domain, and welcomes contributions of additional methods. ELKI aims at providing a large collection of highly parameterizable algorithms, in order to allow easy and fair evaluation and benchmarking of algorithms.
6. [Apache SAMOA (Scalable Advanced Massive Online Analysis)](http://samoa.incubator.apache.org/){:target="_blank"} is a distributed streaming machine learning (ML) framework that contains a programing abstraction for distributed streaming ML algorithms.
Apache SAMOA enables development of new ML algorithms without directly dealing with the complexity of underlying distributed stream processing engines (DSPEe, such as Apache Storm, Apache Flink, and Apache Samza). Apache SAMOA users can develop distributed streaming ML algorithms once and execute them on multiple DSPEs.
7. [MLlib (Spark)](http://spark.apache.org/mllib/){:target="_blank"} is Apache Spark's scalable machine learning library. It fits into Spark's APIs and interoperates with NumPy in Python (as of Spark 0.9) and R libraries (as of Spark 1.5). Any Hadoop data source (e.g. HDFS, HBase, or local files) can by used to make it easy to plug into Hadoop workflows.

More tools or libraries will be updated in my GitHub [ZhuzhuLearning/MachineLearning/JavaLibraries.md](https://github.com/sampig/ZhuzhuLearning/blob/master/MachineLearning/JavaLibraries.md){:target="_blank"}.


## Weka

[Weka](https://www.cs.waikato.ac.nz/ml/weka/){:target="_blank"} (Waikato Environment for Knowledge Analysis) is a collection of machine learning algorithms for data mining tasks. It contains tools for data preparation, classification, regression, clustering, association rules mining, and visualization.

Using Weka in command line:
```
java -Xmx1024m weka.classifiers.trees.J48 -t data.arff -i -k -d J48-data.model
```

The GUI provides several applications:
- Explorer is an environment for exploring data with WEKA (the rest of this documentation deals with this application in more detail). Explorer is used for data preprocess, classifying, clustering, associating, attributes selecting or data visualization.
- Experimenter is an environment for performing experiments and conducts statistical tests between learning schemes.
- KnowledgeFlow. This environment supports essentially the same functions as the Explorer but with a drag-and-drop interface. One advantage is that it supports incremental learning.
- Workbench is an all-in-one application that combines all the others within user-selectable "perspectives".
- SimpleCLI provides a simple command-line interface that allows direct execution of WEKA commands for operating systems that do not provide their own command line interface.

Besides using Weka in command line or in Java Swing UI, you can also extend Weka by creating your own Filter or Classifier.

### WekaDeeplearning4j

Weka also supports Deep Learning by using [WekaDeeplearning4j](https://deeplearning.cms.waikato.ac.nz/){:target="_blank"}.
WekaDeeplearning4j is a deep learning package for the Weka workbench. It is developed to incorporate the modern techniques of deep learning into Weka. The backend is provided by the Deeplearning4j Java library. 

The following Neural Network Layers are available to build sophisticated architectures:
- ConvolutionLayer: applying convolution, useful for images and text embeddings.
- DenseLayer: all units are connected to all units of its parent layer.
- SubsamplingLayer: subsample from groups of units of the parent layer by different strategies (average, maximum, etc.).
- BatchNormalization: applies the common batch normalization strategy on the activations of the parent layer.
- LSTM: uses long short term memory approach.
- GlobalPoolingLayer: apply pooling over time for RNNs and pooling for CNNs applied on sequences.
- OutputLayer: generates classification / regression outputs.


## Deeplearning4j

[Deeplearning4j](https://deeplearning4j.org/){:target="_blank"} is an open-source, distributed, deep learning library for the JVM.

Deeplearning4j is written in Java and is compatible with any JVM language, such as Scala, Clojure or Kotlin. It takes advantage of the latest distributed computing frameworks including Apache Spark and Hadoop to accelerate training. On multi-GPUs, it is equal to Caffe in performance.

Deeplearning4j provides a lot of examples on its GitHub - [Deeplearning4J Examples](https://github.com/deeplearning4j/dl4j-examples){:target="_blank"}. It is better to take a look at those examples for beginning.
Repository of Deeplearning4J neural net examples include:
- MLP Neural Nets
- Convolutional Neural Nets
- Recurrent Neural Nets
- TSNE
- Word2Vec & GloVe
- Anomaly Detection
- User interface examples.

Arbiter is part of the DL4J Suite of Machine Learning/Deep Learning tools for the enterprise. It is dedicated to the hyperparameter optimization of neural networks created or imported into dl4j. It allows users to set up search spaces for the hyperparameters and run either grid search or random search to select the best configuration based on a given scoring metric.
Arbiter can be used to find good performing models, potentially saving you time tuning your model's hyperparameters, at the expense of greater computational time. Note however that Arbiter doesn't completely automate the neural network tuning process, the user still needs to specify a search space. This search space defines the range of valid values for each hyperparameter (example: minimum and maximum allowable learning rate). If this search space is chosen poorly, Arbiter may not be able to find any good models.

DataVec solves one of the most important obstacles to effective machine or deep learning: getting data into a format that neural nets can understand.

Deeplearning4j's NLP relies on ClearTK, an open-source machine learning and natural language processing framework for the Apache Unstructured Information Management Architecture, or UIMA. UIMA enables us to perform language identification, language-specific segmentation, sentence boundary detection and entity detection (proper nouns: persons, corporations, places and things).

Deeplearning4j supports neural network training on a cluster of CPU or GPU machines using Apache Spark. Deeplearning4j also supports distributed evaluation as well as distributed inference using Spark.
DL4J has two implementations of distributed training:
- Gradient sharing, available as of 1.0.0-beta: Based on this paper by Nikko Strom, is an asynchronous SGD implementation with quantized and compressed updates implemented in Spark+Aeron
- Parameter averaging: A synchronous SGD implementation with a single parameter server implemented entirely in Spark.


## Spark MLib

[MLlib (Spark)](http://spark.apache.org/mllib/){:target="_blank"} is Apache Spark's scalable machine learning library.
MLlib fits into Spark's APIs and interoperates with NumPy in Python (as of Spark 0.9) and R libraries (as of Spark 1.5). You can use any Hadoop data source (e.g. HDFS, HBase, or local files), making it easy to plug into Hadoop workflows. 

MLlib contains high-quality algorithms that leverage iteration, and can yield better results than the one-pass approximations sometimes used on MapReduce.
Spark runs on Hadoop, Apache Mesos, Kubernetes, standalone, or in the cloud, against diverse data sources.

MLlib contains many algorithms and utilities.

ML algorithms include:
- Classification: logistic regression, naive Bayes;
- Regression: generalized linear regression, survival regression;
- Decision trees, random forests, and gradient-boosted trees;
- Recommendation: alternating least squares (ALS);
- Clustering: K-means, Gaussian mixtures (GMMs);
- Topic modeling: latent Dirichlet allocation (LDA);
- Frequent itemsets, association rules, and sequential pattern mining.

ML workflow utilities include:
- Feature transformations: standardization, normalization, hashing;
- ML Pipeline construction;
- Model evaluation and hyper-parameter tuning;
- ML persistence: saving and loading models and Pipelines.

Other utilities include:
- Distributed linear algebra: SVD, PCA;
- Statistics: summary statistics, hypothesis testing.


## References

1. [A List of Java Machine Learning Tools or Libraries](https://github.com/sampig/ZhuzhuLearning/blob/master/MachineLearning/JavaLibraries.md){:target="_blank"}
2. [Weka](https://www.cs.waikato.ac.nz/ml/weka/){:target="_blank"}
3. [Deeplearning4j](https://deeplearning4j.org/){:target="_blank"}
4. [MLlib (Spark)](http://spark.apache.org/mllib/){:target="_blank"}
