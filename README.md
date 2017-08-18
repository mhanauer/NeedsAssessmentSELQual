---
title: "Needs Asssessment SEL Quantiative"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
Steps: 
1. Get rid of extra data for each 
2. Combine the relevant data
3. Grab demographics gender, degree, type of teacher, race
4. CCR grab all the and transform to numbers
5. Get an overall average value
6. Export the data 

Probably should get general demographics first.  Need to combine them and then 

Get the variables I want for SEL  

SELQuant1 = SEL first survey quantitative question 
SELQualRes = SEL resources question
SELQualBarr = SEL barriers question

Here is for RBBCSC
```{r}
#setwd("~/Desktop/QualData")
#rbbcsc = read.csv("RBBCSCStaffSurvey.csv", header = TRUE); head(rbbcsc)

rbbcsc = rbbcsc[-c(1:7),]; head(rbbcsc, 20)
rbbcsc = rbbcsc[,-c(1:16)]; head(rbbcsc, 20)

rbbcsc = rbbcsc[,-c(38:54)]; head(rbbcsc, 20)
rbbcsc = rbbcsc[,-c(40:44)]; head(rbbcsc, 20)
head(rbbcsc)
rbbcsc = as.data.frame(rbbcsc)

rbbcsc1 = rbbcsc[,1:8]
eth = rbbcsc[c("Q11")]
gender = rbbcsc[c("Q10")]
edu = rbbcsc[c("Q12")]
job = rbbcsc[c("Q15")]
rbbcsc = cbind(rbbcsc1,eth, gender, edu, job)
head(rbbcsc, 20)
# Quantiative, qual questions, and demographics
head(rbbcsc)
colnames(rbbcsc) = c("SELQuant1", "SELQuant2", "SELQuant3", "SELQuant4", "SELQuant5", "SELQuant6", "SELQualRes", "SELQualBarr", "eth", "gender", "edu", "job") 
head(rbbcsc)



```
Now we want to change all of the quantitative variables to these values and then cbind them back.  So first let us create a new data set with only the quantitative values.  Then we need get the other demographic factors and then combine them back.

