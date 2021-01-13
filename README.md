# Exploring_the_BRFSS

Exploring the BRFSS data
Setup
Load packages
library(ggplot2)
library(dplyr)
Load data
load('/Users/ajitsingh/Downloads/4tiY2fqCQa-YmNn6gnGvzQ_1e7320c30a6f4b27894a54e2de50a805_brfss2013.RData')
Part 1: Data
This study can be generalized to people who are above 18, are not institutionalized, and are able to afford a phone. There was random sampling used, as people were called at random. However, the study only questioned those who are not in an institute, are above 18, and possess a phone, so some demographics of the population are not represented. This study cannot establish causality, as random assignment was not used. This is not an experiment, so random assignment cannot occur, and an observational study such as this one can only establish correlations, not causation.

Part 2: Research questions
Research question 1: Anxiety and depression are very debilitating disorders and may stop people from being as productive as they can be. This is an important question because it may stop people from earning as much as they can and from living a fulfilling life. It can also help find clinical treatments and what social services need to be strengthened. This study can be generalized to people who are not institutionalized, can afford a phone, and are above 18. How correlated is mental health with depression and anxiety?

Research question 2: An individual with poor mental health and not enough sleep is not likely to be as productive as they may be otherwise. This is an important question because it hampers people’s ability to make a living and also hampers a person’s ability to live a fulfilling life. The answer to this question can help discover new clinical treatments and what social services need to be strengthened. This study can be generalized to people who are not institutionalized, can afford a phone, and are above 18. How correlated is overall poor health with mental health and sleep time?

Research question 3: A person not able to work affects their employer, society as less taxes are collected, the individual’s dependents, and the individual themselves. It is therefore an important question of how much mental health issues affect people’s working lives. The answer to this question can indicate what social services need to be created or strengthened. This study can be generalized to people who are not institutionalized, can afford a phone, and are above 18. How correlated are missing work and mental health?

Part 3: Exploratory data analysis
Research question 1:

 mentalhealthandstress<-select(brfss2013, qlstres2, menthlth)
 excludedmentalhealthandstress<-mentalhealthandstress[mentalhealthandstress$menthlth<30,]
 ggplot(excludedmentalhealthandstress, aes(x=menthlth, y = qlstres2))+geom_jitter()+ggtitle('Mental Health vs Stress')+ labs(y="How Many Days Felt Anxious In Past 30 Days", x = "Number Of Days Mental Health Not Good")
## Warning: Removed 465814 rows containing missing values (geom_point).


 mentalhealthandanxiety<-select(brfss2013, qlmentl2, menthlth)
 excludedmentalhealthandanxiety<-mentalhealthandanxiety[mentalhealthandanxiety$menthlth<30,]
 ggplot(excludedmentalhealthandanxiety, aes(x=menthlth, y = qlmentl2))+geom_jitter()+ggtitle('Mental Health vs Depression')+ labs(y="How Many Days Felt Depressed In Past 30 Days", x = "Number Of Days Mental Health Not Good")
## Warning: Removed 465808 rows containing missing values (geom_point).


In the code above, mentalhealthandstress and mentalhealthandanxiety select the data used in the research question. Because in the question only 30 days at most can be spent having bad mental health, menthlth<31. This processed data is saved in excludedmentalhealthandstress and excludedmentalhealthandanxiety. Then, the processed data is charted out. If there is a correlation between two variables, when the variables are charted together there should be a straight line that appears. The amount of scatter and whether a line exists determines the strength of the association. In the Mental Health vs Stress chart there is a correlation in the number of days that mental health is not good in the past 30 days vs the number of days the individual felt anxious in the past 30 days. It is a weak correlation. There is a line forming through the center of the chart that illustrates this correlation. This can be generalized to people who are not institutionalized, are above 18, and can afford a phone.
In the Mental Health vs Depression chart there is a correlation between the number of days in the last 30 days that mental health is not good vs the number of days an individual feels depressed for the last 30 days. This is shown in the chart Mental Health vs Depression. There is a line forming through the center of the graph that shows a weak correlation. This can be generalized to people who are not institutionalized, are above 18, and can afford a phone.
In conclusion, there is an association between the variables mental health and depression, and mental health and stress.

summary(excludedmentalhealthandstress)
##     qlstres2         menthlth     
##  Min.   : 0.0     Min.   : 0.000  
##  1st Qu.: 0.0     1st Qu.: 0.000  
##  Median : 0.0     Median : 0.000  
##  Mean   : 4.8     Mean   : 1.887  
##  3rd Qu.: 5.0     3rd Qu.: 1.000  
##  Max.   :30.0     Max.   :29.000  
##  NA's   :465814   NA's   :8627
This is the summary of the data used to make the mental health and stress chart.

