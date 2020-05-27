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
