---
layout: post
title: "This is a test post for my R blog"
header-style: text
categories: rblogging
tags: 
 - testing
 - ggplot2
---

[数据分析语言-R / Statistical Analysis method-R](#R) 
<p id = "R"></p>


test by rmd
===========

## Personal coding
``` r
x <- 1:3
y <- 4:6

plot(x,y)
```

![](/img/in-post/rmarkdown-testing/unnamed-chunk-1-1.png)

## plots by ggplots
``` r
library(ggplot2) # load the packages
ggplot(mpg, aes(displ, hwy)) +
  geom_point(aes(color = class)) +
  geom_smooth(se = FALSE, method = "loess") +
  labs(
    title = "Fuel efficiency generally decreases with engine size",
    subtitle = "Two seaters (sports cars) are an exception because of their light weight",
    caption = "Data from fueleconomy.gov"
  )
```

    ## `geom_smooth()` using formula 'y ~ x'

![](/img/in-post/rmarkdown-testing/unnamed-chunk-1-1.png)
