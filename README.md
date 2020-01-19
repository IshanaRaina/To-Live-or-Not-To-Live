# kaggle-wids-2020

## Problem Statement 
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

## Timeline
February 21, 2020: Team Merger deadline. This is the last day competitors may join or merge teams.

February 24, 2020: Entry deadline. You must accept the competition rules by this date in order to compete.

February 24, 2020: Final submission deadline.

Winners will be announced at the WiDS Conference at Stanford University on March 2, 2020.

All deadlines are at 11:59 PM UTC on the corresponding day unless otherwise noted. The competition organizers reserve the right to update the contest timeline if necessary. Please join the community mailing list to receive all updates and announcements.

**Source: Kaggle**
