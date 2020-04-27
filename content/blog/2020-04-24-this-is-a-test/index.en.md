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
knitr::kable(data.frame(x = rnorm(3), y = rnorm(3)), align = 'rl', format = "html")
```

<table>
 <thead>
  <tr>
   <th style="text-align:right;"> x </th>
   <th style="text-align:left;"> y </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;"> 0.2174788 </td>
   <td style="text-align:left;"> 1.2859758 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> -0.0862643 </td>
   <td style="text-align:left;"> -0.2227643 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> -0.0502094 </td>
   <td style="text-align:left;"> -1.4075758 </td>
  </tr>
</tbody>
</table>

...
