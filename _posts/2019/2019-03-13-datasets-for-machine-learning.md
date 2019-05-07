---
layout: post
title: "Datasets for Machine Learning"
date: 2019-03-13 22:00:00 +0100
category: tutorial
tagline: ""
tags: [Machine Learning, Big Data]
abstract : "Many datasets for machine learning."
---
{% include JB/setup %}

* [Introduction](#introduction)
* [Dataset Finders](#dataset-finders)
* [Public Government Datasets](#public-government-datasets)
* [Finance and Economics Datasets](#finance-and-economics-datasets)
* [Image Datasets](#image-datasets)
* [Sentiment Analysis Datasets](#sentiment-analysis-datasets)
* [Natural Language Processing Datasets](#natural-language-processing-datasets)
* [Datasets for Self-Driving Cars](#datasets-for-self-driving-cars)
* [Free Sports Datasets](#free-sports-datasets)
    - [Soccer Datasets](#soccer-datasets)
    - [Basketball Datasets](#basketball-datasets)
    - [Racing Datasets](#racing-datasets)
    - [Miscellaneous Sports Datasets](#miscellaneous-sports-datasets)
* [References](#references)


## Introduction

Datasets are important and essential to machine learning.
Besides that extracting or scrapping data from domain or professional websites, there are already a lot of public open datasets on the Internet.


## Dataset Finders

[__Kaggle__](https://www.kaggle.com/){:target="_blank"} is an online community for data scientists and machine learners.
On Kaggle, users can publish datasets and explore these shared datasets for analysis.
The supported file types of its recommendation include CSV, JSON, SQLite, Archives BigQuery and other formats.
Besides its [datasets](https://www.kaggle.com/datasets){:target="_blank"}, Kaggle also provides [ML competitions](https://www.kaggle.com/competitions){:target="_blank"} that allows companies to post problems and develops to build algorithms, and [kernels](https://www.kaggle.com/kernels){:target="_blank"} that is a cloud computational environment that enables reproducible and collaborative analysis.

[__UC Irvine Machine Learning Repository__](http://mlr.cs.umass.edu/ml/){:target="_blank"} and its [Archive](https://archive.ics.uci.edu/ml/index.php){:target="_blank"}: it is a collection of databases, domain theories, and data generators that are used by the machine learning community for the empirical analysis of machine learning algorithms.
The repository maintains 22 + 468 datasets(updated by 2019 March).

[__Common Crawl__](http://commoncrawl.org/){:target="_blank"} is a non-profit organization that crawls the web and freely provides its archives and datasets to the public.
The corpus contains petabytes of data collected over 8 years of web crawling. The corpus contains raw web page data, metadata extracts and text extracts.
[Web Data Commons](http://webdatacommons.org/){:target="_blank"} extracts structured data from Common Crawl and provides the extracted data for public download.


## Public Government Datasets

[Data.gov](https://www.data.gov/){:target="_blank"} provides datasets from multiple US government departments such as federal governments(department of agriculture), city governments, state governments and so on.
The topics of datasets contains agriculture, climate, education, finance, science and others.
It is managed and hosted by the U.S. General Services Administration and it is developed publicly on [GitHub](https://github.com/GSA/datagov-deploy){:target="_blank"}.

The [National Center for Education Statistics (NCES) (美国国家教育统计中心)](https://nces.ed.gov/){:target="_blank"} is the primary federal entity for collecting and analyzing data related to education.

The [UK Data Service (英国数据服务)](https://www.ukdataservice.ac.uk/){:target="_blank"} is the UK's largest collection of social, economic and population data resources.

[Data USA](https://datausa.io/){:target="_blank"} is a comprehensive website and visualization engine of public US Government data.
It provides several [datasets](https://datausa.io/about/datasets/){:target="_blank"}.


## Finance and Economics Datasets

[Quandl](https://www.quandl.com/){:target="_blank"} provides premier source for financial, economic, and alternative datasets, serving investment professionals.

[World Bank (世界银行)](https://data.worldbank.org/){:target="_blank"} Open Data coordinates statistical and data work and maintains a number of macro, financial and sector databases. The economic data and models have gradually been made available to the public.

The [International Monetary Fund (IMF) (国际货币基金组织)](https://www.imf.org/en/Data){:target="_blank"} publishes a range of time series data on IMF lending, exchange rates and other economic and financial indicators. Manuals, guides, and other material on statistical practices at the IMF, in member countries, and of the statistical community at large are also available.

[Financial Times (金融时报市场)](https://markets.ft.com/data/){:target="_blank"} provides markets data from around the world, including stock price indexes, commodities and foreign exchange.

[American Economic Association (AEA) (美国经济协会)](https://www.aeaweb.org/resources/data){:target="_blank"} provides macroeconomic data from around the US, individual-level data on income, employment or health, and some other world data.


## Image Datasets

[LabelMe](http://labelme2.csail.mit.edu/Release3.0/index.php){:target="_blank"} provides a dataset of digital images with annotations.
Its tool is a WEB-based image annotation tool that allows researchers to label images and share the annotations with the world.
It also provides a set of tools for using the LabelMe dataset from Matlab.

[ImageNet](http://image-net.org/){:target="_blank"} is an image database organized according to the WordNet hierarchy (currently only the nouns), in which each node of the hierarchy is depicted by hundreds and thousands of images.

[Indoor Scene Recognition](http://web.mit.edu/torralba/www/indoor.html){:target="_blank"} provides a database that contains 67 Indoor categories, and a total of 15620 images. The number of images varies across categories, but there are at least 100 images per category. All images are in jpg format.
A subset of the images are segmented and annotated with the objects that they contain. The annotations are in LabelMe format.

[COCO](http://cocodataset.org/){:target="_blank"} is a large-scale object detection, segmentation, and captioning dataset.
It contains 330k images, over 200k of which are labeled, 1.5m object instances and 80 object categories.

[Visual Genome](http://visualgenome.org/){:target="_blank"} is a dataset, a knowledge base, an ongoing effort to connect structured image concepts to language.
It contains more than 100k images and 3.8m object instances.

[Labeled Faces in the Wild (LFW)](http://vis-www.cs.umass.edu/lfw/){:target="_blank"} provides a database of face photographs designed for studying the problem of unconstrained face recognition. The data set contains more than 13,000 images of faces collected from the web. Each face has been labeled with the name of the person pictured. 1680 of the people pictured have two or more distinct photos in the data set.


## Sentiment Analysis Datasets

[Multi-Domain Sentiment Dataset](http://www.cs.jhu.edu/~mdredze/datasets/sentiment/){:target="_blank"} from Johns Hopkins University contains product reviews taken from Amazon.com from many product types (domains).
Some domains (books and DVDs) have hundreds of thousands of reviews. Others (musical instruments) have only a few hundred. Reviews contain star ratings (1 to 5 stars) that can be converted into binary labels if needed.

[Large Movie Review Dataset](http://ai.stanford.edu/~amaas/data/sentiment/){:target="_blank"} from AI lab in Stanford University is a dataset for binary sentiment classification containing substantially more data than previous benchmark datasets.
It provides a set of 25,000 highly polar movie reviews for training, and 25,000 for testing. There is additional unlabeled data for use as well. Raw text and already processed bag of words formats are provided.

[Standford Sentiment Analysis](https://nlp.stanford.edu/sentiment/index.html){:target="_blank"} from Stanford NLP Group provides datasets for predicting the sentiment of movie reviews.

[Sentiment140 for Academics](http://help.sentiment140.com/home){:target="_blank"} provides a dataset for the sentiment of a brand, product, or topic on Twitter.
The data is a CSV with emoticons removed. Data file format has 6 fields.


## Natural Language Processing Datasets

[Enron Email Dataset](https://www.cs.cmu.edu/~./enron/){:target="_blank"} contains data from about 150 users, mostly senior management of Enron, organized into folders. The corpus contains a total of about 0.5M messages.

[Web data: Amazon reviews](https://snap.stanford.edu/data/web-Amazon.html){:target="_blank"} from SNAP group in Stanford University provides a dataset consists of reviews from amazon.
The data span a period of 18 years, including ~35 million reviews up to March 2013. Reviews include product and user information, ratings, and a plaintext review.

[Google Books Ngrams in AWS](https://aws.amazon.com/datasets/google-books-ngrams/){:target="_blank"} provides a dataset containing Google Books n-gram corpora.
The entire dataset hasn't been released yet, but those that were complete as of the time of writing are available.

[The Blog Authorship Corpus](http://u.cs.biu.ac.il/~koppel/BlogCorpus.htm){:target="_blank"} consists of the collected posts of 19,320 bloggers gathered from blogger.com in August 2004. The corpus incorporates a total of 681,288 posts and over 140 million words - or approximately 35 posts and 7250 words per person.
Each blog in the corpus includes at least 200 occurrences of common English words.

[Project Gutenberg](http://www.gutenberg.org/){:target="_blank"} provides an offline catalog of e-books available in the XML/RDF format.

[Aligned Hansards of the 36th Parliament of Canada](https://www.isi.edu/natural-language/download/hansard/){:target="_blank"} is provided by the Natural Language Group of the USC Information Sciences Institute.
The release contains 1.3 million pairs of aligned text chunks (sentences or smaller fragments) from the official records (Hansards) of the 36th Canadian Parliament.

[SMS Spam Collection](http://www.dt.fee.unicamp.br/~tiago/smsspamcollection/){:target="_blank"} is a public set of SMS labeled messages that have been collected for mobile phone spam research. It has one collection composed by 5,574 English, real and non-encoded messages, tagged according being legitimate (ham) or spam.

[Yelp Open Dataset](https://www.yelp.com/dataset){:target="_blank"} is a subset of Yelp's businesses, reviews, and user data for use in personal, educational, and academic purposes.
The dataset contains more than 6 million reviews, 192+k businesses and 1+ million tops by 1.6 million users.


## Datasets for Self-Driving Cars

[Berkeley DeepDrive](https://bdd-data.berkeley.edu/){:target="_blank"} provides 100,000 HD video sequences of over 1,100-hour driving experience across many different times in the day, weather conditions, and driving scenarios. The video sequences also include GPS locations, IMU data, and timestamps. 

[ApolloScape](http://apolloscape.auto/){:target="_blank"} provides datasets for scene parsing, car instance, lane segmentation, self localization, trajectory, detection/tracking and stereo.

The [comma.ai](https://comma.ai/){:target="_blank"} provides [driving dataset](https://archive.org/details/comma-dataset){:target="_blank"} containing more than 7 hours of highway driving. Details include car's speed, acceleration, steering angle, and GPS coordinates.

[Oxford's Robotic Car](https://robotcar-dataset.robots.ox.ac.uk/){:target="_blank"} provides datasets that contain over 100 repetitions of a consistent route through Oxford, UK, captured over a period of over a year. The dataset captures many different combinations of weather, traffic and pedestrians, along with longer term changes such as construction and roadworks.

[Cityscape Dataset](https://www.cityscapes-dataset.com/){:target="_blank"} is a large-scale dataset that contains a diverse set of stereo video sequences recorded in street scenes from 50 different cities, with high quality pixel-level annotations of 5000 frames in addition to a larger set of 20000 weakly annotated frames. The dataset is thus an order of magnitude larger than similar previous attempts.

[Traffic Sign Recognition](http://www.vision.ee.ethz.ch/~timofter/traffic_signs/){:target="_blank"} provides KUL Belgium traffic sign dataset that contains more than 10000+ traffic sign annotations from  thousands of physically distinct traffic signs in the Flanders region in Belgium.

[Laboratory for Intelligent & Safe Automobiles (LISA)](http://cvrr.ucsd.edu/LISA/datasets.html){:target="_blank"} from University of California San Diego provides datasets for vehicle detection, traffic sign, traffic light and trajectory.


## Free Sports Datasets

### Soccer Datasets

* [football.db](https://openfootball.github.io/){:target="_blank"} is a free and open public domain football database & schema for use in any (programming) language (e.g. uses plain datasets).
* [football.csv](https://footballcsv.github.io/){:target="_blank"} provides an open public domain football data in csv format.
* Some datasets from [Kaggle](https://www.kaggle.com/){:target="_blank"}:
    - [FIFA 19 complete player dataset](https://www.kaggle.com/karangadiya/fifa19){:target="_blank"} provides 18k+ FIFA 19 players and ~90 attributes extracted from a latest FIFA database, [SoFIFA](https://sofifa.com/){:target="_blank"}.
    - [Fifa 18 More Complete Player Dataset](https://www.kaggle.com/kevinmh/fifa-18-more-complete-player-dataset){:target="_blank"} provides FIFA 18 Players data extracted also from SoFIFA. It is an extension of [FIFA 18 Complete Player Dataset](https://www.kaggle.com/thec03u5/fifa-18-demo-player-dataset){:target="_blank"}.
    - [FIFA World Cup](https://www.kaggle.com/abecklas/fifa-world-cup){:target="_blank"} provides all the results from FIFA World Cup games. The data is courtesy of the FIFA World Cup Archive website.
    - [International football results from 1872 to 2018](https://www.kaggle.com/martj42/international-football-results-from-1872-to-2017){:target="_blank"} includes 39,669 results of international football matches starting from the very first official match in 1972 up to 2018. The data is gathered from several sources including but not limited to Wikipedia, fifa.com, rsssf.com and individual football associations' websites.

### Basketball Datasets

* [NBA player of the week](https://www.kaggle.com/jacobbaruch/nba-player-of-the-week){:target="_blank"} provides player of the week data from 1984-5 to 2018-9. The data is scraped from [basketball real gm](https://basketball.realgm.com/){:target="_blank"}.
* [NCAA Basketball ](https://www.kaggle.com/ncaa/ncaa-basketball){:target="_blank"} contains data about NCAA Basketball games, teams, and players. Game data covers play-by-play and box scores back to 2009, as well as final scores back to 1996.

### Racing Datasets

* [Ergast Formula One Dataset](http://ergast.com/mrd/db/){:target="_blank"}: the Ergast Developer API is an experimental web service and provides data for the Formula One series, from the beginning of the world championships in 1950.
* [formula1.db](https://github.com/opensport/formula1.db){:target="_blank"} is a free open public domain Formula 1/Formula One database 'n' schema for use in any (programming) language (e.g. uses plain text fixtures/data sets).

### Miscellaneous Sports Datasets

* [NFLsavant.com](http://nflsavant.com/about.php){:target="_blank"} is a web site dedicated to providing advanced NFL statistics in a simple to use interface.  All data and stats from this site are compiled from publicly-available NFL play-by-play data on the internet.
* [Lahman’s Baseball Database](http://www.seanlahman.com/baseball-archive/statistics/){:target="_blank"} contains complete batting and pitching statistics from 1871 to 2018, plus fielding statistics, standings, team stats, managerial records, post-season data, and more.


## References

1. [20 Free Sports Datasets for Machine Learning](https://gengo.ai/datasets/20-free-sports-datasets-for-machine-learning/){:target="_blank"}
2. [The 50 Best Free Datasets for Machine Learning](https://gengo.ai/datasets/the-50-best-free-datasets-for-machine-learning/){:target="_blank"}
3. [List of datasets for machine-learning research on Wikipedia](https://en.wikipedia.org/wiki/List_of_datasets_for_machine-learning_research){:target="_blank"}
4. [17 Free Financial & Economic Datasets for Machine Learning](https://gengo.ai/datasets/17-best-finance-economic-datasets-for-machine-learning/){:target="_blank"}
5. [The Best 25 Datasets for Natural Language Processing](https://gengo.ai/datasets/the-best-25-datasets-for-natural-language-processing/){:target="_blank"}
