# Detroit_Traffic_Crash_Project_602
The Detroit_Traffic_Crash project is about the crashes that happened between 2011 and 2017. We want to focus on predicting whether the person involved in the crash has consumed alcohol or drug. The project contains the visualization in the form of text, and various graphs, the Python libraries used in this notebook are Numpy, Pandas, Matplotlib, Seaborn. The modeling is done with the help of several modules of the Scikit-Learn package. Two version of the notebooks are uploaded, the final and the elaborated one which contains extra modeling part.

# Dataset Description
The dataset is about the traffic crashes in Detroit city available on [OpenData.gov](https://data.ferndalemi.gov/datasets/detroitmi::traffic-crashes/about). There are 36 columns (including the target column) total and about 142K records. The description of the columns is not specified, so interpreting the values present in the columns is unclear. I attempted to evaluate the data by comparing it to a similar dataset of crashes that occurred in [Maryland](https://opendata.maryland.gov/Public-Safety/Maryland-Statewide-Vehicle-Crashes/65du-s3qu). There were about 12K missing values in the column 'jurisdiction', imputing the median or mode value to it would not be appropriate as the jurisdiction for the different factors can be the same and this can mislead the training model. So we have dropped those 12K values.
 

# Business Question/Problem Statement
Predicting the presence of matter (Drug/ Alcohol) in the person's body involved in the crash is the problem statement. This project can be a potential alternative to confirm the presence of the results of drug test takes time or not possible to conduct. According to the 4th Amendment, the police need a warrant or to develop probable cause that the person is intoxicated, the person involved in the crash can deny taking a blood/breath test. This is the reason why we will find very few records on drugs and alcohol. Based on the historical data, we can develop the instinct and we can eliminate the time delay to confirm the presence of the matter. We will be tuning the Logistic Regression and Random Forest model based on the accuracy metrics.

# Exploratory Analysis Findings


- Initially, based on three columns, we created 8 classes
- The columns such as 'deer', 'school_bus', 'train', can be dropped while modeling as these columns are singleton
- After checking the percent values of the crashes, we found an almost similar distribution within the alcohol and drug
- After drawing the similarity, it can be interpreted that most crashes happen 'Same Direction Rear End,' but for other codes, the accurate mapping won't be possible as the factors for crashes in Detroit wouldn't be the same as in Maryland
- The majority of the people who consume alcohol or drug their crashes mostly occur around midnight, while the people who didn't consume drugs or alcohol, crashes were mostly recorded between 2 pm and 6 pm
- Most of the crashes that happened, which involved the people who haven't consumed drugs or alcohol, occurred at the evening peak hours between 3 pm to 7 pm (Time when people get home)
- A maximum of the accidents have happened in the local roads where the red_light_running also happens most, but most of them are less severe
- We can step the primary roads into others except the top 10 roads but the top 10 primary roads covers less than 15% of the crashes and there are over 7K primary roads. So stepping all the primary roads into others except top 10 of them won't be good option as the variance in the data would be very low.

__Inference:__ From these points, we can infer that the inspection or patrolling duty from evening to midnight should be increased; this might help to find more people who consume alcohol or drug and drive.



# Classification Results
We segmented our experiment into three parts:

- __Class Imbalance (8 Classes)__
   - __Logistic Regression__
      - Accuracy: 86%
      - With the imbalance, the model could only do good on 'Non-Consumed Youth,' and for others, it couldn't do well
      - The data has very low variance
      - Similarly, similar results were obtained after training the model such as Decision Tree and Random Forest. With the more number of co-related classes, the model gets confused, so instead of differentiating the classes based on elder or youth, we will focus on whether a person has alcohol or drug consumed
- __Balanced Classes SMOTE(8 Classes)__
   -  __Logistic Regression__
      - Accuracy: 38%
      - With the up-sampled values, the model was able to identify all the classes but not with sufficiently good accuracy. With the more co-related classes, the model gets confused, so instead of differentiating the classes based on elder or youth, we will focus on whether a person has alcohol or drug consumed in the third part
- __Balanced Classes SMOTE(3 Classes)__
   - __Logistic Regression (Ridge_Regularization(C): 0.01, Solver: SAG)__
      - Accuracy: 81%
      - The class Drug has the lowest number of records (before SMOTE) and generates a significantly high number of samples using least values; low variance got slightly better
   - __Decision Tree (GridSearch(max_depth: 7))__
      - Accuracy: 83%
      - The class Drug has the lowest number of records (before SMOTE), and generating a significantly high number of samples using least values; low variance got slightly better
   - __Random Forest (n_estimators=100, criterion='entropy', max_depth=6)__
      - Accuracy: 80%
      - The model has memorized the values of the 'Alcohol' class as its recall is 1
    - __Support Vector Machine (Defaults) (Took a lot amount of time to compute, code mentioned in 'Elborated' file)__
      - Accuracy: NA
      - NA
   -  __Best Estimator:__
      - The best estimator is the shown above, the solver is 'Newton-CG' as it was able to deal well with the all the three classes than other solvers, although there is not vast differences in the results of all the models
      - 'LBFGS' is not used in the Grid Search as it is not able to converge in 1000 iterations
      - In terms of computing time, Decision tree was the fastest of all, but it shows more deviation among precision and recall than the deviation in Logistic Regression, that's why we are selecting Logistic Regression as the best estimator


# Potential Next Steps and Follow-ups

- The help from an SME regarding the significance of features such as 'dis_ctrl_i', 'young', '(a, b, c)_level_count', etc., and their values should be explained, as it can help to perform the required feature engineering appropriately
- The 12K missing values in the jurisdiction should be addressed, we can run a clustering model on those values but which feature can be the most relevant for it is our concern to check
- The additional features such as the 'exact_age' of the person instead of a boolean feature 'elderly' can provide a good variance. More specific numeric is better than the boolean feature
- As per the inference about the patrolling, we need more data on where the person has consumed alcohol or drug and was involved in the crash. A significant level of variance will be obtained if this step is achieved
- Introducing the additional continuous numeric features can be a good improvising point from the above point. Features such as car_damage_severity, age of the person can help in feature engineering.
