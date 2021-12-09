# Detroit_Traffic_Crash_Project_602
# 
The Detroit_Traffic_Crash project is about the crashes that happened between 2011 and 2017. We want to focus on the predicting whether the person involved in the crash has consumed alcohol or drug.The project contains the visualization in the form of text and various graphs, the Python libraries which are used in this notebook are Numpy, Pandas, Matplotlib, Seaborn. The modelling is done with the help of several modules of Scikit-Learn package.

# Dataset Description
The dataset is about the traffic crashes in Detroit city available on [OpenData.gov](https://data.ferndalemi.gov/datasets/detroitmi::traffic-crashes/about). There are 36 columns(including target column) in total and about 142K records. The description of the columns is not provided, so interpreting the values present in the columns is unclear. We have tried interpreting the values by mapping the values to the similar dataset of crashes occurred in [Maryland.](https://opendata.maryland.gov/Public-Safety/Maryland-Statewide-Vehicle-Crashes/65du-s3qu) There were about 12K missing values in the the column 'jurisdiction', imputing the median or mode value to it would not be appropriate as the jurisdiction for the different factors can be same and this can mislead the training model. So we have dropped those 12K values.
 

# Business Question/Problem Statement
Predicting the presence of matter (Drug/ Alcohol) in the person's body who involed in the crash is the problem statement. This project can be a potential alternative to confirm the presence if the results of drug test takes time or not possible to conduct. We will be tuning the Logistic Regression and Random Forest model based on the accuracy metrics.


# Exploratory Analysis Findings
- Initially, based on three columns, we created 8 classes.
- The columns such as 'deer', 'school_bus', 'train', can be dropped while modeling as these columns are singleton
- After checking the percent values of the crashes, we found the almost similar distribution within the alcohol and drug
- After drawing the similarity, it can interpreted that the most of the crashes happen 'Same Direction Rear End' but for other codes, the accurate mapping won't be possible as the factors for crashes in Detroit wouldn't be same as Maryland.
- Majority of the people who consumes alcohol or drug, their crashes are mostly occured around midnight while the people who didn't consume drug or alcohol, their crashes were    mostly reocrded between 2pm and 6pm.
- Most of the crashes that happened, which involve the people who haven't consumed drug or alcohol occurred at the evening peak hours between 3pm to 7pm (Time when people get home)
- Maximum of the accidents have happened in the local roads where the red_light_running also happens most, but most of them are very less severe.

__Inference:__ From these points we can infer that the inspection or patrolling duty from evening to midnight should be increased, this might help to find more people who consumes alcohol or drug and drive.



# Classification Results
We segemented our experiment into three parts:
- __Class Imbalance (8 Classes)__
    - Logistic Regression__
      - Accuracy: 86%
      - With the imbalance, the model was only able to do good on 'Non-Consumed Youth' and for others it couldn't do well.
      - The data has very low variance.
      - Similarly after training the model such as Decision Tree and Random Forest, similar results were obtained. With the more number of co-related classes, the model gets confused, so instead of differentiating the classes on the basis of elder or youth, we will focus on whether a person has alcohol or drug consumed.
  
 - __Balanced Classes SMOTE(8 Classes)__
    - __Logistic Regression__ 
      -  Accuracy: 38%
      - With the up-sampled values, the model was able to identify all the classes but not with sufficiently good accuracy. With the more number of co-related classes, the model gets confused, so instead of differentiating the classes on the basis of elder or youth, we will focus on whether a person has alcohol or drug consumed in the third part.

 - __Balanced Classes SMOTE(3 Classes)__
     - __Logistic Regression (Ridge_Regularization(C): 0.01, Solver: SAG)__
        - Accuracy: 81%
        - The class Drug has the lowest number of records (before SMOTE) and generating significantly high number of samples using least values, low variance got slightly better.
      - __Decision Tree (GridSearch(max_depth: 7))__
        - Accuracy: 83%
        - The class Drug has the lowest number of records (before SMOTE) and generating significantly high number of samples using least values, low variance got slightly better.
      - __Random Forest (n_estimators=100, criterion='entropy', max_depth=6)__
        - Accuracy: 80%
        - The model has memorized the values of 'Alcohol' class as its recall is 1.
      - __Support Vector Machine (Defaults) (Took a lot amount of time)__
        - Accuracy: NA
        - NA


# Potential Next Steps and Follow-ups
- The help from an SME regarding the significance of features such as 'dis_ctrl_i', 'young', etc and their values should be explained, as it can help to perform the required feature engineering appropriately.
- The 12K missing values in the jurisdiction should be addressed, we can run a clustering model on those values but which feature can be the most relevant for it is our concern to check.
- The additional features such as the 'exact_age' of the person instead of a boolean feature 'elderly' can provide a good variance. More specific numeric is better than boolean feature.
- As per the inference about the patrolling, we need more data where the person has consumed alcohol or drug and involved in the crash. Significant level of variance will be obtained if this step is achieved.
- From the above point, introducing the additional continous numeric features can be a good improvising point. Features such as 