summary(excludedmentalhealthandanxiety)
##     qlmentl2         menthlth     
##  Min.   : 0.0     Min.   : 0.000  
##  1st Qu.: 0.0     1st Qu.: 0.000  
##  Median : 0.0     Median : 0.000  
##  Mean   : 3.3     Mean   : 1.887  
##  3rd Qu.: 3.0     3rd Qu.: 1.000  
##  Max.   :30.0     Max.   :29.000  
##  NA's   :465808   NA's   :8627
This is the summary of the data used to make the mental health and anxiety chart.

Research question 2:

mentalandpoorhealth<-select(brfss2013, menthlth, poorhlth)
excludedmentalandpoorhealth<-mentalandpoorhealth[mentalandpoorhealth$menthlth<31,]
ggplot(excludedmentalandpoorhealth, aes(x=menthlth, y=poorhlth))+geom_jitter()+ggtitle('Mental Health vs Poor Health')+ labs(y="Poor Physical Or Mental Health", x = "Number Of Days Mental Health Not Good")
## Warning: Removed 249788 rows containing missing values (geom_point).


sleptimeandpoorhealth<-select(brfss2013, sleptim1, poorhlth)
excludedpoorhlthandsleptim1<-sleptimeandpoorhealth[sleptimeandpoorhealth$poorhlth<31,]
ggplot(excludedpoorhlthandsleptim1, aes(x=sleptim1, y= poorhlth))+geom_jitter()+ggtitle('Sleep Time vs Poor Health')+ labs(y="Poor Physical Or Mental Health", x = "How Much Time Do You Sleep")
## Warning: Removed 247066 rows containing missing values (geom_point).


In the code above, mentalandpoorhealth and sleptimeandpoorhealth select the data to be used in the code. excludedmentalandpoorhealth and excludedpoorhlthandsleptim1 clean the data by setting mentalhealth and poorhealth to less than 31, as there are 30 days asked in the question. Then, the excludedmentalandpoorhealth and excludedpoorhlhtandsleptim1 are used to chart the data. In the Mental Health vs Poor Health chart there is a correlation between the number of days mental health is not good and the poor physical or mental health variables as illustrated by the line formed in the center of the chart. This can be generalized to people who are not institutionalized, are above 18, and can afford a phone.
In the Sleep Time vs Poor Health chart there is no linear correlation between the variables poor physical or mental health and the time the individual sleeps. This is illustrated by the fact that no line has formed. This can be generalized to people who are not institutionalized, are above 18, and can afford a phone.
In conclusion, there is some type of association between poor health and mental health. No association exists between sleep time and poor health.

summary(excludedmentalandpoorhealth)
##     menthlth         poorhlth     
##  Min.   : 0.000   Min.   : 0.00   
##  1st Qu.: 0.000   1st Qu.: 0.00   
##  Median : 0.000   Median : 0.00   
##  Mean   : 3.372   Mean   : 5.28   
##  3rd Qu.: 2.000   3rd Qu.: 5.00   
##  Max.   :30.000   Max.   :30.00   
##  NA's   :8627     NA's   :249788
This is the summary data for the mental and poor health chart.

summary(excludedpoorhlthandsleptim1)
##     sleptim1         poorhlth     
##  Min.   : 0.00    Min.   : 0.00   
##  1st Qu.: 6.00    1st Qu.: 0.00   
##  Median : 7.00    Median : 0.00   
##  Mean   : 6.92    Mean   : 5.27   
##  3rd Qu.: 8.00    3rd Qu.: 5.00   
##  Max.   :24.00    Max.   :30.00   
##  NA's   :247066   NA's   :243153
This is the summary data for the poor health and sleeptime chart.

Research question 3:

 mentalhealthandwork<-select(brfss2013, misnowrk, menthlth)
 excludedmentalhealthandwork<-mentalhealthandwork[mentalhealthandwork$menthlth<31,]
 ggplot(excludedmentalhealthandwork, aes(x=menthlth, y = misnowrk))+geom_jitter()+ggtitle('Mental Health vs Missing Work')+ labs(y="Emotional Problem Kept You From Doing Work Past 30 Days", x = "Number Of Days Mental Health Not Good")
## Warning: Removed 456327 rows containing missing values (geom_point).


In the code above, mentalhealthandwork selects the data to be used in the code. excludedmentalhealthandwork clean the data by setting mentalhealth to less than 31, as there are 30 days asked in the question. Then, the excludedmentalhealthandwork and is used to chart the data. In the Mental Health vs Missing Work chart, there is no linear correlation between the number of days mental health not good and emotional problem kept you from doing work for the past 30 days. This is illustrated by no line existing on the chart. This can be generalized to people who are not institutionalized, are above 18, and can afford a phone.

summary(excludedmentalhealthandwork)
##     misnowrk         menthlth     
##  Min.   : 0       Min.   : 0.000  
##  1st Qu.: 0       1st Qu.: 0.000  
##  Median : 0       Median : 0.000  
##  Mean   : 1       Mean   : 3.372  
##  3rd Qu.: 0       3rd Qu.: 2.000  
##  Max.   :30       Max.   :30.000  
##  NA's   :456327   NA's   :8627
This is the summary for the mental health and work plot.
