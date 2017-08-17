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
setwd("~/Desktop/QualData")
rbbcsc = read.csv("RBBCSCStaffSurvey.csv", header = TRUE); head(rbbcsc)

rbbcsc = rbbcscTest[-c(1:11),]; head(rbbcsc, 20)
rbbcsc = rbbcsc[,-c(1:16)]; head(rbbcsc, 20)

rbbcsc = rbbcsc[,-c(38:54)]; head(rbbcsc, 20)
rbbcsc = rbbcsc[,-c(40:44)]; head(rbbcsc, 20)
head(rbbcsc)
rbbcsc = as.data.frame(rbbcsc)

rbbcsc = rbbcsc[,7:8]
head(rbbcsc1)

colnames(rbbcsc) = c( "SELQualRes", "SELQualBarr")
write.csv(rbbcsc, "rbbcsc.csv", row.names = FALSE)
rbbcsc = read.csv("rbbcsc.csv", header = TRUE, na.strings = "")
rbbcsc = na.omit(rbbcsc)
head(rbbcsc)
dim(rbbcsc)
########### Now get qualitative data for MCCSC
setwd("~/Desktop/QualData")
mccsc = read.csv("MCCSCStaffSurvey.csv", header = TRUE)

mccsc = mccsc[c("Q2", "Q3")]
head(mccsc, 20)
# qual questions
head(mccsc)
colnames(mccsc) = c("SELQualRes", "SELQualBarr") 
head(mccsc)
write.csv(mccsc, "mccsc.csv", row.names = FALSE)
mccsc = read.csv("mccsc.csv", header = TRUE, na.strings = "")
mccsc = na.omit(mccsc)
head(mccsc)
dim(mccsc)

both = rbind(mccsc, rbbcsc)
```
Now we have the data and need to make the word clouds.
```{r}

```

