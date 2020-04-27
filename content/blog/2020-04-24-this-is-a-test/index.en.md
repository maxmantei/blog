---
title: this is a test
author: Max
date: '2020-04-24'
slug: this-is-a-test
categories: []
tags: []
toc: false
images: null
output: 
  html_document: 
    keep_md: yes
    theme: null
---



## R code


```r
3 + 6
```

```
[1] 9
```
### R plot


```r
hist(rpois(5, 1.5))
```

![](hist-pois-1.png)<!-- -->
## Python code


```python
print(4 + 3)
```

```
7
```

## $\LaTeX$

$$y = x^2 + 3x - 5$$

## A Table?

|item   | a | b |
|------:|--:|--:|
|tomato | 3 | 5 |
|apple  | 2 | 0 |


### now a table?


```r
knitr::kable(data.frame(x = rnorm(3), y = rnorm(3)))
```

          x            y
-----------  -----------
 -0.0871453    0.1577408
  0.3743182    0.5726561
  0.3768026   -0.1726091
