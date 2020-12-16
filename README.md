
### Table of Contents

1. [Installation](#installation)
2. [Project Motivation](#motivation)
3. [File Descriptions](#files)
4. [Results](#results)
5. [Licensing, Authors, and Acknowledgements](#licensing)

## Installation <a name="installation"></a>

This project requires the installation of Jupiter notebooks and the Anaconda distribution of Python and associated libraries.  The code should run with no issues using Python versions 3.*.
The project uses four *.csv files azdias.csv, customers.csv, mailout_train.csv, and mailout_test.csv.  The files are proprietary and thus not included in this repository but might be obtained from Udacity.  

## Project Motivation<a name="motivation"></a>

The purpose of this project is to apply machine-learning techniques to the interpretation of demographic data.  The insight gained through such an analysis can help a company target its marketing and business development campaigns ore effectively.

## File Descriptions <a name="files"></a>

The project is divided into two notebooks that must be executed sequentially:  
1. Notebook1:  Data exploration and cleaning
  * Reading the *.csv files into pandas data frames
  * Assessing null values in columns and rows, and removing elements as appropriate
  * Identifying categorical features and replacing them with dummy variables (standard get_dummy() techniques).

The "cleaned" dataframes are then saved as *.csv files for use as input to Notebook2.  
Therefore, different strategies can be explored in the second notebook without having to start from scratch.

2. Notebook2: Unsupervised and supervised classification
  * Reading the cleaned data
  * Exploring dimensionality reduction with PCA
    - Interpreting top Principal Components
  * Clustering population and customers data with KMeans
    - Interpreting differences between population and customers clusters
  * Developing predictive models for mailout data
    - Tuning up and comparing AdaBoost and RandomForest classifiers
    - Predicting RESPONSE with an augmented mailout dataset and a binary target (y)
    - Predicting RESPONSE with a synthetic target based on knowledge derived from the previous cluster analysis 
		
NOTE:  The coding details are specific to these datasets but the process can be replicated to study other situations.

model_filename.pkl is the pickle file storing the trained model; the name is specified in the command line.

## Results<a name="results"></a>

  * PCA weighs more strongly the following features:
    - Financial status (FINANZ_, HH_EINKOMMEN_SCORE)
    - Residental housing types (PLZ8_)
    - Advertising preferences or sensitivity (CJT_)
    - Car ownership characteristics (KBA05_, KBA13_)
These observations would invite the company to profile existing customers along these dimensions and target new customers accordingly.

  * Cluster distribution seems to confirm the PCA conclusions:

   - The features with the largest weigths in the cluster where the difference between the general population and customers is the greatest show the importance of the financial variables--both investment style (FININANZ_) and economic means ( LP_STATUS_).

   - This observation is confirmed by looking at the next cluster in term of differences. In this cluster we also note the weights given to the features associated with advertising (CJT_TYP_) but we do not have enough information to interpret this further.

  * Predictions

The training dataset (mailout_train) is strongly unbalanced with only 1.2% of positive RESPONSE.  It does not seem that the two predictive models developed are effective in targetting likely customers against such odds.

A summary is available on Medium.

## Licensing, Authors, Acknowledgements<a name="licensing"></a>
The initial data were provided by Arvato/Betelsman and are proprietary.  Otherwise, the code is free to use.
