
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
    - Predicting RESPONSE with an augmented mailout dataset and a binary target (y) (Strategy 1)
    - Predicting RESPONSE with a synthetic target based on knowledge derived from the previous cluster analysis (Strategy 2)
		
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

  * Strategy 1 predictions
 
We split mailout_train 20/80 between testing and training. The accuracy for the test results was found to be marginally better for AdaBoost (81.3%) than for RandomForest (78.8%), although the ROC curve shown below implies that both classifiers gave virtually identical results.

![alt text](https://github.com/gsegol/customer_segments/blob/master/ROC.png " roc_curve"

  * Strategy 2 predictions
 
 With  the same 80/20 split as in Strategy1, we find RandomForest to be more accurate at predicting the test data. The accuracy with RandomForest was 82.9% vs. 49.4% for AdaBoost.  With a 70/30 split, the accuracy of RandomForest (81.6%) is almost the same as previously. The accuracy of AdaBoost (60.6%) is higher than before, but the gap between the results of the two classifiers is still significant.

We conclude AdaBoost performs marginally better than RandomForest when we use the binary form of the target y (Stragtegy 1). In contrast, RandomForest appears significantly more reliable than AdaBoost when y is not binary (Strategy 2). We base this assessment on the fact that the accuracy of RandomForest is stable when we change the ratio between training and testing subsets, while the accuracy of AdaBoost changes significantly when we vary this ratio.
  
A summary is available on Medium (https://genevievesegol.medium.com/r-s-v-p-2217af931016)

## Licensing, Authors, Acknowledgements<a name="licensing"></a>
The initial data were provided by Arvato Financial Services and are proprietary.  Otherwise, the code is free to use.
