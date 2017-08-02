---
layout: page
title: Setup
permalink: /setup/
---

This lesson assumes you have the R, RStudio software installed on your computer.

R can be downloaded [here](https://cran.r-project.org/mirrors.html).

RStudio is an environment for developing using R.
It can be downloaded [here](https://www.rstudio.com/products/rstudio/download/).
You will need the Desktop version for your computer.

You can also install the packages we will be using R.  To do this open RStudio and in the console (bottom of the window) type:

```
install.packages('tidyverse')
```

Tidyverse is a collection of packages that are commonly used for data acquisition, cleaning, analysis and visualization.

If you load (tell R you want to use it in your current session) `tidyverse` by running:

```
library(tidyverse)
#> Loading tidyverse: ggplot2
#> Loading tidyverse: tibble
#> Loading tidyverse: tidyr
#> Loading tidyverse: readr
#> Loading tidyverse: purrr
#> Loading tidyverse: dplyr
```
R will print out the other packages loaded by the tidyverse package.  You can also install a couple of more stand-alone packages we will use:

```
install.packages('dataverse') #provides access to Dataverse v.4 APIs for search, retrieval & deposit.
```

Load it:

```
library(dataverse)
```

And one more:

```
install.packages('xlsx')
```

This might fail b/c `xlsx` depends on a package called rJava, which also requires your system to run a JDK (Java Development Kit). Don't worry if you can't get it installed for class, you can use example code later -- I put the exmaple in more for demonstration.
