---
title: "Needs Asssessment SEL Quantiative"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
Grabbing the data for both qual questions
```{r}
#setwd("~/Desktop/QualData")
#rbbcsc = read.csv("RBBCSCStaffSurvey.csv", header = TRUE); head(rbbcsc)

rbbcsc = as.data.frame(rbbcsc)
head(rbbcsc)
rbbcsc = rbbcsc[c("Q2", "Q3", "Q5", "Q6", "Q8", "Q9")]
rbbcsc = rbbcsc[-c(1:2),]
head(rbbcsc1)

colnames(rbbcsc) = c( "SELQualRes", "SELQualBarr", "CCRQualRes", "CCRQualBar", "ASQualRes", "ASQualBar")




########### Now get qualitative data for MCCSC
#setwd("~/Desktop/QualData")
#mccsc = read.csv("MCCSCStaffSurvey.csv", header = TRUE)
head(mccsc)
mccsc = mccsc[c("Q2", "Q3","Q7", "Q8", "Q28", "Q11")]
mccsc = mccsc[-c(1:2),]

# qual questions
head(mccsc)
colnames(mccsc) = c( "SELQualRes", "SELQualBarr", "CCRQualRes", "CCRQualBar", "ASQualRes", "ASQualBar")
both = rbind(mccsc, rbbcsc)
write.csv(both, "both.csv", row.names = FALSE)
```
