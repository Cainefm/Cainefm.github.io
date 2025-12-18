---
layout: post
title: A understanding of Immortal time bias when doing a research
date: 2025-01-18 11:59:00-0400
description: "Immortal time bias"
header-style: text
tags: epi
---

# Immortal Time Bias

## Abbreviations

- **Rx**: prescription  
- **Dx**: diagnosis  
- **FU**: follow-up   
- **Index date**: day 0, start of observation

## Key Points

1. **Equal criteria for groups**  
   It is crucial to apply consistent criteria for both the treatment and control groups. For example, the follow-up should start at the same point for both groups to avoid biases.

2. **Define exposure with pre-index information**  
   Defining exposure status based on characteristics after the index date can lead to biases.

## Definition

[Immortal time bias](https://academic-oup-com/aje/article/167/4/492/233064?login=false) is a span of cohort follow-up during which, because of exposure definition, the outcome under study could not occur.

Most of this bias would not be observed in an active comparator new user design. In other words, immortal time bias usually exists in studies that: (1) lack an active comparator, or (2) include prevalent users. It is also common when exploring combination therapy.

## Scenarios Leading to Immortal Time Bias

### 1. Inconsistent follow-up rules between groups

We should use one set of rules, not two different rules, for exposure and control groups. For example, if follow-up starts from treatment initiation in the exposure group but from diagnosis in the control group, this creates bias. [Reference](https://www-bmj-com/content/340/bmj.b5087)

For instance, if patients in the treatment group are required to survive until their first prescription, they may inherently be healthier than those in the untreated group. This can skew results and lead to incorrect conclusions about the effectiveness of treatments.

### 2. Event-based cohort definition

[Event-based cohort definition](https://academic-oup-com/aje/article/167/4/492/233064?login=false) can create traditional immortal time bias. Starting the observation from the diagnosis date in both groups can lead to bias because the time period from follow-up initiation to first prescription is wrongly classified as a treated period.

### 3. Time-based index date definition

[Time-based index date definition](https://academic-oup-com/aje/article/167/4/492/233064?login=false): Using administrative or arbitrary dates as the index date (e.g., database entry date, calendar date) for both groups can cause prevalent user bias or immortal time bias. [Reference](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8087121/)

In this scenario, some patients who experienced the outcome or death before follow-up initiation were excluded, and those drug effects are cumulative effects, which may lead to prevalent user bias.

### 4. Exposure-based cohorts

According to Suissa's description, another type of issue comes from [exposure-based cohorts](https://academic-oup-com/aje/article/167/4/492/233064?login=false). In a [study](https://erj.ersjournals.com/content/20/4/819.short) comparing combination therapies to single therapies, the index date for combination therapies is the time point of the second drug initiation. This requires patients to survive until the initiation of the second drug, which can lead to immortal time bias, as only healthier individuals who can tolerate the first drug will be included.

## Solutions

1. **Random assignment of index date** is inappropriate. However, assigning an index date for the non-user group and matching with the same diagnosis-to-prescription distribution is acceptable. [Reference: five method comparison](https://academic.oup.com/aje/article/162/10/1016/65057?login=false)

2. **Landmark analysis** may fix immortal time bias, but it introduces prevalent user bias.

3. **[Time-varying exposure](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8087121/)**: Classify the immortal time as unexposed prior to the prescription using either a [Poisson model approach or a Cox proportional hazards model with a time-dependent definition for drug exposure](https://academic-oup-com/aje/article/167/4/492/233064?login=false).

4. **[Time-dependent variable](https://academic.oup.com/aje/article/162/10/1016/65057?login=false)**: Start follow-up at diagnosis. A new variable is defined as 0 before the time of first prescription and changes to 1 when the prescription is filled and onward for users. For non-users, the value remains 0 throughout the follow-up.

5. **[Grace period with inverse probability of censoring weights (IPCW)](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8087121/)**

6. **[Time-matched, nested case-control analysis](https://www-bmj-com/content/340/bmj.b5087.long)**

7. **Sequential trials** may be more efficient from a statistical perspective. [Reference: time-to-event analysis](https://doi.org/10.1093/aje/kwv254)
