# Company_Absenteeism_Problem
Predicting company absenteeism while integrating Python, SQL, Tableau (Python)



## Defining the Problem
This project will address Absenteeism at a company during a work day.

`Absenteeism`: Absence form work during normal working hours, resulting in temporary incapacity to execute regular working activity

* Higher competitveness --> Increased pressure
* Unachievable business goals --> Raised stress levels
* Elevated risk of becoming unemployed --> Raised stress levels

**Why would a business care?** 
To explore whether a person presenting certain characteristics is expected to be away from work at some point in time or not - and for how many hours.

**The features considered in the analysis**
* 28 Reasons for absence (These will be broken down into 4 groups - Explained later)
* Date of absence
* Transportation (Costs related to business travel)
* Distance to work (Measured in kilometers)
* Age of employee
* Daily work load average (Measured in minutes)
* Body Mass Index
* Education (Categorical variable representing different levels of education)
* Number of children
* Number of pets
* Absenteeism in hours


## Preprocessing
`Absenteeism Time in hours` is the dependent variable to predict absenteeism from work (the goal)

#### Removed irrelevant data
Removed columns containing irrelevant data (i.e. `ID` column)

#### `Reason for Absence` Analysis
Values here represent categories that are equally meaningful. 
* Refer to Feature Descriptions

* Note: We can be certain than an individual has been absent from work because of only one distinct reason

`Reason 0` is for unknow cases when a person is absent from work. If a person has been absent due to reason 0, this means they have been away from work for an unknown reason. Hence, this column acts like the baseline, and all the rest are represented in comparison to this.

To avoid issues with `multicollinearity`, we must remove one column with dummy variables. To preserve the logic of our analysis, this will be the column that stands for reason 0.

Grouping dummy varaibles from `reason_columns` in this regresison analysis is `classification` - See Feature Desciptions table (4 groups)

* Group 1: Related to Diseases/illnesses
* Group 2: Related to birth/pregnancy
* Group 3: Related to poisoining or signs not otherwise categorized
* Group 4: "Light" reasons, i.e. Dental check-up

**Modified `Date` and other features to prepare dataframe for machine learning

## Machine Learning
**Created a logistic regression to predict absenteeism**

#### Created the target
Logistic regression is a type of Classification. The 2 classes in the problem are: 

* 1. Moderately absent
* 2. Excessively absent

We will take the median value of the 'Absenteeism Time in Hours' to use as the cut-off line.

**What are the classes in our problem?**
* 1. Moderately absent (<= 3 hours)... We will give this class a value of `0`
* 2. Excessively absent (>= 4 hours)... We will give this class a value of `1`

In supervised learning, the 0s and 1s are the `Targets` (what we are trying to predict)

Using the median as a cut-off line is 'numerically stable and rigid' and has implicitly balanced the dataset. This will prevent the model from learning to output only 0s or only 1s.

Around ~46% of the targets are 1s, ~54% of targets are 0s. Meaning, out dataset is balanced (falls within 60-40 split for logistic regression).

#### Standardize the data


#### Split data into train & test sets and shuffle the data
This shows, the inputs contain 560 observations along 14 features, while the targets are a vector of length 560 for the training set. As for the test sets, the inputs contain 140 observations along 14 features, and a single target array of length 140. 

80:20 Train-test split

#### Assessing model accuracy
Based on the data used, the model is able to classify ~78% (.775) of the observations correctly, our train accuracy

#### Interpreting the model coefficients

INSERT TABLE HERE!!!

The further away form 0 a coefficient is, the more important it is.
We see that the features with the highest coefficients (most important) are at the top. `Reason_3`, `Reason_1`, `Reason_3`, `Reason_4`, `Transportation Expense`, etc.

A reminder that these "Reason" are as follows:
* Poisoning
* Various diseases
* Pregancy and birth
* Light diseases

The features with the smallest impact are `Month Value`, `Daily Work Load Average`, `Distance to Work`, and `Day of the Week`. We can consider dropping theses features.

To look at one of the negative coefficients, i.e. `Pets`, the odds are 1-0.759676 = 24% lower than the base model (no pet)

** Reminder that we used Reason_0 = No reason is given, as the baseline model

** The `Intercept` (Bias) 'calibrates' the model

#### Test the model
Based on the data the model has never seen before (test set), in ~74% (.7357) of the cased, the model will predict (correctly) if the person is going to be excessively absent.

## Integrate Data into MySQL Workbench

INSERT MySQL WORKBENCH LOGO

## Visualize Insights for the Business in Tableau

INSERT TABLEAU LOGO



