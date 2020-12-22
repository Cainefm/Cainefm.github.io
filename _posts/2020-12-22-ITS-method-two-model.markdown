---
title: "Two methods for interrupted time series"
subtitle: '两种不同的ITS方法'
author: "FAN Min"
header-style: text
tags:
  - Methods 
  - R
output:
  html_document:
    df_print: paged
  pdf_document: default
layout: post
---


## 1. Background

The textbook for ITS is the JLB’s tutorial [《Interrupted time series regression for the evaluation of public health interventions: a tutorial》](https://pubmed.ncbi.nlm.nih.gov/27283160-interrupted-time-series-regression-for-the-evaluation-of-public-health-interventions-a-tutorial/). When i dig deeper, i found the ultimate reference was AKD articles in 2002 [《Segmented regression analysis of interrupted time series studies in medication use research》](https://pubmed.ncbi.nlm.nih.gov/12174032-segmented-regression-analysis-of-interrupted-time-series-studies-in-medication-use-research/). But the formulas used in these two papers have a slight difference.

## 2. The JLB's **interaction model**:  
$$
\begin{aligned}
Y \sim {\sf  } \beta_{1}·Time + \beta_{2}·Intervention +\beta_{3}·Time ·Intervention
\end{aligned}
$$   

## 2.1 The dataset lookd like:  
![ ](F:\Projects\PCV-HMRF\0.material\Capture1.PNG)

## 2.2 Interpretation of parameters
![ ](F:\Projects\PCV-HMRF\0.material\Capture3.PNG)


## 3 The AKD's **additional model**:  
$$
\begin{aligned}
Y \sim {\sf  } \beta_{1}·Time + \beta_{2}·Intervention +\beta_{3}·NewTimeAfter  Intervention
\end{aligned}
$$   

## 3.1 The dataset looks like:  
![ ](F:\Projects\PCV-HMRF\0.material\Capture2.PNG)

## 3.2 Interpretation of parameters
![ ](F:\Projects\PCV-HMRF\0.material\Capture4.PNG)



## 4 The difference between two models
```{r,load packages,message=FALSE}
library('ggplot2')
```


### 4.1 Generate a dataset
```{r}
set.seed(999)
testdf <- data.frame(outcome = ceiling(runif(100,1,100)),Time = 1:100, PCV = c(rep(0,70),rep(1,30)),NewTime = c(rep(0,70),1:30))
testdf
```

### 4.2 Model with interaction term
```{r}
test1 <- glm(data=testdf,outcome~Time+PCV+Time*PCV)
coef(test1)
```

### 4.3 Model with additional term
```{r}
test2 <- glm(data=testdf,outcome~Time+PCV+NewTime)
coef(test2)
```

### **Two of the paper both pointed out that the parameter of PCV is the slope changes after intervention. But the numbers are quite different.**  

### **I think one of them is wrong, or we should present it after some adjustments like Dr.Qiu did in the Wechat group. It may be the reason why we always see a level change even we just used the slope-only model in JLB’s method.**  

### **I am not going to say JLB’s method is wrong. I consider that it is not appropriate for the slope-only model, and we should be cautious when interpreting the level’s parameter.** 

### **I am still thinking from the formula perspective. Maybe my point of view is wrong. Pls save me.**


## 5.Slope-only model in two method

```{r}

test3 <- glm(data=testdf,outcome~Time+Time:PCV)
coef(test3)
test4 <- glm(data=testdf,outcome~Time+NewTime)
coef(test4)

predicted_df <- data.frame(outcome_pred = predict(test3,testdf),Time=testdf$Time)
predicted_df2 <- data.frame(outcome_pred = predict(test4,testdf),Time=testdf$Time,NewTime=testdf$NewTime)


ggplot(data = testdf, aes(x = Time, y = outcome)) + 
    geom_point(color='black') +
    geom_line(color='red',data = predicted_df, aes(x=Time, y=outcome_pred))+
    geom_line(color='blue',data = predicted_df2,aes(x=Time,y=outcome_pred))
```

### 5.1. Fixed the previous problem by changing the time

```{r}
test5 <- glm(data=testdf,outcome~Time+NewTime:PCV)
coef(test5)

predicted_df3 <- data.frame(outcome_pred = predict(test5,testdf),Time=testdf$Time,NewTime = testdf$NewTime)

ggplot(data = testdf, aes(x = Time, y = outcome)) + 
    geom_point(color='black') +
    geom_line(color='red',data = predicted_df3, aes(x=Time, y=outcome_pred))



ggplot(data = testdf, aes(x = Time, y = outcome)) + 
    geom_point(color='black') +
    geom_line(color='blue',data = predicted_df2,aes(x=Time,y=outcome_pred))

```

## 6 Apply to our dataset

```{r}
df <- read.csv('Y:/Irene/PCV_ITS/stdpm.csv')
df$NewTime <- c(rep(0,69),1:(166-69))
df
```


```{r}
Interaction.model <- glm(data=df,pneu_ad~time+time:pcv)
coef(Interaction.model)

Interaction.model.adj <- glm(data=df,pneu_ad~time+NewTime:pcv)
coef(Interaction.model.adj)

Additional.model <- glm(data=df,pneu_ad~time+NewTime)
coef(Additional.model)

```

```{r}
predicted_df.in <- data.frame(outcome_pred = predict(Interaction.model,df),Time=df$time)

predicted_df.in.adj <- data.frame(outcome_pred = predict(Interaction.model.adj,df),Time=df$time)

predicted_df.ad <- data.frame(outcome_pred = predict(Additional.model,df),Time=df$time,NewTime=df$NewTime)


ggplot(data = df,aes(x = time, y = pneu_ad)) + 
    geom_point(color='black') +
    geom_line(color='red',data = predicted_df.in, aes(x=Time, y=outcome_pred))+
    ggtitle('JBL model')

ggplot(data = df,aes(x = time, y = pneu_ad)) + 
    geom_point(color='black') +
    geom_line(color='orange',data = predicted_df.in.adj, aes(x=Time, y=outcome_pred))+
    ggtitle('JBL adjusted model')

ggplot(data = df,aes(x = time, y = pneu_ad)) + 
    geom_point(color='black') +
    geom_line(color='blue',data = predicted_df.ad,aes(x=Time,y=outcome_pred))+
    ggtitle('AKD model')
  
```

## I used the count to do the testing. I did not add offset and deseasonalized terms in the model.





```{r}
### 4.3 Model with additional term
testtesttest <- lm(data=testdf[testdf$PCV==0,],outcome~Time)
coef(testtesttest)
```

```{r}
testtesttest <- lm(data=testdf[testdf$PCV==1,],outcome~Time)
coef(testtesttest)
```

