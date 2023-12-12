# Decoding Emotions: An In-Depth Exploration of Sentiment Detection through EEG Signal Analysis

## Table of Contents
1. [Introduction](#introduction)
2. [Notebooks](#notebooks)
    1. [Light Runs](#light-runs)
    2. [Heavy Runs](#heavy-runs)


## Introduction
In this repository, you'll find Jupyter notebooks related to our recent machine-learning article about emotion detection from EEG (Electroencephalogram) data. The notebooks cover two main types of runs, one which needs less computational resources (`Light Runs`) and one which needs a noticable amount of RAM to be executed (`Heavy Runs`). [SEED](https://bcmi.sjtu.edu.cn/home/seed/seed.html) dataset is used for all notebooks.

## Notebooks
Here is an detailed explanation about each notebook file:

### Light Runs
The file `Light Runs.ipynb` contains methods we experimented with that need normal (about 12GB of RAM) computational resources. Mainly runs on each feature separately. Below you'll find a description of each section in the file and how to run it.

#### Imports
Contains all of the libraries needed for runnig this notebook. You need to run this cell only once.

#### Utils
Contains some variables or functions that may be useful. This notebook was run on Google Colab, so it loads `drive`. If you're running this on another setup, just ignore this cell.

Remember to set `base_path` according to your environment. It must point out where the dataset exists.

#### Loading Data
Here it loads all of the data from all features into a variable named `data`. We use this variable in the entire notebook for selecting train and test data. You need to run this cell once. It also reads labels. You may need to change the path of `label.mat` according to your setup.

#### All Subjects, 5-Fold (Mixed Data), Each Feature
This cell is run for section 4.2 of the article, Answering the question: 

> Can emotional information be derived from features extracted from EEG data?

The plot of these results is presented in `Figure 2 (b)` of the article.

Just run it and it will show detailed output at runtime. After it finishes running, results will be saved it `final-allsubj-5fold-eachfeatures.csv` at the root of `base_path` previously defined in the `Imports` section.

#### All Subjects, 3 Subjects Aside, Each Feature
This cell is run for section 4.4 of the article, Answering the question: 

> How does the presence of overlapping subjects in both the training and testing data impact the classification of emotions?

The plot of these results is presented in `Figure 4 (b)` of the article.

Just run it and it will show detailed output at runtime. After it finishes running, results will be saved it `final-allsubj-5fold-3subjaside-eachfeatures.csv` at the root of `base_path` previously defined in the `Imports` section.

#### All Subjects, 3 Videos Aside, Each Feature
This cell is run for section 4.3 of the article, Answering the question: 

> How does the presence of overlapping videos in both the training and testing data impact the classification of emotions?

The plot of these results is presented in `Figure 3 (b)` of the article.

Just run it and it will show detailed output at runtime. After it finishes running, results will be saved it `final-allsubj-5fold-3vidaside-eachfeatures.csv` at the root of `base_path` previously defined in the `Imports` section.

#### All Subjects, 3 Subjects Aside, Each Feature, Each Frequency Band
This cell is run for section 4.7 of the article, Answering the question: 

> Which frequency bands carry the most informative content for classification purposes?

The plot of these results is presented in `Figure 7` of the article.

Just run it and it will show detailed output at runtime. After it finishes running, results will be saved it `final-allsubj-5fold-3subjaside-eachfeatures-5bands.csv` at the root of `base_path` previously defined in the `Imports` section.


### Heavy Runs
The file `Heavy Runs.ipynb` contains methods we experimented with that need high (minimum of 16GB of RAM) computational resources. Mainly runs on all features. Below you'll find a description of each section in the file and how to run it. Some of them may take hours to run.

#### Imports
Contains all of the libraries needed for runnig this notebook. You need to run this cell only once.

#### Utils
Contains some variables or functions that may be useful. This notebook was run on Google Colab, so it loads `drive`. If you're running this on another setup, just ignore this cell.

Remember to set `base_path` according to your environment. It must point out where the dataset exists.

#### Loading Data
Here it loads all of the data from all features into a variable named `data`. We use this variable in the entire notebook for selecting train and test data. You need to run this cell once. It also reads labels. You may need to change the path of `label.mat` according to your setup.

#### All Subjects, 5-Fold (Mixed Data), All Features
This cell is run for section 4.2 of the article, Answering the question: 

> Can emotional information be derived from features extracted from EEG data?

The plot of these results is presented in `Figure 2 (a)` of the article.

Just run it and it will show detailed output at runtime. After it finishes running, results will be saved it `final-allsubj-5fold-allfeatures.cs` at the root of `base_path` previously defined in the `Imports` section.

#### All Subjects, 3 Subjects Aside, All Features
This cell is run for section 4.4 of the article, Answering the question: 

> How does the presence of overlapping subjects in both the training and testing data impact the classification of emotions?

The plot of these results is presented in `Figure 4 (a)` of the article.

Just run it and it will show detailed output at runtime. After it finishes running, results will be saved it `final-allsubj-5fold-3subjaside-allfeatures.csv` at the root of `base_path` previously defined in the `Imports` section.

#### All Subjects, 3 Videos Aside, All Features
This cell is run for section 4.3 of the article, Answering the question: 

> How does the presence of overlapping videos in both the training and testing data impact the classification of emotions?

The plot of these results is presented in `Figure 3 (a)` of the article.

Just run it and it will show detailed output at runtime. After it finishes running, results will be saved it `final-allsubj-5fold-3vidaside-allfeatures.csv` at the root of `base_path` previously defined in the `Imports` section.

#### All Subjects, 3 Subjects Aside, Selected Features
This cell is run for section 4.6 of the article, Answering the question: 

> Which features carry the most informative content for classification purposes, and does classifying based on these features lead to an improvement in classification accuracy?

The plot of these results is presented in `Figure 6` of the article.

Just run it and it will show detailed output at runtime. After it finishes running, results will be saved it `final-allsubj-5fold-3subjaside-selectedfeatures.csv` at the root of `base_path` previously defined in the `Imports` section.
