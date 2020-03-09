<p>
<img src="https://i.imgur.com/E2TUJSD.jpg" width="900" height="400">
</p>

## Problem Statement (source: Kaggle)
The challenge is to create a model that uses data from the first 24 hours of intensive care to predict patient survival. MIT's GOSSIS community initiative, with privacy certification from the Harvard Privacy Lab, has provided a dataset of more than 130,000 hospital Intensive Care Unit (ICU) visits from patients, spanning a one-year timeframe. This data is part of a growing global effort and consortium spanning Argentina, Australia, New Zealand, Sri Lanka, Brazil, and more than 200 hospitals in the United States.

## Evaluation
Submissions will be evaluated on the Area under the Receiver Operating Characteristic (ROC) curve between the predicted mortality and the observed target (hospital_death).

## Submission Format
For each `encounter_id` in the test set, you are asked to explore the columns of data (for example, patient laboratory results, demographics, and vital signs) and create a model for predicting the probability of patient survival.

A `hospital_death` value of 1 corresponds to patient death and a value of 0 corresponds to survival.

Your submission file should contain a header and have the following format:

```
encounter_id,hospital_death
1,0.814
2,0.01
3, 0.5

etc
```

---

## Data

The [Datasets](Datasets) :file_folder: contains the required data files:
- **training_v2.csv**: the training data which contains 91,713 patient records. 
- **WiDS Datathon 2020 Dictionary.csv**: additional information about the data.
- **unlabeled.csv**: the test data which contains 39,308 records. Predictions were required to be submitted against the test data.

## Files

Working in a 4-person team, we decided on Jupyter Notebooks using Python :snake: as the programming language and divided up the tasks into what you now see as folders in the repository:
- [EDA](EDA) (Exploratory Data Analysis)
- [Data Preprocessing](DataPreprocessing)
- [Modeling](DataModeling)
- Wrapping the entire code base into modular functions 

### :sparkles: main.ipynb :sparkles: 
The star of the show was most definitely our final file named [main.ipynb](main.ipynb). All our efforts were consolidated here. Feel free to clone the repo, run the main.ipynb file and see the magic happen! 

:warning: Make sure you have Python3, Jupyter and all the third-party libraries installed in the environment prior to running the file.

### Output

When you run `main.ipynb`, an output file called `submission_file.csv` will be created. It will contain 2 columns as per the Kaggle requirements: 
- `encounter_id` 
- the vector of prediction probabilities for the target variable in `hospital_death`

## Machine Learning

### Exploratory Data Analysis
- Check for **duplicate, unique and missing values** in the dataset.
- **Data Profiling**
    - We split the numerical columns and categorical columns and obtained a summary statistics against both column types. This allowed us to gain a general idea about the quality of the data and to check for anomalous patterns.
- **Visualization**
    - We used univariate analysis to visually observe the distribution of data in particular columns.

### Data Preprocessing
- **Resampling**
    - Downsampling was performed to resolve the class imbalance problem. 
    - Followed by, shuffling the downsampled data to randomize the class distribution in the new dataset.

- **Missing Value Imputation**
    - For numerical variables: The missing values were imputed with their column-wise mean.
    - For categorical variables: Based on team discussions, missing values were imputed with values as illustrated in the examples below.
    > Example 1: Imputed the missing values for `ethnicity` with _Other/Unknown_ since that value was already present in the data.
    
    > Example 2: Imputed missing values for `gender` as either _M_ or _F_ based on the percentage of the non-null values of these 2 classes. 

- **Dimensionality Reduction**
The original training data had 186 features and in order to reduce dimensions, we did the following:
    - Dropped columns containing more than 75% null values
    > The column `h1_pao2fio2ratio_min` was missing 83.5% of its data and hence was dropped.
    - Reduced collinearity
    > Dropped the `height` and `weight` columns since they were collinear to the `bmi` column.
    - Dropped columns based on manual evaluation of the data 
    > Dropped `readmission_status` since the entire column contained the same value for every observation and didn't add any extra information to the predictability of the target variable.

### Modeling

Various classification algorithms were used to model the data:
- Logistic Regression
- Random Forest Classification
- Gradient Boosting
- Support Vector Machine

Gradient Boosting was eventually selected as the final model.

### Model Tuning

- **Hyperparameter Tuning**
    - Grid Search was used to find the best set of hyperparamters to run the model with. 
- **Cross-Validation**
    - We applied 10-fold cross validation in order to use the entire training set efficiently for both training as well as validation (in different runs). 
- **Feature Engineering**
    - We added Group Description Statistics to the dataframe in order to increase our score which it did!

### Programming Aspects
- Use of Python's `os` folder to resolve the path to the data files.
**Advantage:** Anyone cloning the repo can immediately run the main file (provided they have all the dependencies installed as mentioned above.)

- Wrapping the entire code base into functions. 
**Advantage:** The code instantly became more readable, modular and reusable.

- Following Python's PEP-8 standards such as:
    - standard library imports before third-party imports
    - using `import random` instead of `from random import *`
    - using proper naming conventions for variable and function names
    - writing docstrings for every function
    - writing comments at the indentation level of the code

## Result

We achieved an overall AUC ROC (Area Under the Receiver Operating Characteristics Curve) score of 92.4%. Below is the progression of our score levels:

Implementation | AUC ROC Score
--- | ---
Gradient Boosting Classifier | 80%
10-fold Cross Validation | 89%
Feature Engineering using Group Description Statistics | 92.4%


