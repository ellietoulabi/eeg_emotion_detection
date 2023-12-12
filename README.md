# Decoding Emotions: An In-Depth Exploration of Sentiment Detection through EEG Signal Analysis

## Table of Contents
1. [Introduction](#introduction)
2. [Requirements](#requirements)
3. [Notebooks](#notebooks)
    1. [EDA](#eda)
    2. [Load Data](#load-data)
    3. [Light Runs](#light-runs)
    4. [Heavy Runs](#heavy-runs)
    5. [Raw Classify](#raw-classify)


## Introduction
In this repository, you'll find Jupyter notebooks related to our recent machine-learning article about emotion detection from EEG (Electroencephalogram) data. The notebooks cover two main types of runs, one which needs less computational resources (`Light Runs`) and one which needs a noticable amount of RAM to be executed (`Heavy Runs`). [SEED](https://bcmi.sjtu.edu.cn/home/seed/seed.html) dataset is used for all notebooks.

## Requirements
- Any environment that runs jupyter notebooks.
- Python >=3.8
- No sepecific version of libraries needed.

## Notebooks
Here is an detailed explanation about each notebook file:

### EDA
This file represents the Exploratory Data Analysis (EDA) of the dataset.

#### Installing and Importing Packages
This section installs the required package MNE and imports other packages. It also loads Google Drive. If you're running this on another platform, you can bypass the cell containing google drive loading code.

#### Defining Variables and Functions
This section defines 3 types of channel names (as they will be used during the rest of the notebook). It also defines some constants like `base_path` that you must set according to the setup you have. There are some helper functions and some functions for reading and plotting different kinds of charts and topo maps, each described in the notebook.

#### Drawing Signal Image
In this section, we plotted the power of each channel in the time and the signal shape for the first trial of the first experiment of the first subject which by the way is a happy video. It shows that some channels have power way too much bigger than other channels and they are candidate to be removed. So in the next sub-section, we removed very high energy channels and repeated the same plots which led to better outcomes in terms of interpretability.

#### Loading EEG Data Into MNE
In this section, we used the popular MNE library to explore data analysis on data with more meaningful diagrams.

We started with a single trial (all properties same as before) and after loading raw data, plotted raw signal, `psd` and `psd average`. Then we applied a notch filter on 50Hz and plotted the same diagrams again. The effect of the notch filter was clear in the `psd` and `psd average` plots.

In the next sub-section, we plotted the energy of each channel for each of the frequency bands (Delta, Theta, Alpha, Beta, and Gamma). The effect of very high energy channels caused a problem here too because it prevented other channels from being shown properly. Then we plotted the topo map (image and gif) and also the joint topo map.

In the EDA of EEG data, one of the important plots is plotting ICA components. These components show us the effect of noise on data (like blinking). We plotted 20 components to analyze them later. 

After epoching data into 1s epochs each with an event of type happy, we plotted the average plot but still, high energy channels blocked the potential of data in other channels. This problem occurred even when we were plotting two concatenated happy and neutral trials.

We repeated the process and plotted everything the same and as we expected, now everything started to make sense.

#### Replicating Fig 6
In this section, we plotted stacked Differential Entropy (DE) of all channels in all frequency bands but better results were shown when we removed very high energy channels.

#### New ICA Plot with Channels Dropped
In this section, we analyzed ICA components and then analyzed them using `plot_overlay` and excluded some components.

### Load Data
**Notice: This file must be run before any of `Light Runs` or `Heavy Runs`**

This file loads all data from `Extracted_Features` and store them in a file name `alldata.pkl`.

#### Imports
Contains all of the libraries needed for runnig this notebook. You need to run this cell only once.

#### Utils
Contains some variables or functions that may be useful.

Remember to set `base_path` according to your environment. It must point out where the dataset exists. Remember that `Extracted_Features` folder must be inside the `base_path`

#### Saving All Features Data to Pickle File
This part reads and saves all features data into the `alldata.pkl` file. Remember to change paths in other files if you change this file name.

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

Just run it and it will show detailed output at runtime. After it finishes running, results will be saved in `final-allsubj-5fold-eachfeatures.csv` at the root of `base_path` previously defined in the `Utils` section.

#### All Subjects, 3 Subjects Aside, Each Feature
This cell is run for section 4.4 of the article, Answering the question: 

> How does the presence of overlapping subjects in both the training and testing data impact the classification of emotions?

The plot of these results is presented in `Figure 4 (b)` of the article.

Just run it and it will show detailed output at runtime. After it finishes running, results will be saved in `final-allsubj-5fold-3subjaside-eachfeatures.csv` at the root of `base_path` previously defined in the `Utils` section.

#### All Subjects, 3 Videos Aside, Each Feature
This cell is run for section 4.3 of the article, Answering the question: 

> How does the presence of overlapping videos in both the training and testing data impact the classification of emotions?

The plot of these results is presented in `Figure 3 (b)` of the article.

Just run it and it will show detailed output at runtime. After it finishes running, results will be saved in `final-allsubj-5fold-3vidaside-eachfeatures.csv` at the root of `base_path` previously defined in the `Utils` section.

#### All Subjects, 3 Subjects Aside, Each Feature, Each Frequency Band
This cell is run for section 4.7 of the article, Answering the question: 

> Which frequency bands carry the most informative content for classification purposes?

The plot of these results is presented in `Figure 7` of the article.

Just run it and it will show detailed output at runtime. After it finishes running, results will be saved in `final-allsubj-5fold-3subjaside-eachfeatures-5bands.csv` at the root of `base_path` previously defined in the `Utils` section.


### Heavy Runs
The file `Heavy Runs.ipynb` contains methods we experimented with that need high (minimum of 16GB of RAM) computational resources. Mainly runs on all features. Below you'll find a description of each section in the file and how to run it. Some of them may take hours to run.

**Notice: You must load data each time before running each scenario in this file**

#### Imports
Contains all of the libraries needed for runnig this notebook. You need to run this cell only once.

#### Utils
Contains some variables or functions that may be useful.

Remember to set `base_path` according to your environment. It must point out where the dataset exists.

#### Loading Data
Here it loads all of the data from all features into a variable named `data`. We use this variable in the entire notebook for selecting train and test data. You need to run this cell once. It also reads labels. You may need to change the path of `label.mat` according to your setup.

#### All Subjects, 5-Fold (Mixed Data), All Features
This cell is run for section 4.2 of the article, Answering the question: 

> Can emotional information be derived from features extracted from EEG data?

The plot of these results is presented in `Figure 2 (a)` of the article.

Just run it and it will show detailed output at runtime. After it finishes running, results will be saved in `final-allsubj-5fold-allfeatures.cs` at the root of `base_path` previously defined in the `Utils` section.

#### All Subjects, 3 Subjects Aside, All Features
This cell is run for section 4.4 of the article, Answering the question: 

> How does the presence of overlapping subjects in both the training and testing data impact the classification of emotions?

The plot of these results is presented in `Figure 4 (a)` of the article.

Just run it and it will show detailed output at runtime. After it finishes running, results will be saved in `final-allsubj-5fold-3subjaside-allfeatures.csv` at the root of `base_path` previously defined in the `Utils` section.

#### All Subjects, 3 Videos Aside, All Features
This cell is run for section 4.3 of the article, Answering the question: 

> How does the presence of overlapping videos in both the training and testing data impact the classification of emotions?

The plot of these results is presented in `Figure 3 (a)` of the article.

Just run it and it will show detailed output at runtime. After it finishes running, results will be saved in `final-allsubj-5fold-3vidaside-allfeatures.csv` at the root of `base_path` previously defined in the `Utils` section.

#### All Subjects, 3 Subjects Aside, Selected Features
This cell is run for section 4.6 of the article, Answering the question: 

> Which features carry the most informative content for classification purposes, and does classifying based on these features lead to an improvement in classification accuracy?

The plot of these results is presented in `Figure 6` of the article.

Just run it and it will show detailed output at runtime. After it finishes running, results will be saved in `final-allsubj-5fold-3subjaside-selectedfeatures.csv` at the root of `base_path` previously defined in the `Utils` section.

#### Overfitting Test
**Notice: This scenario needs a folder named weights beside the notebook to store weights for faster runs. It may need around 40GB of storage for this folder**

This cell is run for section 4.5 of the article, Answering the question: 

> Why does the overall classification accuracy improve when subject bias is removed, contrary to the expected decrease?

The plot of these results is presented in `Figure 5` of the article.

Just run it and it will show detailed output at runtime. After it finishes running, results will be saved in `allsubj-5fold-3subjaside-overfit-allfeatures.csv` and `steps.csv` at the root of `base_path` previously defined in the `Utils` section.


### Raw Classify
The file `Raw Classify.ipynb` contains methods we experimented with that need high (minimum of 16GB of RAM) computational resources. Mainly runs on raw data. Below you'll find a description of each section in the file and how to run it.

#### Imports
Contains all of the libraries needed for runnig this notebook. You need to run this cell only once.

#### Utils
Contains some variables or functions that may be useful.

Remember to set `base_path` according to your environment. It must point out where the dataset exists.

#### Loading Data
Here it loads the last 20 seconds of the data from all experiments into a variable named `data`. We use this variable in the entire notebook for selecting train and test data. You need to run this cell once. It also reads labels. You may need to change the path of `label.mat` according to your setup. You must have the `Preprocessed_Data` folder in the root of `base_path` for running this file.

#### Raw Data - 5 Fold - Last 20 Seconds
This cell is run for section 4.1 of the article, Answering the question: 

> Can emotional information be extracted from raw EEG data?

The plot of these results is presented in `Figure 1` of the article.

Just run it and it will show detailed output at runtime. After it finishes running, results will be saved in `rawdata-5fold-last20sec.csv` at the root of `base_path` previously defined in the `Utils` section.
