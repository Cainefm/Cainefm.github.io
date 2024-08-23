---
layout: post
title: "The first blog in Github"
subtitle: '利用Github进行代码记录'
date: 2020-12-23 11:12:00-0400
author: "FAN Min"
tags:
  - Life 
  - Rmarkdown
  - Enviornment
---

- [Background / 背景](#bg) 
- [Build a blog in Github](#bb)
- [Jekyll with Rmarkdown / 将Rmarkdown上传至Blog](#R) 


<p id = "bg"></p>
## Background

I am a student, and now working on the phramocoepidimiology studies in the HKU.

Since my team is focusing on the statistical studies with big datasets, in our team, the members are using R or SAS. Now, I spent most of the time on R or python. In the near future, I may use SAS as well. 

In the previous coding life, it is inevitable to have many difficulties, ig. setting up coding enviornment, different codings for analysis, or different statistically models. This blog aims at recording some interesting points about researches or codings.

<p id = "bb"></p>
## How to build such a blog

The blog is build on [GitHub](https://pages.github.com/) and [Jekyll](http://jekyllrb.com/). The Theme is provided by [Hux](Huxpro/huxpro.github.io). 

It is easy to use and build. The process is list:
1. Learn and install **Git**.
2. Register in **Github**.
3. Instal **jekyll**
4. Fork the template in Github. You can check varies [jekyll template ](https://jekyllrb.com/docs/themes/) online.
5. Test locally by :  bundle exec jekyll serve

<p id = "R"></p>
## Rmarkdown with jekyll

The coding in R is quite simple and stratforwards. However, it is desgined for just statistical analysis. So, sometimes it will be better to learn something else to support with it, eg. python, SQL, or JAVA.

In the routine study, Rmarkdown is frequently used rather than markdown. However, it is not so easy to knit the Rmarkdown into the jekyll. The only way I found now is generate `md` files from `Rmarkdown` first.


1.The header in Rmarkdown for transfering into md is 

```
---
title: "This is a test rmarkdown file for Github blog"
author: "FM"
date: '`r Sys.Date()`'
output: 
  md_document:
    variant: markdown_github
---
```

2. copy the md files into the _post and relocate those pic files

3. change the header in the md file

```
---
title: "This is a test rmarkdown file for Github blog"
author: "FM"
header-style: text
categories: rblogging
layout: post
tags: 
 - testing
 - ggplot2
---

```

### Example knited by rmarkdown
#### R basic codes 
``` r
x <- 1:3
y <- 4:6

plot(x,y)
```

![](/img/in-post/rmarkdown-testing/unnamed-chunk-1-1.png)

#### plots by ggplots
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

![](/img/in-post/rmarkdown-testing/unnamed-chunk-1-1.png)

![Old method by md](https://shiring.github.io/blogging/2016/12/04/diy_your_own_blog)

