
# Predicting High Blood Pressure with Classification Model
This topic was chosen for Metis Data Science Bootcamp Summer 2020 Cohort's Project 3 on Classification.

## GENERAL INFORMATION
Author & Investigator: **[Celina Plaza](https://github.com/cecann10)**

Institution: **Metis**

Email: celina.plaza@gmail.com

Date of data collection: 2020-07-20 through 2020-07-29

## PROJECT OVERVIEW
### Context
High blood pressure is both a high health risk and economic risk for America.  In 2017, high blood pressure was a primary or contributing cause of death for more than 472,000 people in the United States; that is nearly 1,300 deaths each day.*  Additionally, high blood pressure cost the United States about $131 billion each year, based on an average over 12 years from 2003 to 2014.**

The model developed for this project intends to help the medical community identify those that have high blood pressure and help idenify signals that an individual can be aware of that may cause high blood pressure.

High blood pressure for this model was defined in accordance to American College of Cardiology and the American Heart Association's guidelines published in 2017 that defines high blood pressure as a reading greater than 130 mm Hg for Systolic Blood Pressure or greater than 80 mm Hg for Diastolic Blood Pressure.

All data was gathered from the Center for Disease Control's National Health and Nutrition Examination Survey (NHANES) results for the years 2007 - 2016.  The survey is conducted in two-year cycles and is representative of the non-institutionalized, U.S. population. While youth are included in this survey, this model only examined data for adults between the ages of 18-80.



### Goal
Find a classification model that identifies features of individuals' demographics, behaviors, or other health conditions that could help idenifity whether or not the individual has high blood pressure.  By identifying those features it could help medical professionals have warning signs a patient could be at risk and also help individuals be better aware of risks and susceptibility to high blood pressure.


### Findings
Multiple featues were considered for the classifcation modeling:
- BMI (kg/m**2)
- Waist Circumference (cm)
- Height (cm)
- Weight (kg)
- Gender
- Age
- Race
- Frequency of eating out
- Frequency of eating ready-to-eat meals
- Frequencey of eating frozen foods
- Whether smoked cigarettes 100 times in lifetime
- Current frequency of smoking cigarettes
- Whether have vigorous activity at work (over 10 min avg daily)
- Whether have moderate activity at work (over 10 min avg daily)
- Whether bike or walk to get to and from places 10 min continously each week
- Whether do vigorous activity for recreational activity
- Length of time spent sitting (avg daily)
- Whether have had more than 12 alcoholic drinks in past year
- Number of drinks had per day on average for past year
- Occupation status
- If have job, number of hours worked in past week

Final features of the model were:
- x1 = Age
- x2 = Weight (kg)
- x3 = Amount of alcohol consumed on average daily in past year
- x4 = Being a non-Hispanic Black adult (a 'dummy' value of 1)
- x5 = Being a current cigarette smoker (a 'dummy' value of 1)

A logistic Regression model leveraging oversampling for the 'positive' class (= high blood pressure) was found to be the best option between various classification models considered (Logistic Regression, Random Forest, and Decision Tree).  All models had similiar performance numbers, but the Linear Regression model selected could be a a higher threshold than the others while retaining high recall.  The model's resulting features were also easy to interpret and apply for individuals.

This model's main metric of performance was **Recall**, as it was determined that it was important to catch more people that could have high blood pressure (i.e. lower number False Negatives) vs. looking more to Precision where there would be risk of missing some people that did have high blood pressure (i.e. lower number False Positives).

With scaled data, formula for the model is:

Yp  =  -0.121 + 0.887(x1) + 0.340(x2) + 0.139(x3) + 0.152(x4) - 0.005(x5)

Threshold was set at 0.34, resulting in:

- **Recall: 0.899**
- Precision: 0.454
- Accuarcy score: 0.664
- F1 Score: 0.592
- ROC AUC Score: 0.720


### Conclusion
The model demonstrates a relationship between an individual having high blood pressure to their age, weight, race, alcohol consumption, and smoking of cigarettes.

Age is the most significant of indicators of high blood pressure, followed by weight, then race, alcohol consumption, and cigarette smoking.


The model indicates that a person is more likely to have high blood pressure as their age, weight, and alcohol consumption increases.  And also if they currently smoke and idenify as of the race of Non-Hispanic Black.



## METHODOLOGICAL INFORMATION

#### Methods used for collection/generation of data:
The data was collected from the [CDC's website](https://wwwn.cdc.gov/nchs/nhanes/continuousnhanes/default.aspx) where all survey data is offered in XPT format for free download and access.


#### Methods for processing and cleaning the data:
NHANES uses a code-based system for all of the categorical answers and also to idenify values such as 'Missing' and 'Don't Know'.  Missing or don't know values where removed and some categorical values were simplied to be yes/no responses where appropriate while in other cases where edited to 'real' category text values for readability sake of data.

No values where changed, but in two cases null values were replaced:
1. Average daily alcohol amount: only people who had answered in a previous that they had drank more than 12 alcoholic drinks in their lifetime were asked this question, so null values were changed to 0 to represent those who had previously responded that they had not had more than 12 drinks in their lifetime

2. Number of hours worked: only people who had answered in a previous that they had a job answered this question, so null values were changed to 0 to represent those who had previously responded that they were looking for job, not at job, or have no job

High blood pressure was determined for each sample by taking the average of three readings done for survey, all within a 10 minute period.  If the average reading was greater than 130 mm Hg for Systolic Blood Pressure and/or greater than 80 mm Hg for Diastolic Blood Pressure, the sample was marked as having high blood pressure -- all others were marked as not having high blood pressure.


#### Methods for analysis and modeling:
This project was specifically about application of classification modeling, so only models in this category were considered.  Logistic Regression, Decision Tree, and Random Forest models were all tested and compared.

'Dummies' were created for categorical data were needed and data was scaled for Logistic Regression modeling.  Imbalance was managed with oversampling for the Logistic Regression model.  GridSearch was implmented to optimize parameters for Decision Tree & Random Forest models.  Thresholds were considered to best meet target metric of recall performance without too great of sacrifice to other metrics of precision, F1 score, and accuracy.


## DATA & FILE OVERVIEW

- **File List**:
    * [Data Collection](data_and_modeling/data/NHANES_data_collection.ipynb) - worksheet for pulling in all XPT files that NHANES data originally came in.  Then data was combined to master document, filtered to key features, and cleaned.  csv of cleaned dataset is [here](data_and_modeling/data/csv/nhanes_clean.csv) **NOTE ORIGINAL XPT FILES HAVE BEEN REMOVED FROM FOLDER DUE TO SIZE LIMITIONS OF METIS PROJECTS ON GITHUB. THEREFORE FUNCTIONS IN THIS WORKSHEET PULLING IN XPT DATA WILL NOT WORK.**

    * [Exploratory Data Analysis & Model Development](data_and_modeling/nhanes_bp_model.ipynb) - worksheet where exploratory data analysis and classification models were explored, developed, analyzed, and refined.

    * [Images](data_and_modeling/images) - images of key graphs made in data collection and modeling process

- **Relationship between files**:
    * Files listed above are in order of collection and build from each other, but pickles have been made so that each file can be pulled independent of the other.  All pickles can be found in the [`data_and_modeling/data/pickles` folder](data_and_modeling/data/pickles)

- **Presentation Deck**:
    * [PDF version](Presentation/Presentation_PDF.zip)
    * [Google Slides version](https://docs.google.com/presentation/d/1gitfajWjBjCEeO7Mntv2HIZoynT-rIEznpd1pmIcA1Y/edit?usp=sharing)
    * [PPT version](Presentation/Presentation_PPT.zip)

## SHARING/ACCESS INFORMATION

 - Licenses/restrictions placed on the data: None, open for usage.  Obtained from public government source.

 - Links to other publicly accessible locations of the data: [CDC website](https://wwwn.cdc.gov/nchs/nhanes/continuousnhanes/default.aspx)

 - Was data derived from another source? Yes, [CDC website](https://wwwn.cdc.gov/nchs/nhanes/continuousnhanes/default.aspx)'s National Health and Nutrition Examination Survey results

 - Recommended citation for this dataset: [CDC's National Health and Nutrition Examination Survey](https://wwwn.cdc.gov/nchs/nhanes/continuousnhanes/default.aspx)


## Technologies/Packages Used
  * Jupyter Notebook
  * Python
  * pandas
  * numpy
  * Pickle
  * statsmodels
  * seaborn
  * sklearn
  * matplotlib
  * yellowbrick
  * mlxtend


## Presentation Materials Used
  * Slidesgo - Template
  * freepik - Photos
  * Google Slides


*Centers for Disease Control and Prevention, National Center for Health Statistics. Underlying Cause of Death, 1999–2017. CDC WONDER Online Database. Atlanta, GA: Centers for Disease Control and Prevention; 2018. Accessed January 7, 2019.

** Kirkland EB, Heincelman M, Bishu KG, et. al. Trends in healthcare expenditures among US adults with hypertension: national estimates, 2003-2014. J Am Heart Assoc. 2018;7:e008731.
