---
title: "Reading THIN"
subtitle: 'THIN 数据读取'
author: "FAN Min"
header-style: text
tags:
  - Methods 
  - R
output:
  pdf_document: default
  html_document: default
layout: post

---
# read files by loop

```{r}
library('parallel')
read_Thin_ahd <- function(x){
    readr::read_fwf(x,col_positions = 
                                readr::fwf_widths(c(5, 10), c("name",'test')))
}
file.dir<- list.files(path='/Users/fanmin/Desktop/',pattern = 'ahd',
                      full.names = T)
```

I random select 3 files in ahd: 
`r list.files(path='/Users/fanmin/Desktop/',pattern = 'ahd')``


# 1. loop
```{r}
loop_reading <- function(x){
    output<- list()
    for(i in x){
        temp_file<-read_Thin_ahd(i)
        output <- append(output,temp_file)
    }
}
system.time(loop_reading(file.dir))
```

# 2. By parlappy
```{r}
no_cores <- detectCores() - 1
cl <- makeCluster(no_cores)
system.time(parLapply(cl, file.dir, read_Thin_ahd))

```


# 3. by data.table ready

```{r}

```