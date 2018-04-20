# No Show Medical Appointment Project
A person makes a doctor appointment, receives all the instructions and it’s a no-show.

### Who/What to blame?

### What is a no-show?
Basically, it’s a non-attending person who neither uses nor cancels their reservation.

### The problem is…
People have no idea of the scale of this problem.
A recent survey concluded that as many as 42% of patients skip their appointments.
            
### “An appointment missed by you is an appointment missed by two.”

A missed appointment is more than just a missed opportunity. When a patient doesn’t show up on time, it also affects people who could’ve been treated instead of that patient.

Visitors, doctors, and even hospital administration…they’re all affected.

### Finding Reasons
### Different Surveys using different datasets came up with some influencing factors :
Financial Reasons

Discouraged by long Hospital wait time 

Poor Medical Literacy

Anxiety

Transportation

### The data we had
Gender & Age

Signs of Hypertension, Diabetes & Alcoholism

Appointment date and the date of Scheduling

Medical Insurance 

SMS Notification

![data](https://user-images.githubusercontent.com/35349226/34854017-0bfba464-f705-11e7-95e3-1a866f55cc07.png)

![image](https://user-images.githubusercontent.com/35349226/34854194-2a97061a-f706-11e7-819e-053d60be1cb0.png)


### Data Struggles
Irrelevant Columns – Patient & Appointment ID

Date & Time Stamps – Always an issue!!

Outliers in Age – 0, negative and above 100

Junk Rows – Handicap Row values

Appointment & Schedule data Difference- Is it Relevant?

Bias Data – 80:20 Show : No-Show

Balancing the data

### Clean it UP!!!
Remove Patient ID, Appointment ID columns

Cleaning up date columns

Extracting date month and year from appointment and schedule day columns

Calculate difference between Scheduled and Appointment dates

Creating Balanced Data

removing negative values and values >1

Convert columns to factors

## Real World Data Set is not your friend!

Bias in Distribution: 85,000 v/s 21,000 Rows

![image](https://user-images.githubusercontent.com/35349226/34854140-d52365c0-f705-11e7-9ac1-cfe6c16773c9.png)


### Brief overview of techniques used

As this dataset is about predicting Show/No Show of a Customer at hospital, so it’s a classification problem.

We performed classification techniques:

Logistic Regression

Naïve Bayes

Cross validation

Ridge, Lasso and PCA for dimensionality reduction


### Lasso Results

![image](https://user-images.githubusercontent.com/35349226/34854331-1a1947ac-f707-11e7-9f91-3ea95f89fbbb.png)

Most Significant columns- Age, Scholarship and SMS_Received

Insignificant – Gender, Diabetes, HandCap, Hipertension, Alcoholism


### Ridge Regression

Performed similar steps for Ridge regression

Change alpha to 0

cv.out <- cv.glmnet(x1, y, alpha=0, nlambda=100, lambda.min.ratio=0.0001)

predict(ridge.mod, s=best.lambda, type="coefficients")[1:9, ]

Does not push coefficients to 0

Ridge says Age is insignificant and Alcoholism is significant 

Significant columns – Alcoholism, SMS_Received, Scholarship

Got best results using columns identified by Lasso.

![image](https://user-images.githubusercontent.com/35349226/34854368-566dfde2-f707-11e7-8987-dd55a3bc5c70.png)

### Logistic Regression

Performed on most significant columns identified by Lasso

Test : Train datasets = 50 :50

Accuracy – 57.9%

Confusion Matrix:

![image](https://user-images.githubusercontent.com/35349226/34854401-7fa5c60e-f707-11e7-933d-8a292d1e6093.png)

### Naïve Bayes Procedure

Performed on most significant columns identified by Lasso

Test : Train datasets = 50 :50

Accuracy – 58%

![image](https://user-images.githubusercontent.com/35349226/34854444-c02a8ab6-f707-11e7-865c-4ea3cf9cd4fe.png)

### Cross Validation

Performed 10-fold cross validation on Logistic and Naïve Bayes procedure

#### Naïve Bayes:

Accuracy : Between 56 to 58

Mean accuracy – 57.96%

#### Logistic Regression:
Accuracy : Between 55 to 58

Mean accuracy – 56.95%

### Principal Component Analysis	
Created 9 Principal components

Libraries used: FactoMineR, factoextra

Columns used – 

Gender, Age, Scholarship, Hypertension, Diabetes, Alcoholism

63.4% variance is explained by first 4 PCA components

![image](https://user-images.githubusercontent.com/35349226/34854526-350806b0-f708-11e7-85ef-7bf55afffb76.png)

### Conclusions

Naïve Bayes procedure was slightly better than Logistic Regression as it gave us better accuracy

Feature Elimination was done better by Lasso when compared to Ridge for this dataset

Dataset could have more relevant features that would have helped increasing accuracy (ex: Disease records, Work schedule of patients, new or retuning patient, location from hospital etc.)
