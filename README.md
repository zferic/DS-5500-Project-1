---
author:
- 'Thomas Carpenito, Zlatan Feric'
date: September 2019
title: DS 5500 Proposal
---

\maketitle
Summary
=======

Puerto Rico continues to have some of the highest rates of preterm birth
(delivery before 37 weeks of gestation) compared to the US and the rest
of the world. It is hypothesized that exposure to an increase in
contamination in the environment is a contributing factor to preterm
birth. Contamination can occur in a multitude of ways such as drinking
contaminated water, using products containing high concentration of
certain chemicals, or even from eating contaminated foods. The Puerto
Rico Test site for Exploring Contamination Threats (PROTECT) study has
been recruiting pregnant women since 2011 in the northern part of the
island, and collecting a vast amount of data in an effort to find the
cause of high adverse birth outcomes.

The current data sets include a wide array of different data types:
analytes, biological and environmental data, as well as individual level
characteristics (all hereafter known as covariates). In total there are
576 measurable covariates and 1,020 mothers. The primary goal of this
analysis is to see how accurately we can predict the term status of a
new born infant given time varying and static covariates while comparing
and testing various imputation methods.

While PROTECT has conducted many analysis of potential contributing
factors, studies mostly focused on analyzing very specific areas in
order to try and find associations. (List some references) Our approach
will look into using roughly 576 covariates in order to create a more
accurate and robust model for predicting preterm.

                        Null   Fullterm       Preterm        p-val
  ------------------ -- ------ -------------- -------------- -------
                               913            107            
  Current Age           1      26.7 (5.5)     26.9 (5.6)     0.708
  Weight (pounds)       40     151.9 (32.0)   158.1 (36.9)   0.115
  Child Number          110    0.7 (0.8)      0.9 (0.9)      0.066
  Pregnancy Number      11     1.9 (1.0)      2.1 (1.3)      0.066

Research Plan
=============

For this analysis, we will be comparing the prediction accuracy of two
different instances of one aggregated dataset. The first instance will
simply use K-nearest neighbors (KNN), Least Absolute Shrinkage and
Selection Operator (LASSO), decision trees, and k-fold cross validation
to predict term status of mothers. For the second dataset we will use
KNN to independently impute the missing values within each column (of
the original dataset) creating a new complete dataset. We will then use
this complete dataset to again predict term status using the previously
mentioned machine learning techniques (KNN, LASSO, and decision trees).
Finally, we will compare predictive ability both within and across
datasets and methodologies using cross validation and the mean squared
error (MSE).

The general flow of our project will be as follows: First, we will merge
all appropriate data sets in to a single data set. Second, we will
generate a simple correlation matrix among all covariates to see if
there is any general clustering present (either between covariates
across time points or within time points between covariates). Next, we
will generate our second instance of the data frame using a developed
imputation method (described below). Finally, we will predict baby term
status using the previously mentioned models for both data sets and
compare.

The method for imputing missing data in the second data set is as
follows: first, moving one column at a time, we will isolate the entire
the dataset for which there are values for that particular column. We
will then hold out one third of those rows (as a testing set) and the
remaining two thirds will be used as the training set. We will then use
KNN and cross validation on the training set to generate a predictive
model. Finally, we will generate a MSE on the held out testing data and
compare our results to the generated MSE when only using the sample mean
(or mode, depending on categorical/numerical data). For whichever method
(KNN or sample mean) generates the lowest MSE we will then impute the
missing data from the original dataset and add this column to a new data
set. This new dataset will continue to grow as each new column is
imputed with this technique (Figure
[\[fig:imputation\]](#fig:imputation){reference-type="ref"
reference="fig:imputation"}).

![Diagram for explaining the analysis and imputation
methodology.[]{label="fig:imputation"}](figures/imputation.png){#fig:imputation
width="\textwidth"}

Preliminary Results
===================

Add more preliminary results - Zlatan

1-2 paragraphs describing any preliminary results you have. At the very
least, this should include some basic summary statistics or exploratory
data analysis results from your dataset(s) or a pilot/preliminary
dataset (if you are scraping or mining data).

Blood and urine samples were collected on pregnant women 1-3 times
throughout their pregnancy at targeted intervals 20,24, and 28 weeks
gestation. The project ran different blood and urine panels on the
samples collected. The panels that we plan to look at in this analysis
are Hormones, Trace metals, Inflammation, Pesticieds, PAHS, Phenols,
Phthalates, and Oxidative stress. The heatmap in Figure 1 suggests that
data is not missing at random, but rather depends on the partifcipant.

Preliminary results show a variance in available data between the
different classes of biological panels

\centering
  ---------------------- -------- ---------- ----- ----- -----
     Biological Panel     Source   Analytes   V1    V2    V3
   \[0.5ex\] Tracemetal   Blood       24      624    0    490
         Hormones         Blood       15      541    0    405
       Isoprostane        Blood       2       257   349   221
       Inflammtion        Blood       5       201    0    161
         Phenols          Urine       12      827   850   662
        Phthalates        Urine       19      828   851   661
           PAH            Urine       8       394    0    394
        Pesticides        Urine       28      153   48    151
        Tracemetal        Urine       21      460   435   330
  ---------------------- -------- ---------- ----- ----- -----

  : N=Number of subjects with at lest one sample and a pregnancy
  outcome.[]{label="table:1"}

1\. Getting covariates: mothers age, smoking 2. Categorizing number of
preterm vs. term and mean gestation

![The black color indicates complete cases and the beige indicates
missing](figures/missingdata.png){width="\textwidth"}

Out of the 1020 in the PROTECT study, 913( 89.5 $\%$) delivered full
term ( gestational age $\geq$ 37 weeks) and 107 (10.5 $\%$ delivered
pre-term (gestational age $\le$ 37 weeks.) The average gestational age
was 39.31 weeks for term deliveries, and 34.21 weeks for pre-term
deliveries. The imbalance in the outcome will require additional
pre-processing and model adjustments to properly carry out training and
analysis.

\centering
References
==========