```{r}
rbbcsc2 = rbbcsc[,1:6] 
rbbcsc2 = apply(rbbcsc2, 2, function(x){ifelse(x == "Strongly agree", 7, x)}); rbbcsc2
rbbcsc2 = as.data.frame(rbbcsc2)
rbbcsc2 = apply(rbbcsc2, 2, function(x){ifelse(x == "Agree", 6, x)}); rbbcsc2
rbbcsc2 = as.data.frame(rbbcsc2)
rbbcsc2 = apply(rbbcsc2, 2, function(x){ifelse(x == "Somewhat agree", 5, x)}); rbbcsc2
rbbcsc2 = as.data.frame(rbbcsc2)
rbbcsc2 = apply(rbbcsc2, 2, function(x){ifelse(x == "Neither agree nor disagree", 4, x)}); 
rbbcsc2 = as.data.frame(rbbcsc2)
rbbcsc2 = apply(rbbcsc2, 2, function(x){ifelse(x == "Somewhat disagree", 3, x)}); rbbcsc2
rbbcsc2 = as.data.frame(rbbcsc2)
rbbcsc2 = apply(rbbcsc2, 2, function(x){ifelse(x == "Disagree", 2, x)}); rbbcsc2
rbbcsc2 = as.data.frame(rbbcsc2)
rbbcsc2 = apply(rbbcsc2, 2, function(x){ifelse(x == "Strongly disagree", 1, x)}); rbbcsc2
rbbcsc2 = as.data.frame(rbbcsc2)
write.csv(rbbcsc2, "rbbcsc2.csv", row.names = FALSE)
rbbcsc2 = read.csv("rbbcsc2.csv", header = TRUE)
head(rbbcsc2)

```
Now MCCSC SEL
```{r}
#setwd("~/Desktop/QualData")
#mccsc = read.csv("MCCSCStaffSurvey.csv", header = TRUE)
head(mccsc)
mccsc = mccsc[-c(1:11),]; head(mccsc, 20)
mccsc1 = mccsc[c("Q1_1", "Q1_2", "Q1_3", "Q1_4", "Q1_5", "Q1_6", "Q2", "Q3")]
eth = mccsc[c("Q30")]
gender = mccsc[c("Q36")]
edu = mccsc[c("Q38")]
job = mccsc[c("Q44")]
mccsc = cbind(mccsc1,eth, gender, edu, job)
head(mccsc, 20)
# Quantiative, qual questions, and demographics
head(mccsc)
colnames(mccsc) = c("SELQuant1", "SELQuant2", "SELQuant3", "SELQuant4", "SELQuant5", "SELQuant6", "SELQualRes", "SELQualBarr", "eth", "gender", "edu", "job") 
head(mccsc)

mccsc2 = mccsc[,1:6] 
mccsc2 = apply(mccsc2, 2, function(x){ifelse(x == "Strongly agree", 7, x)}); mccsc2
mccsc2 = as.data.frame(mccsc2)
mccsc2 = apply(mccsc2, 2, function(x){ifelse(x == "Agree", 6, x)}); mccsc2
mccsc2 = as.data.frame(mccsc2)
mccsc2 = apply(mccsc2, 2, function(x){ifelse(x == "Somewhat agree", 5, x)}); mccsc2
mccsc2 = as.data.frame(mccsc2)
mccsc2 = apply(mccsc2, 2, function(x){ifelse(x == "Neither agree nor disagree", 4, x)}); 
mccsc2 = as.data.frame(mccsc2)
mccsc2 = apply(mccsc2, 2, function(x){ifelse(x == "Somewhat disagree", 3, x)}); mccsc2
mccsc2 = as.data.frame(mccsc2)
mccsc2 = apply(mccsc2, 2, function(x){ifelse(x == "Disagree", 2, x)}); mccsc2
mccsc2 = as.data.frame(mccsc2)
mccsc2 = apply(mccsc2, 2, function(x){ifelse(x == "Strongly disagree", 1, x)}); mccsc2
mccsc2 = as.data.frame(mccsc2)
write.csv(mccsc2, "mccsc2.csv", row.names = FALSE)
mccsc2 = read.csv("mccsc2.csv", header = TRUE)
head(mccsc2)
```
Now we can combine the data and then get an average value across every column.  That could be a bar chart with those means.  These are not the means broken down will do that later.

Means of each questions, means broken down by eth, gender, and job along with the n's for each

