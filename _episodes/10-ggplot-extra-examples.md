---
title: "Plotting with GGPLOT2 - Extra examples"
author: "Tim Dennis & Reid Otsuji"
teaching: 0
exercises: 0
date: "August 2, 2017"
output:
  html_document:
    toc: yes
questions:
    - "Extra ggplot examples"
source: Rmd
---


## Line Graphs

**Download climate data first**


~~~
download.file('https://raw.github.com/karthikram/ggplot-lecture/master/climate.csv', 'data/climate.csv')
#climate <- read.csv(text=RCurl::getURL(https://raw.github.com/karthikram/ggplot-lecture/master/climate.csv))
~~~
{: .r}

* In the climate data set, `Anomaly10y` is a 10-year running average of the deviation (in Celsius) from the average 1950–1980 temperature, and `Unc10y` is the 95% confidence interval. We’ll set ymax and ymin to Anomaly10y plus or minus Unc10y (Figure 4-25):



~~~
climate <- read.csv("data/climate.csv", header = T)
ggplot(climate, aes(Year, Anomaly10y)) +
  geom_line()
~~~
{: .r}

<img src="../fig/rmd-10-line-plots-1.png" title="plot of chunk line-plots" alt="plot of chunk line-plots" style="display: block; margin: auto;" />

**We can also plot confidence regions**

* In the climate data set, `Anomaly10y` is a 10-year running average of the deviation (in Celsius) from the average 1950–1980 temperature, and `Unc10y` is the 95% confidence interval. We’ll set ymax and ymin to Anomaly10y plus or minus Unc10y (Figure 4-25):


~~~
ggplot(climate, aes(Year, Anomaly10y)) +
  geom_ribbon(aes(ymin = Anomaly10y - Unc10y, ymax = Anomaly10y + Unc10y),
              fill = "blue", alpha = .1) +
  geom_line(color = "steelblue")
~~~
{: .r}

<img src="../fig/rmd-10-unnamed-chunk-2-1.png" title="plot of chunk unnamed-chunk-2" alt="plot of chunk unnamed-chunk-2" style="display: block; margin: auto;" />

### Exercise 2

Modify the previous plot and change it such that there are three lines instead of one with a confidence band.


~~~
cplot <- ggplot(climate, aes(Year, Anomaly10y))
cplot <- cplot + geom_line(size = 0.7, color = "black")
cplot <- cplot + geom_line(aes(Year, Anomaly10y + Unc10y), linetype = "dashed", size = 0.7, color = "red")
cplot <- cplot + geom_line(aes(Year, Anomaly10y - Unc10y), linetype = "dashed", size = 0.7, color = "red")
cplot + theme_gray()
~~~
{: .r}

<img src="../fig/rmd-10-answer-ex2-1.png" title="plot of chunk answer-ex2" alt="plot of chunk answer-ex2" style="display: block; margin: auto;" />

~~~
#theme_classic
#theme_bw()
#theme_minimal()
~~~
{: .r}


## Transformations and Statistics

### With iris data - add a smooth


~~~
ggplot(iris, aes(Sepal.Length, Sepal.Width, color = Species)) +
  geom_point(aes(shape = Species), size = 3) +
  geom_smooth(method = "lm")
~~~
{: .r}

<img src="../fig/rmd-10-smooth-lm-1.png" title="plot of chunk smooth-lm" alt="plot of chunk smooth-lm" style="display: block; margin: auto;" />

### Within facet


~~~
ggplot(iris, aes(Sepal.Length, Sepal.Width, color = Species)) +
  geom_point(aes(shape = Species), size = 3) +
  geom_smooth(method = "lm") +
  facet_grid(. ~ Species)
~~~
{: .r}

<img src="../fig/rmd-10-unnamed-chunk-3-1.png" title="plot of chunk unnamed-chunk-3" alt="plot of chunk unnamed-chunk-3" style="display: block; margin: auto;" />

### With iris along coloumns


~~~
#str(iris)
ggplot(iris, aes(Sepal.Length, Sepal.Width, color = Species)) +
  geom_point() +
  facet_grid(Species ~ .)
~~~
{: .r}

<img src="../fig/rmd-10-facet-columns-1.png" title="plot of chunk facet-columns" alt="plot of chunk facet-columns" style="display: block; margin: auto;" />
### And along rows


~~~
ggplot(iris, aes(Sepal.Length, Sepal.Width, color = Species)) +
  geom_point() +
  facet_grid(. ~ Species)
~~~
{: .r}

<img src="../fig/rmd-10-facet-rows-1.png" title="plot of chunk facet-rows" alt="plot of chunk facet-rows" style="display: block; margin: auto;" />

### Or wrap your panels


~~~
ggplot(iris, aes(Sepal.Length, Sepal.Width, color = Species)) +
  geom_point() +
  facet_wrap( ~ Species)
~~~
{: .r}

<img src="../fig/rmd-10-unnamed-chunk-4-1.png" title="plot of chunk unnamed-chunk-4" alt="plot of chunk unnamed-chunk-4" style="display: block; margin: auto;" />

## Bar Charts

## Exercise 4

* Using the climate dataset, create a new variable called sign. Make it logical (true/false) based on the sign of Anomaly10y.
* Plot a bar plot and use sign variable as the fill.
* HINT: Look up `ifelse` function to create `clim$sign`


~~~
clim <- read.csv('data/climate.csv', header = TRUE)
clim$sign <- ifelse(clim$Anomaly10y<0, FALSE, TRUE)
# or as simple as
# clim$sign <- clim$Anomaly10y < 0
ggplot(clim, aes(Year, Anomaly10y)) + geom_bar(stat = "identity", aes(fill = sign)) + theme_gray()
~~~
{: .r}

<img src="../fig/rmd-10-unnamed-chunk-5-1.png" title="plot of chunk unnamed-chunk-5" alt="plot of chunk unnamed-chunk-5" style="display: block; margin: auto;" />
