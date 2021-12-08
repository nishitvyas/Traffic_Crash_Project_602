# Detroit_Traffic_Crash_Project_602
# 
The Detroit_Traffic_Crash project is about the crashes that happened between 2011 and 2017. We want to focus on the predicting whether the person involved in the crash has consumed alcohol or drug.The project contains the visualization in the form of text and various graphs, the Python libraries which are used in this notebook are Numpy, Pandas, Matplotlib, Seaborn. The modelling is done with the help of several modules of Scikit-Learn package.

# Dataset Description
The dataset is about the traffic crashes in Detroit city available on [OpenData.gov](https://data.ferndalemi.gov/datasets/detroitmi::traffic-crashes/about). There are 36 columns(including target column) in total and about 142K records. The description of the columns is not provided, so interpreting the values present in the columns is unclear. We have tried interpreting the values by mapping the values to the similar dataset of crashes occurred in [Maryland.](https://opendata.maryland.gov/Public-Safety/Maryland-Statewide-Vehicle-Crashes/65du-s3qu) There were about 12K missing values in the the column 'jurisdiction', imputing the median or mode value to it would not be appropriate as the jurisdiction for the different factors can be same and this can mislead the training model. So we have dropped those 12K values.
 

# Business Question/Problem Statement
Predicting the presence of matter (Drug/ Alcohol) in the person's body who involed in the crash is the problem statement. This project can be a potential alternative to confirm the presence if the results of drug test takes time or not possible to conduct. We will be tuning the Logistic Regression and Random Forest model based on the accuracy metrics.

- ____ 

- __With the proportion it is known that young people are more likely to drink and drive as compared to elderly people.__

- ____

__Inference:__ From these points we can infer that the inspection or patrolling duty from evening to midnight should be increased, this might help to find more people who consumes alcohol or drug and drive.



# Exploratory Analysis Findings
- Initially, based on three columns, we created 8 classes.
- The columns such as 'deer', 'school_bus', 'train', can be dropped while modeling as these columns are singleton
- After checking the percent values of the crashes, we found the almost similar distribution within the alcohol and drug
- After drawing the similarity, it can interpreted that the most of the crashes happen 'Same Direction Rear End' but for other codes, the accurate mapping won't be possible as the factors for crashes in Detroit wouldn't be same as Maryland.
- Majority of the people who consumes alcohol or drug, their crashes are mostly occured around midnight while the people who didn't consume drug or alcohol, their crashes were    mostly reocrded between 2pm and 6pm. __Inference:__ From these points we can infer that the inspection or patrolling duty from evening to midnight should be increased, this  might help to find more people who consumes alcohol or drug and drive.
- Most of the crashes that happened, which involve the people who haven't consumed drug or alcohol occurred at the evening pick hours between 3pm to 7pm
- Maximum of the accidents have happened in the local roads where the red_light_running also happens most, but most of them are very less severe.


# Classification Results
We segemented our experiment into three parts:
- __Model 1: Logistic Regression (Class Imbalance)__
    - __Accuracy:__ 38%
    - With the imbalance, the model was only able to do good on 'Non-Consumed Youth' and for others it couldn't do well.
    - The data has very low variance.
  
 - __Model 1: Logistic Regression (Class Imbalance)__
    - __Accuracy:__ 38%
    - With the imbalance, the model was only able to do good on 'Non-Consumed Youth' and for others it couldn't do well.
    - The data has very low variance.
  
 



- In the first part we have implemented the cross validation score on Logistic Regression(LogR), Decision Tree(DT) and Support Vector Machine(SVM). We got good accuracy on SVM but the deviation was of 2%, for DT and LogR it was 64% for both and the deviation of 2% and 1% repectively. 
- For the second part, we passed three models into an ensemble where the voting was selected as 'hard', since we are concerned about the accuracy, probability can be opted out.
- In the third part, we performed the GridSearch on the Ensemble to get the best estimator and its score, which was 67% (__max of all__)
- Lastly, we performed the AdaBoosting Classification where we kept 500 estimators but we got 64% which wasn't that effective as GridSearch.
- As __conclusion__, we should consider the Ensemble with the GridSearch as it gave maximum accuracy of all and also the deviation was 0%, it took __more computations__ than other models.


# Potential Next Steps and Follow-ups
License type details, or to know the exact age of the person 


The consideration of the wind_dir, origin and dest needs to done for checking how the model predicts then.
Also the clarification on the weather of the origin or dest is not given.

