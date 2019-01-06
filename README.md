# Customer-Segmentation
Customer Segmentation Report for Arvato Financial Solutions

### Table of Contents

1. [Installation](#installation)
2. [Project Analysis](#motivation)
3. [File Descriptions](#files)
4. [Results](#results)
5. [Licensing, Authors, and Acknowledgements](#licensing)

## Installation <a name="installation"></a>
The code in this project is written in Python 3.6.6 :: Anaconda custom (64-bit).
The following additional libraries have been used:
* pandas
* numpy
* matplotlib
* seaborn
* sklearn
* warnings
* time
* progressbar
* plot_learning_curve
* xgboost (see installation notes below)

In order to install XGBoost on Mac, please follow the steps below:
```
# This is from https://machinelearningmastery.com/install-xgboost-python-macos/
# except I didn't install gcc using MacPorts but brew. Also assumed python 3.6
# already installed


# Open a terminal and install latest gcc (gcc-8) in your home dir
brew install gcc

# Add the following lines to .bash-profile in the home directory
alias gcc='gcc-8'
alias cc='gcc-8'
alias g++='g++-8'
alias c++='c++-8'
export CC='gcc-8'
export CXX='g++-8'

# Install xgboost

git clone --recursive https://github.com/dmlc/xgboost

cd xgboost/

cp make/config.mk ./config.mk

make -j8

# Final install xgboost into python

cd python-package

sudo python setup.py install

# And that should be it! You can verify if everything works with this code
$ python
Python 3.6.6 |Anaconda custom (64-bit)| (default, Jun 28 2018, 11:07:29)
[GCC 4.2.1 Compatible Clang 4.0.1 (tags/RELEASE_401/final)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> import xgboost
>>> print("xgboost", xgboost.__version__)
xgboost 0.81
>>>
```
## Project Analysis<a name="motivation"></a>
This project shows that cutting-edge algorithms typically used in Data Science competitions can be extended to handle real life problems, like predicting if a lead can be converted with over 80% accuracy.
The data for this project has been provided to Udacity by Bertelsmann Arvato Analytics, and represents a real-life data science task. It includes demographics for customers of a mail-order sales company in Germany, a dataset of general population demographics, a mailout campaign with response and a final test dataset to make predictions on a Kaggle competition.
We used unsupervised learning techniques to describe the relationship between the demographics of the company's existing customers and the general population of Germany . This allowed to describe which parts of the general population are more likely to be part of the mail-order company's main customer base, and which parts of the general population are less so (Customer Segmemtation).
We then developed a supervised learning model to predict which individuals are most likely to convert into customers using a marketing campaign dataset. Tree-based and boosting algorithms usually perform very well on tabular data, and are widely employed across data science competitions. After comparing learning curves from four candidate algorithms using stratified kfold cross-validation, we have chosen XGBoost and proceeded to tune its parameter following a step-by-step strategy rather than applying a wide GridSearch. This allowed us to tune XGBoost in around 4hrs on a MacBook.
The final optimized model was run against a test dataset and gave a final score of 0.80467. The best score in the Leaderboard is 0.80819.
Metric
 The metric used in the model is ROC (Receiver Operating Characteristic Curve) AUC ("Area under the ROC Curve"). AUC provides an aggregate measure of performance across all possible classification thresholds. One way of interpreting AUC is as the probability that the model ranks a random positive example higher than a random negative example.
AUC ranges in value from 0 to 1. A model whose predictions are 100% wrong has an AUC of 0.0; one whose predictions are 100% correct has an AUC of 1.0. AUD is scale-invariant, i.e. it measures how well predictions are ranked, rather than their absolute values. This property makes it very useful in case of unbalanced datasets, as we will see later in this project.

## File Descriptions <a name="files"></a>
The Jupyter notebooks included in this project are:
- Arvato Project Workbook.ipynb

Python Files:
- plot_learning_curve.py  utility function to plot learning curves

Data files (under data directory):
- azdias_info_reloaded.csv  dataframe of feature description
- Udacity_AZDIAS_052018.csv: Demographics data for the general population of Germany; 891 211 persons (rows) x 366 features (columns).
- Udacity_CUSTOMERS_052018.csv: Demographics data for customers of a mail-order company; 191 652 persons (rows) x 369 features (columns).
- Udacity_MAILOUT_052018_TRAIN.csv: Demographics data for individuals who were targets of a marketing campaign; 42 982 persons (rows) x 367 (columns).
- Udacity_MAILOUT_052018_TEST.csv: Demographics data for individuals who were targets of a marketing campaign; 42 833 persons (rows) x 366 (columns)



## Results<a name="results"></a>
The Customer Segmentation report shows that customers of the mail order company are positively correlated with indicators of wealth, tend to be less mobile than the general population and live in buildings/neighborhoods with a smaller number of households. They tend to drive luxury cars, do not belong to youngest generations and they have a more conservative approach to financial investments. Their customer journey experience is more of a conservative, traditionalist shopper as opposed to online-shopper and cross-channel.
XGBoost was the best Supervised Learning model to predict which individuals are most likely to convert into customers using a marketing campaign dataset, with a final CV score of 0.7674 with 323 estimators. This model was used against a test dataset in the Kaggle competition, with a final score of 0.80467.

## Licensing, Authors, Acknowledgements<a name="licensing"></a>
For licensing see LICENSE file.
Due to the sensitive and proprietary nature of the demographics data used in the project, the data will not be provided on this page. The data should be considered exclusive to the project and not be used for any other purpose, as according to the Terms & Conditions associated with the project on Udacity. The only file that will be present on this page is an example of what a submission should look like for this competition.