Here is for the Overall, Male 
```{r}
# Both just for the quantitative section
bothQuan = as.data.frame(rbind(mccsc2, rbbcsc2))
dim(bothQuan)
bothQuan = na.omit(bothQuan)
bothQuan = as.data.frame(bothQuan)
dim(bothQuan)
meansBoth = apply(bothQuan, 2, mean)
meansBoth

# Both for the different breakdowns.  Gender first
bothAll = as.data.frame(rbind(mccsc, rbbcsc))
bothGender = bothAll[c("SELQuant1", "SELQuant2", "SELQuant3", "SELQuant4", "SELQuant5", "SELQuant6", "gender")]
head(bothGender)
bothGender = na.omit(bothGender)
bothGender = as.data.frame(bothGender)
dim(bothGender)
# I want to get means for each column for the two different genders
bothGenderMale = as.data.frame(bothGender[bothGender$gender == "Male",])
head(bothGenderMale)
bothGenderMale = as.data.frame(bothGenderMale[c(-7)])

bothGenderMale = apply(bothGenderMale, 2, function(x){ifelse(x == "Strongly agree", 7, x)}); bothGenderMale
bothGenderMale = as.data.frame(bothGenderMale)
bothGenderMale = apply(bothGenderMale, 2, function(x){ifelse(x == "Agree", 6, x)}); bothGenderMale
bothGenderMale = as.data.frame(bothGenderMale)
bothGenderMale = apply(bothGenderMale, 2, function(x){ifelse(x == "Somewhat agree", 5, x)}); bothGenderMale
bothGenderMale = as.data.frame(bothGenderMale)
bothGenderMale = apply(bothGenderMale, 2, function(x){ifelse(x == "Neither agree nor disagree", 4, x)}); 
bothGenderMale = as.data.frame(bothGenderMale)
bothGenderMale = apply(bothGenderMale, 2, function(x){ifelse(x == "Somewhat disagree", 3, x)}); bothGenderMale
bothGenderMale = as.data.frame(bothGenderMale)
bothGenderMale = apply(bothGenderMale, 2, function(x){ifelse(x == "Disagree", 2, x)}); bothGenderMale
bothGenderMale = as.data.frame(bothGenderMale)
bothGenderMale = apply(bothGenderMale, 2, function(x){ifelse(x == "Strongly disagree", 1, x)}); bothGenderMale
bothGenderMale = as.data.frame(bothGenderMale)

head(bothGenderMale)
write.csv(bothGenderMale, "bothGenderMale.csv", row.names = FALSE)
bothGenderMale = read.csv("bothGenderMale.csv", header = TRUE)
meansBothGenderMale = apply(bothGenderMale, 2, mean)
meansBothGenderMale


```
Female
```{r}
bothAll = as.data.frame(rbind(mccsc, rbbcsc))
bothGender = apply(bothGender,2, function(x){ifelse(x == "NA", NA, x)})

bothGender = bothAll[c("SELQuant1", "SELQuant2", "SELQuant3", "SELQuant4", "SELQuant5", "SELQuant6", "gender")]
head(bothGender)
bothGender = na.omit(bothGender)
bothGender = apply(bothGender,2, function(x){ifelse(x == "NA", NA, x)})
bothGender = na.omit(bothGender)
bothGender = as.data.frame(bothGender)
dim(bothGender)
# I want to get means for each column for the two different genders
bothGenderFemale = as.data.frame(bothGender[bothGender$gender == "Female",])
head(bothGenderFemale)
bothGenderFemale = as.data.frame(bothGenderFemale[c(-7)])

bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Strongly agree", 7, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Agree", 6, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Somewhat agree", 5, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Neither agree nor disagree", 4, x)}); 
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Somewhat disagree", 3, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Disagree", 2, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Strongly disagree", 1, x)}); 
bothGenderFemale = as.data.frame(bothGenderFemale)
dim(bothGenderFemale)
typeof(bothGenderFemale)
bothGenderFemale = data.frame(bothGenderFemale)
bothGenderFemale = matrix(unlist(bothGenderFemale), ncol= 6)

write.csv(bothGenderFemale, "bothGenderFemale.csv", row.names = FALSE)
bothGenderFemale = read.csv("bothGenderFemale.csv", header = TRUE)
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = na.omit(bothGenderFemale)
typeof(bothGenderFemale)
meansbothGenderFemale = apply(bothGenderFemale, 2, mean)
meansbothGenderFemale
```
This is for White.  
```{r}
bothAll = as.data.frame(rbind(mccsc, rbbcsc))
bothGender = apply(bothGender,2, function(x){ifelse(x == "NA", NA, x)})

bothGender = bothAll[c("SELQuant1", "SELQuant2", "SELQuant3", "SELQuant4", "SELQuant5", "SELQuant6", "eth")]
head(bothGender)
bothGender = na.omit(bothGender)
bothGender = apply(bothGender,2, function(x){ifelse(x == "NA", NA, x)})
bothGender = na.omit(bothGender)
bothGender = as.data.frame(bothGender)
dim(bothGender)
# I want to get means for each column for the two different genders
bothGenderFemale = as.data.frame(bothGender[bothGender$eth == "White",])
head(bothGenderFemale)
bothGenderFemale = as.data.frame(bothGenderFemale[c(-7)])

bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Strongly agree", 7, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Agree", 6, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Somewhat agree", 5, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Neither agree nor disagree", 4, x)}); 
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Somewhat disagree", 3, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Disagree", 2, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Strongly disagree", 1, x)}); 
bothGenderFemale = as.data.frame(bothGenderFemale)
dim(bothGenderFemale)
typeof(bothGenderFemale)
bothGenderFemale = data.frame(bothGenderFemale)
bothGenderFemale = matrix(unlist(bothGenderFemale), ncol= 6)

write.csv(bothGenderFemale, "bothGenderFemale.csv", row.names = FALSE)
bothGenderFemale = read.csv("bothGenderFemale.csv", header = TRUE)
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = na.omit(bothGenderFemale)
typeof(bothGenderFemale)
meansbothGenderFemale = apply(bothGenderFemale, 2, mean)
meansbothGenderFemale
```
This is for non-white
```{r}
bothAll = as.data.frame(rbind(mccsc, rbbcsc))
bothGender = apply(bothGender,2, function(x){ifelse(x == "NA", NA, x)})

bothGender = bothAll[c("SELQuant1", "SELQuant2", "SELQuant3", "SELQuant4", "SELQuant5", "SELQuant6", "eth")]
head(bothGender)
bothGender = na.omit(bothGender)
bothGender = apply(bothGender,2, function(x){ifelse(x == "NA", NA, x)})
bothGender = na.omit(bothGender)
bothGender = as.data.frame(bothGender)
dim(bothGender)
# I want to get means for each column for the two different genders
bothGenderFemale = as.data.frame(bothGender[bothGender$eth != "White",])
head(bothGenderFemale)
bothGenderFemale = as.data.frame(bothGenderFemale[c(-7)])

bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Strongly agree", 7, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Agree", 6, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Somewhat agree", 5, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Neither agree nor disagree", 4, x)}); 
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Somewhat disagree", 3, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Disagree", 2, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Strongly disagree", 1, x)}); 
bothGenderFemale = as.data.frame(bothGenderFemale)
dim(bothGenderFemale)
typeof(bothGenderFemale)
bothGenderFemale = data.frame(bothGenderFemale)
bothGenderFemale = matrix(unlist(bothGenderFemale), ncol= 6)

write.csv(bothGenderFemale, "bothGenderFemale.csv", row.names = FALSE)
bothGenderFemale = read.csv("bothGenderFemale.csv", header = TRUE)
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = na.omit(bothGenderFemale)
typeof(bothGenderFemale)
meansbothGenderFemale = apply(bothGenderFemale, 2, mean)
meansbothGenderFemale
```
This is for a Master's
```{r}
bothAll = as.data.frame(rbind(mccsc, rbbcsc))
bothGender = apply(bothGender,2, function(x){ifelse(x == "NA", NA, x)})
# Change this
bothGender = bothAll[c("SELQuant1", "SELQuant2", "SELQuant3", "SELQuant4", "SELQuant5", "SELQuant6", "edu")]
head(bothGender)
bothGender = na.omit(bothGender)
bothGender = apply(bothGender,2, function(x){ifelse(x == "NA", NA, x)})
bothGender = na.omit(bothGender)
bothGender = as.data.frame(bothGender)
dim(bothGender)
head(bothGender)
# Change this
bothGenderFemale = as.data.frame(bothGender[bothGender$edu == "Master\xe4\xf3\xbbs degree",])
head(bothGenderFemale)
bothGenderFemale = as.data.frame(bothGenderFemale[c(-7)])

bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Strongly agree", 7, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Agree", 6, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Somewhat agree", 5, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Neither agree nor disagree", 4, x)}); 
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Somewhat disagree", 3, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Disagree", 2, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Strongly disagree", 1, x)}); 
bothGenderFemale = as.data.frame(bothGenderFemale)
dim(bothGenderFemale)
typeof(bothGenderFemale)
bothGenderFemale = data.frame(bothGenderFemale)
bothGenderFemale = matrix(unlist(bothGenderFemale), ncol= 6)

write.csv(bothGenderFemale, "bothGenderFemale.csv", row.names = FALSE)
bothGenderFemale = read.csv("bothGenderFemale.csv", header = TRUE)
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = na.omit(bothGenderFemale)
typeof(bothGenderFemale)
meansbothGenderFemale = apply(bothGenderFemale, 2, mean)
meansbothGenderFemale
```
This is for a Bachelors
```{r}
bothAll = as.data.frame(rbind(mccsc, rbbcsc))
bothGender = apply(bothGender,2, function(x){ifelse(x == "NA", NA, x)})
# Change this
bothGender = bothAll[c("SELQuant1", "SELQuant2", "SELQuant3", "SELQuant4", "SELQuant5", "SELQuant6", "edu")]
head(bothGender)
bothGender = na.omit(bothGender)
bothGender = apply(bothGender,2, function(x){ifelse(x == "NA", NA, x)})
bothGender = na.omit(bothGender)
bothGender = as.data.frame(bothGender)
dim(bothGender)
head(bothGender,30)
# Change this
bothGenderFemale = as.data.frame(bothGender[bothGender$edu == "Bachelor\xe4\xf3\xbbs degree",])
head(bothGenderFemale)
bothGenderFemale = as.data.frame(bothGenderFemale[c(-7)])

bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Strongly agree", 7, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Agree", 6, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Somewhat agree", 5, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Neither agree nor disagree", 4, x)}); 
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Somewhat disagree", 3, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Disagree", 2, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Strongly disagree", 1, x)}); 
bothGenderFemale = as.data.frame(bothGenderFemale)
dim(bothGenderFemale)
typeof(bothGenderFemale)
bothGenderFemale = data.frame(bothGenderFemale)
bothGenderFemale = matrix(unlist(bothGenderFemale), ncol= 6)

write.csv(bothGenderFemale, "bothGenderFemale.csv", row.names = FALSE)
bothGenderFemale = read.csv("bothGenderFemale.csv", header = TRUE)
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = na.omit(bothGenderFemale)
typeof(bothGenderFemale)
meansbothGenderFemale = apply(bothGenderFemale, 2, mean)
meansbothGenderFemale
```
This is for primary teachers
```{r}
bothAll = as.data.frame(rbind(mccsc, rbbcsc))
bothGender = apply(bothGender,2, function(x){ifelse(x == "NA", NA, x)})
# Change this
bothGender = bothAll[c("SELQuant1", "SELQuant2", "SELQuant3", "SELQuant4", "SELQuant5", "SELQuant6", "job")]
head(bothGender)
bothGender = na.omit(bothGender)
bothGender = apply(bothGender,2, function(x){ifelse(x == "NA", NA, x)})
bothGender = na.omit(bothGender)
bothGender = as.data.frame(bothGender)
dim(bothGender)
head(bothGender,30)
# Change this
bothGenderFemale = as.data.frame(bothGender[bothGender$job == "Primary school teacher",])
head(bothGenderFemale)
bothGenderFemale = as.data.frame(bothGenderFemale[c(-7)])

bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Strongly agree", 7, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Agree", 6, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Somewhat agree", 5, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Neither agree nor disagree", 4, x)}); 
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Somewhat disagree", 3, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Disagree", 2, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Strongly disagree", 1, x)}); 
bothGenderFemale = as.data.frame(bothGenderFemale)
dim(bothGenderFemale)
typeof(bothGenderFemale)
bothGenderFemale = data.frame(bothGenderFemale)
bothGenderFemale = matrix(unlist(bothGenderFemale), ncol= 6)

write.csv(bothGenderFemale, "bothGenderFemale.csv", row.names = FALSE)
bothGenderFemale = read.csv("bothGenderFemale.csv", header = TRUE)
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = na.omit(bothGenderFemale)
typeof(bothGenderFemale)
meansbothGenderFemale = apply(bothGenderFemale, 2, mean)
meansbothGenderFemale
```
This is for secondary teachers
```{r}
bothAll = as.data.frame(rbind(mccsc, rbbcsc))
bothGender = apply(bothGender,2, function(x){ifelse(x == "NA", NA, x)})
# Change this
bothGender = bothAll[c("SELQuant1", "SELQuant2", "SELQuant3", "SELQuant4", "SELQuant5", "SELQuant6", "job")]
head(bothGender)
bothGender = na.omit(bothGender)
bothGender = apply(bothGender,2, function(x){ifelse(x == "NA", NA, x)})
bothGender = na.omit(bothGender)
bothGender = as.data.frame(bothGender)
dim(bothGender)
head(bothGender,30)
# Change this
bothGenderFemale = as.data.frame(bothGender[bothGender$job == "Secondary school teacher",])
head(bothGenderFemale)
bothGenderFemale = as.data.frame(bothGenderFemale[c(-7)])

bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Strongly agree", 7, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Agree", 6, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Somewhat agree", 5, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Neither agree nor disagree", 4, x)}); 
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Somewhat disagree", 3, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Disagree", 2, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Strongly disagree", 1, x)}); 
bothGenderFemale = as.data.frame(bothGenderFemale)
dim(bothGenderFemale)
typeof(bothGenderFemale)
bothGenderFemale = data.frame(bothGenderFemale)
bothGenderFemale = matrix(unlist(bothGenderFemale), ncol= 6)

write.csv(bothGenderFemale, "bothGenderFemale.csv", row.names = FALSE)
bothGenderFemale = read.csv("bothGenderFemale.csv", header = TRUE)
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = na.omit(bothGenderFemale)
typeof(bothGenderFemale)
meansbothGenderFemale = apply(bothGenderFemale, 2, mean)
meansbothGenderFemale
```
This is for Administrator
```{r}
bothAll = as.data.frame(rbind(mccsc, rbbcsc))
bothGender = apply(bothGender,2, function(x){ifelse(x == "NA", NA, x)})
# Change this
bothGender = bothAll[c("SELQuant1", "SELQuant2", "SELQuant3", "SELQuant4", "SELQuant5", "SELQuant6", "job")]
head(bothGender)
bothGender = na.omit(bothGender)
bothGender = apply(bothGender,2, function(x){ifelse(x == "NA", NA, x)})
bothGender = na.omit(bothGender)
bothGender = as.data.frame(bothGender)
dim(bothGender)
head(bothGender,30)
# Change this
bothGenderFemale = as.data.frame(bothGender[bothGender$job == "Administrator",])
head(bothGenderFemale)
bothGenderFemale = as.data.frame(bothGenderFemale[c(-7)])

bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Strongly agree", 7, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Agree", 6, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Somewhat agree", 5, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Neither agree nor disagree", 4, x)}); 
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Somewhat disagree", 3, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Disagree", 2, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Strongly disagree", 1, x)}); 
bothGenderFemale = as.data.frame(bothGenderFemale)
dim(bothGenderFemale)
typeof(bothGenderFemale)
bothGenderFemale = data.frame(bothGenderFemale)
bothGenderFemale = matrix(unlist(bothGenderFemale), ncol= 6)

write.csv(bothGenderFemale, "bothGenderFemale.csv", row.names = FALSE)
bothGenderFemale = read.csv("bothGenderFemale.csv", header = TRUE)
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = na.omit(bothGenderFemale)
typeof(bothGenderFemale)
meansbothGenderFemale = apply(bothGenderFemale, 2, mean)
meansbothGenderFemale
```
This is for Special Education teacher
```{r}
bothAll = as.data.frame(rbind(mccsc, rbbcsc))
bothGender = apply(bothGender,2, function(x){ifelse(x == "NA", NA, x)})
# Change this
bothGender = bothAll[c("SELQuant1", "SELQuant2", "SELQuant3", "SELQuant4", "SELQuant5", "SELQuant6", "job")]
head(bothGender)
bothGender = na.omit(bothGender)
bothGender = apply(bothGender,2, function(x){ifelse(x == "NA", NA, x)})
bothGender = na.omit(bothGender)
bothGender = as.data.frame(bothGender)
dim(bothGender)
head(bothGender,30)
# Change this
bothGenderFemale = as.data.frame(bothGender[bothGender$job == "Special Education teacher",])
head(bothGenderFemale)
bothGenderFemale = as.data.frame(bothGenderFemale[c(-7)])

bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Strongly agree", 7, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Agree", 6, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Somewhat agree", 5, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Neither agree nor disagree", 4, x)}); 
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Somewhat disagree", 3, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Disagree", 2, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Strongly disagree", 1, x)}); 
bothGenderFemale = as.data.frame(bothGenderFemale)
dim(bothGenderFemale)
typeof(bothGenderFemale)
bothGenderFemale = data.frame(bothGenderFemale)
bothGenderFemale = matrix(unlist(bothGenderFemale), ncol= 6)

write.csv(bothGenderFemale, "bothGenderFemale.csv", row.names = FALSE)
bothGenderFemale = read.csv("bothGenderFemale.csv", header = TRUE)
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = na.omit(bothGenderFemale)
typeof(bothGenderFemale)
meansbothGenderFemale = apply(bothGenderFemale, 2, mean)
meansbothGenderFemale
```
This is for Principal
```{r}
bothAll = as.data.frame(rbind(mccsc, rbbcsc))
bothGender = apply(bothGender,2, function(x){ifelse(x == "NA", NA, x)})
# Change this
bothGender = bothAll[c("SELQuant1", "SELQuant2", "SELQuant3", "SELQuant4", "SELQuant5", "SELQuant6", "job")]
head(bothGender)
bothGender = na.omit(bothGender)
bothGender = apply(bothGender,2, function(x){ifelse(x == "NA", NA, x)})
bothGender = na.omit(bothGender)
bothGender = as.data.frame(bothGender)
dim(bothGender)
head(bothGender,30)
# Change this
bothGenderFemale = as.data.frame(bothGender[bothGender$job == "Principal",])
head(bothGenderFemale)
bothGenderFemale = as.data.frame(bothGenderFemale[c(-7)])

bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Strongly agree", 7, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Agree", 6, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Somewhat agree", 5, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Neither agree nor disagree", 4, x)}); 
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Somewhat disagree", 3, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Disagree", 2, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Strongly disagree", 1, x)}); 
bothGenderFemale = as.data.frame(bothGenderFemale)
dim(bothGenderFemale)
typeof(bothGenderFemale)
bothGenderFemale = data.frame(bothGenderFemale)
bothGenderFemale = matrix(unlist(bothGenderFemale), ncol= 6)

write.csv(bothGenderFemale, "bothGenderFemale.csv", row.names = FALSE)
bothGenderFemale = read.csv("bothGenderFemale.csv", header = TRUE)
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = na.omit(bothGenderFemale)
typeof(bothGenderFemale)
meansbothGenderFemale = apply(bothGenderFemale, 2, mean)
meansbothGenderFemale
```
This is for School Counselor
```{r}
bothAll = as.data.frame(rbind(mccsc, rbbcsc))
bothGender = apply(bothGender,2, function(x){ifelse(x == "NA", NA, x)})
# Change this
bothGender = bothAll[c("SELQuant1", "SELQuant2", "SELQuant3", "SELQuant4", "SELQuant5", "SELQuant6", "job")]
head(bothGender)
bothGender = na.omit(bothGender)
bothGender = apply(bothGender,2, function(x){ifelse(x == "NA", NA, x)})
bothGender = na.omit(bothGender)
bothGender = as.data.frame(bothGender)
dim(bothGender)
head(bothGender,30)
# Change this
bothGenderFemale = as.data.frame(bothGender[bothGender$job == "School Counselor",])
head(bothGenderFemale)
bothGenderFemale = as.data.frame(bothGenderFemale[c(-7)])

bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Strongly agree", 7, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Agree", 6, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Somewhat agree", 5, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Neither agree nor disagree", 4, x)}); 
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Somewhat disagree", 3, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Disagree", 2, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Strongly disagree", 1, x)}); 
bothGenderFemale = as.data.frame(bothGenderFemale)
dim(bothGenderFemale)
typeof(bothGenderFemale)
bothGenderFemale = data.frame(bothGenderFemale)
bothGenderFemale = matrix(unlist(bothGenderFemale), ncol= 6)

write.csv(bothGenderFemale, "bothGenderFemale.csv", row.names = FALSE)
bothGenderFemale = read.csv("bothGenderFemale.csv", header = TRUE)
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = na.omit(bothGenderFemale)
typeof(bothGenderFemale)
meansbothGenderFemale = apply(bothGenderFemale, 2, mean)
meansbothGenderFemale
```
This is for School Social Worker 
```{r}
bothAll = as.data.frame(rbind(mccsc, rbbcsc))
bothGender = apply(bothGender,2, function(x){ifelse(x == "NA", NA, x)})
# Change this
bothGender = bothAll[c("SELQuant1", "SELQuant2", "SELQuant3", "SELQuant4", "SELQuant5", "SELQuant6", "job")]
head(bothGender)
bothGender = na.omit(bothGender)
bothGender = apply(bothGender,2, function(x){ifelse(x == "NA", NA, x)})
bothGender = na.omit(bothGender)
bothGender = as.data.frame(bothGender)
dim(bothGender)
head(bothGender,30)
# Change this
bothGenderFemale = as.data.frame(bothGender[bothGender$job == "School Social Worker ",])
head(bothGenderFemale)
bothGenderFemale = as.data.frame(bothGenderFemale[c(-7)])

bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Strongly agree", 7, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Agree", 6, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Somewhat agree", 5, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Neither agree nor disagree", 4, x)}); 
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Somewhat disagree", 3, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Disagree", 2, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Strongly disagree", 1, x)}); 
bothGenderFemale = as.data.frame(bothGenderFemale)
dim(bothGenderFemale)
typeof(bothGenderFemale)
bothGenderFemale = data.frame(bothGenderFemale)
bothGenderFemale = matrix(unlist(bothGenderFemale), ncol= 6)

write.csv(bothGenderFemale, "bothGenderFemale.csv", row.names = FALSE)
bothGenderFemale = read.csv("bothGenderFemale.csv", header = TRUE)
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = na.omit(bothGenderFemale)
typeof(bothGenderFemale)
meansbothGenderFemale = apply(bothGenderFemale, 2, mean)
meansbothGenderFemale
```
This is for School Social Worker
```{r}
bothAll = as.data.frame(rbind(mccsc, rbbcsc))
bothGender = apply(bothGender,2, function(x){ifelse(x == "NA", NA, x)})
# Change this
bothGender = bothAll[c("SELQuant1", "SELQuant2", "SELQuant3", "SELQuant4", "SELQuant5", "SELQuant6", "job")]
head(bothGender)
bothGender = na.omit(bothGender)
bothGender = apply(bothGender,2, function(x){ifelse(x == "NA", NA, x)})
bothGender = na.omit(bothGender)
bothGender = as.data.frame(bothGender)
dim(bothGender)
head(bothGender,30)
# Change this
bothGenderFemale = as.data.frame(bothGender[bothGender$job == "School Counselor",])
head(bothGenderFemale)
bothGenderFemale = as.data.frame(bothGenderFemale[c(-7)])

bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Strongly agree", 7, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Agree", 6, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Somewhat agree", 5, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Neither agree nor disagree", 4, x)}); 
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Somewhat disagree", 3, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Disagree", 2, x)}); bothGenderFemale
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = apply(bothGenderFemale, 2, function(x){ifelse(x == "Strongly disagree", 1, x)}); 
bothGenderFemale = as.data.frame(bothGenderFemale)
dim(bothGenderFemale)
typeof(bothGenderFemale)
bothGenderFemale = data.frame(bothGenderFemale)
bothGenderFemale = matrix(unlist(bothGenderFemale), ncol= 6)

write.csv(bothGenderFemale, "bothGenderFemale.csv", row.names = FALSE)
bothGenderFemale = read.csv("bothGenderFemale.csv", header = TRUE)
bothGenderFemale = as.data.frame(bothGenderFemale)
bothGenderFemale = na.omit(bothGenderFemale)
typeof(bothGenderFemale)
meansbothGenderFemale = apply(bothGenderFemale, 2, mean)
meansbothGenderFemale
```

