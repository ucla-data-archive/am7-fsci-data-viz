---
title: "Reading Data in R"
teaching: 20
exercises: 0
output: html_document
---



## Reading in Data

One of R’s most powerful features is its ability to deal with tabular data - such as you may already have in a spreadsheet or a CSV file. Let’s start by making a toy dataset in your data/ directory, called feline-data.csv:

We can load this into R via the following:

The read.table function is used for reading in tabular data stored in a text file where the columns of data are separated by punctuation characters such as CSV files (csv = comma-separated values). Tabs and commas are the most common punctuation characters used to separate or delimit data points in csv files. For convenience R provides 2 other versions of read.table. These are: read.csv for files where the data are separated with commas and read.delim for files where the data are separated with tabs. Of these three functions read.csv is the most commonly used. If needed it is possible to override the default delimiting punctuation marks for both read.csv and read.delim.

We can begin exploring our dataset right away, pulling out columns by specifying them using the $ operator:


```r
head(read.csv('data/gapminder-FiveYearData.csv')) #outputs to screen just top of dataframe
```

```
##       country year      pop continent lifeExp gdpPercap
## 1 Afghanistan 1952  8425333      Asia  28.801  779.4453
## 2 Afghanistan 1957  9240934      Asia  30.332  820.8530
## 3 Afghanistan 1962 10267083      Asia  31.997  853.1007
## 4 Afghanistan 1967 11537966      Asia  34.020  836.1971
## 5 Afghanistan 1972 13079460      Asia  36.088  739.9811
## 6 Afghanistan 1977 14880372      Asia  38.438  786.1134
```


```r
gapmind <- read.csv('data/gapminder-FiveYearData.csv') # Saves dataframe as variable (see Environment top right change)
```


```r
head(gapmind)
```

```
##       country year      pop continent lifeExp gdpPercap
## 1 Afghanistan 1952  8425333      Asia  28.801  779.4453
## 2 Afghanistan 1957  9240934      Asia  30.332  820.8530
## 3 Afghanistan 1962 10267083      Asia  31.997  853.1007
## 4 Afghanistan 1967 11537966      Asia  34.020  836.1971
## 5 Afghanistan 1972 13079460      Asia  36.088  739.9811
## 6 Afghanistan 1977 14880372      Asia  38.438  786.1134
```


```r
str(gapmind) #prints out information about the dataset including the data types (v. important in plotting)
```

```
## 'data.frame':	1704 obs. of  6 variables:
##  $ country  : Factor w/ 142 levels "Afghanistan",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ year     : int  1952 1957 1962 1967 1972 1977 1982 1987 1992 1997 ...
##  $ pop      : num  8425333 9240934 10267083 11537966 13079460 ...
##  $ continent: Factor w/ 5 levels "Africa","Americas",..: 3 3 3 3 3 3 3 3 3 3 ...
##  $ lifeExp  : num  28.8 30.3 32 34 36.1 ...
##  $ gdpPercap: num  779 821 853 836 740 ...
```

* Notice that character columns in the dataframe are convereted to `factors` by default in R on read.
* You can turn off this behavior by using a `read.csv("data/gapminder-FiveYearData.csv", **stringsAsFactors = FALSE**)` to the `read.csv`function.

### What about other formats? I have xls, dta, spss


```r
#install.packages('foreign', 'xlsx') #remove the pound in front of this line to install it, if you haven't yet
library(foreign) #turn it on
library(xlsx)
```

```
## Loading required package: rJava
```

```
## Loading required package: methods
```

```
## Loading required package: xlsxjars
```


```r
read.xlsx('data/gapminder-FiveYearData.xlsx', 1)
```

```
## Error in loadWorkbook(file): Cannot find data/gapminder-FiveYearData.xlsx
```

### Reading from the Web


```r
read.csv("https://raw.githubusercontent.com/swcarpentry/r-novice-gapminder/gh-pages/_episodes_rmd/data/gapminder-FiveYearData.csv")
```

```
##                       country year        pop continent  lifeExp
## 1                 Afghanistan 1952    8425333      Asia 28.80100
## 2                 Afghanistan 1957    9240934      Asia 30.33200
## 3                 Afghanistan 1962   10267083      Asia 31.99700
## 4                 Afghanistan 1967   11537966      Asia 34.02000
## 5                 Afghanistan 1972   13079460      Asia 36.08800
## 6                 Afghanistan 1977   14880372      Asia 38.43800
## 7                 Afghanistan 1982   12881816      Asia 39.85400
## 8                 Afghanistan 1987   13867957      Asia 40.82200
## 9                 Afghanistan 1992   16317921      Asia 41.67400
## 10                Afghanistan 1997   22227415      Asia 41.76300
## 11                Afghanistan 2002   25268405      Asia 42.12900
## 12                Afghanistan 2007   31889923      Asia 43.82800
## 13                    Albania 1952    1282697    Europe 55.23000
## 14                    Albania 1957    1476505    Europe 59.28000
## 15                    Albania 1962    1728137    Europe 64.82000
## 16                    Albania 1967    1984060    Europe 66.22000
## 17                    Albania 1972    2263554    Europe 67.69000
## 18                    Albania 1977    2509048    Europe 68.93000
## 19                    Albania 1982    2780097    Europe 70.42000
## 20                    Albania 1987    3075321    Europe 72.00000
## 21                    Albania 1992    3326498    Europe 71.58100
## 22                    Albania 1997    3428038    Europe 72.95000
## 23                    Albania 2002    3508512    Europe 75.65100
## 24                    Albania 2007    3600523    Europe 76.42300
## 25                    Algeria 1952    9279525    Africa 43.07700
## 26                    Algeria 1957   10270856    Africa 45.68500
## 27                    Algeria 1962   11000948    Africa 48.30300
## 28                    Algeria 1967   12760499    Africa 51.40700
## 29                    Algeria 1972   14760787    Africa 54.51800
## 30                    Algeria 1977   17152804    Africa 58.01400
## 31                    Algeria 1982   20033753    Africa 61.36800
## 32                    Algeria 1987   23254956    Africa 65.79900
## 33                    Algeria 1992   26298373    Africa 67.74400
## 34                    Algeria 1997   29072015    Africa 69.15200
## 35                    Algeria 2002   31287142    Africa 70.99400
## 36                    Algeria 2007   33333216    Africa 72.30100
## 37                     Angola 1952    4232095    Africa 30.01500
## 38                     Angola 1957    4561361    Africa 31.99900
## 39                     Angola 1962    4826015    Africa 34.00000
## 40                     Angola 1967    5247469    Africa 35.98500
## 41                     Angola 1972    5894858    Africa 37.92800
## 42                     Angola 1977    6162675    Africa 39.48300
## 43                     Angola 1982    7016384    Africa 39.94200
## 44                     Angola 1987    7874230    Africa 39.90600
## 45                     Angola 1992    8735988    Africa 40.64700
## 46                     Angola 1997    9875024    Africa 40.96300
## 47                     Angola 2002   10866106    Africa 41.00300
## 48                     Angola 2007   12420476    Africa 42.73100
## 49                  Argentina 1952   17876956  Americas 62.48500
## 50                  Argentina 1957   19610538  Americas 64.39900
## 51                  Argentina 1962   21283783  Americas 65.14200
## 52                  Argentina 1967   22934225  Americas 65.63400
## 53                  Argentina 1972   24779799  Americas 67.06500
## 54                  Argentina 1977   26983828  Americas 68.48100
## 55                  Argentina 1982   29341374  Americas 69.94200
## 56                  Argentina 1987   31620918  Americas 70.77400
## 57                  Argentina 1992   33958947  Americas 71.86800
## 58                  Argentina 1997   36203463  Americas 73.27500
## 59                  Argentina 2002   38331121  Americas 74.34000
## 60                  Argentina 2007   40301927  Americas 75.32000
## 61                  Australia 1952    8691212   Oceania 69.12000
## 62                  Australia 1957    9712569   Oceania 70.33000
## 63                  Australia 1962   10794968   Oceania 70.93000
## 64                  Australia 1967   11872264   Oceania 71.10000
## 65                  Australia 1972   13177000   Oceania 71.93000
## 66                  Australia 1977   14074100   Oceania 73.49000
## 67                  Australia 1982   15184200   Oceania 74.74000
## 68                  Australia 1987   16257249   Oceania 76.32000
## 69                  Australia 1992   17481977   Oceania 77.56000
## 70                  Australia 1997   18565243   Oceania 78.83000
## 71                  Australia 2002   19546792   Oceania 80.37000
## 72                  Australia 2007   20434176   Oceania 81.23500
## 73                    Austria 1952    6927772    Europe 66.80000
## 74                    Austria 1957    6965860    Europe 67.48000
## 75                    Austria 1962    7129864    Europe 69.54000
## 76                    Austria 1967    7376998    Europe 70.14000
## 77                    Austria 1972    7544201    Europe 70.63000
## 78                    Austria 1977    7568430    Europe 72.17000
## 79                    Austria 1982    7574613    Europe 73.18000
## 80                    Austria 1987    7578903    Europe 74.94000
## 81                    Austria 1992    7914969    Europe 76.04000
## 82                    Austria 1997    8069876    Europe 77.51000
## 83                    Austria 2002    8148312    Europe 78.98000
## 84                    Austria 2007    8199783    Europe 79.82900
## 85                    Bahrain 1952     120447      Asia 50.93900
## 86                    Bahrain 1957     138655      Asia 53.83200
## 87                    Bahrain 1962     171863      Asia 56.92300
## 88                    Bahrain 1967     202182      Asia 59.92300
## 89                    Bahrain 1972     230800      Asia 63.30000
## 90                    Bahrain 1977     297410      Asia 65.59300
## 91                    Bahrain 1982     377967      Asia 69.05200
## 92                    Bahrain 1987     454612      Asia 70.75000
## 93                    Bahrain 1992     529491      Asia 72.60100
## 94                    Bahrain 1997     598561      Asia 73.92500
## 95                    Bahrain 2002     656397      Asia 74.79500
## 96                    Bahrain 2007     708573      Asia 75.63500
## 97                 Bangladesh 1952   46886859      Asia 37.48400
## 98                 Bangladesh 1957   51365468      Asia 39.34800
## 99                 Bangladesh 1962   56839289      Asia 41.21600
## 100                Bangladesh 1967   62821884      Asia 43.45300
## 101                Bangladesh 1972   70759295      Asia 45.25200
## 102                Bangladesh 1977   80428306      Asia 46.92300
## 103                Bangladesh 1982   93074406      Asia 50.00900
## 104                Bangladesh 1987  103764241      Asia 52.81900
## 105                Bangladesh 1992  113704579      Asia 56.01800
## 106                Bangladesh 1997  123315288      Asia 59.41200
## 107                Bangladesh 2002  135656790      Asia 62.01300
## 108                Bangladesh 2007  150448339      Asia 64.06200
## 109                   Belgium 1952    8730405    Europe 68.00000
## 110                   Belgium 1957    8989111    Europe 69.24000
## 111                   Belgium 1962    9218400    Europe 70.25000
## 112                   Belgium 1967    9556500    Europe 70.94000
## 113                   Belgium 1972    9709100    Europe 71.44000
## 114                   Belgium 1977    9821800    Europe 72.80000
## 115                   Belgium 1982    9856303    Europe 73.93000
## 116                   Belgium 1987    9870200    Europe 75.35000
## 117                   Belgium 1992   10045622    Europe 76.46000
## 118                   Belgium 1997   10199787    Europe 77.53000
## 119                   Belgium 2002   10311970    Europe 78.32000
## 120                   Belgium 2007   10392226    Europe 79.44100
## 121                     Benin 1952    1738315    Africa 38.22300
## 122                     Benin 1957    1925173    Africa 40.35800
## 123                     Benin 1962    2151895    Africa 42.61800
## 124                     Benin 1967    2427334    Africa 44.88500
## 125                     Benin 1972    2761407    Africa 47.01400
## 126                     Benin 1977    3168267    Africa 49.19000
## 127                     Benin 1982    3641603    Africa 50.90400
## 128                     Benin 1987    4243788    Africa 52.33700
## 129                     Benin 1992    4981671    Africa 53.91900
## 130                     Benin 1997    6066080    Africa 54.77700
## 131                     Benin 2002    7026113    Africa 54.40600
## 132                     Benin 2007    8078314    Africa 56.72800
## 133                   Bolivia 1952    2883315  Americas 40.41400
## 134                   Bolivia 1957    3211738  Americas 41.89000
## 135                   Bolivia 1962    3593918  Americas 43.42800
## 136                   Bolivia 1967    4040665  Americas 45.03200
## 137                   Bolivia 1972    4565872  Americas 46.71400
## 138                   Bolivia 1977    5079716  Americas 50.02300
## 139                   Bolivia 1982    5642224  Americas 53.85900
## 140                   Bolivia 1987    6156369  Americas 57.25100
## 141                   Bolivia 1992    6893451  Americas 59.95700
## 142                   Bolivia 1997    7693188  Americas 62.05000
## 143                   Bolivia 2002    8445134  Americas 63.88300
## 144                   Bolivia 2007    9119152  Americas 65.55400
## 145    Bosnia and Herzegovina 1952    2791000    Europe 53.82000
## 146    Bosnia and Herzegovina 1957    3076000    Europe 58.45000
## 147    Bosnia and Herzegovina 1962    3349000    Europe 61.93000
## 148    Bosnia and Herzegovina 1967    3585000    Europe 64.79000
## 149    Bosnia and Herzegovina 1972    3819000    Europe 67.45000
## 150    Bosnia and Herzegovina 1977    4086000    Europe 69.86000
## 151    Bosnia and Herzegovina 1982    4172693    Europe 70.69000
## 152    Bosnia and Herzegovina 1987    4338977    Europe 71.14000
## 153    Bosnia and Herzegovina 1992    4256013    Europe 72.17800
## 154    Bosnia and Herzegovina 1997    3607000    Europe 73.24400
## 155    Bosnia and Herzegovina 2002    4165416    Europe 74.09000
## 156    Bosnia and Herzegovina 2007    4552198    Europe 74.85200
## 157                  Botswana 1952     442308    Africa 47.62200
## 158                  Botswana 1957     474639    Africa 49.61800
## 159                  Botswana 1962     512764    Africa 51.52000
## 160                  Botswana 1967     553541    Africa 53.29800
## 161                  Botswana 1972     619351    Africa 56.02400
## 162                  Botswana 1977     781472    Africa 59.31900
## 163                  Botswana 1982     970347    Africa 61.48400
## 164                  Botswana 1987    1151184    Africa 63.62200
## 165                  Botswana 1992    1342614    Africa 62.74500
## 166                  Botswana 1997    1536536    Africa 52.55600
## 167                  Botswana 2002    1630347    Africa 46.63400
## 168                  Botswana 2007    1639131    Africa 50.72800
## 169                    Brazil 1952   56602560  Americas 50.91700
## 170                    Brazil 1957   65551171  Americas 53.28500
## 171                    Brazil 1962   76039390  Americas 55.66500
## 172                    Brazil 1967   88049823  Americas 57.63200
## 173                    Brazil 1972  100840058  Americas 59.50400
## 174                    Brazil 1977  114313951  Americas 61.48900
## 175                    Brazil 1982  128962939  Americas 63.33600
## 176                    Brazil 1987  142938076  Americas 65.20500
## 177                    Brazil 1992  155975974  Americas 67.05700
## 178                    Brazil 1997  168546719  Americas 69.38800
## 179                    Brazil 2002  179914212  Americas 71.00600
## 180                    Brazil 2007  190010647  Americas 72.39000
## 181                  Bulgaria 1952    7274900    Europe 59.60000
## 182                  Bulgaria 1957    7651254    Europe 66.61000
## 183                  Bulgaria 1962    8012946    Europe 69.51000
## 184                  Bulgaria 1967    8310226    Europe 70.42000
## 185                  Bulgaria 1972    8576200    Europe 70.90000
## 186                  Bulgaria 1977    8797022    Europe 70.81000
## 187                  Bulgaria 1982    8892098    Europe 71.08000
## 188                  Bulgaria 1987    8971958    Europe 71.34000
## 189                  Bulgaria 1992    8658506    Europe 71.19000
## 190                  Bulgaria 1997    8066057    Europe 70.32000
## 191                  Bulgaria 2002    7661799    Europe 72.14000
## 192                  Bulgaria 2007    7322858    Europe 73.00500
## 193              Burkina Faso 1952    4469979    Africa 31.97500
## 194              Burkina Faso 1957    4713416    Africa 34.90600
## 195              Burkina Faso 1962    4919632    Africa 37.81400
## 196              Burkina Faso 1967    5127935    Africa 40.69700
## 197              Burkina Faso 1972    5433886    Africa 43.59100
## 198              Burkina Faso 1977    5889574    Africa 46.13700
## 199              Burkina Faso 1982    6634596    Africa 48.12200
## 200              Burkina Faso 1987    7586551    Africa 49.55700
## 201              Burkina Faso 1992    8878303    Africa 50.26000
## 202              Burkina Faso 1997   10352843    Africa 50.32400
## 203              Burkina Faso 2002   12251209    Africa 50.65000
## 204              Burkina Faso 2007   14326203    Africa 52.29500
## 205                   Burundi 1952    2445618    Africa 39.03100
## 206                   Burundi 1957    2667518    Africa 40.53300
## 207                   Burundi 1962    2961915    Africa 42.04500
## 208                   Burundi 1967    3330989    Africa 43.54800
## 209                   Burundi 1972    3529983    Africa 44.05700
## 210                   Burundi 1977    3834415    Africa 45.91000
## 211                   Burundi 1982    4580410    Africa 47.47100
## 212                   Burundi 1987    5126023    Africa 48.21100
## 213                   Burundi 1992    5809236    Africa 44.73600
## 214                   Burundi 1997    6121610    Africa 45.32600
## 215                   Burundi 2002    7021078    Africa 47.36000
## 216                   Burundi 2007    8390505    Africa 49.58000
## 217                  Cambodia 1952    4693836      Asia 39.41700
## 218                  Cambodia 1957    5322536      Asia 41.36600
## 219                  Cambodia 1962    6083619      Asia 43.41500
## 220                  Cambodia 1967    6960067      Asia 45.41500
## 221                  Cambodia 1972    7450606      Asia 40.31700
## 222                  Cambodia 1977    6978607      Asia 31.22000
## 223                  Cambodia 1982    7272485      Asia 50.95700
## 224                  Cambodia 1987    8371791      Asia 53.91400
## 225                  Cambodia 1992   10150094      Asia 55.80300
## 226                  Cambodia 1997   11782962      Asia 56.53400
## 227                  Cambodia 2002   12926707      Asia 56.75200
## 228                  Cambodia 2007   14131858      Asia 59.72300
## 229                  Cameroon 1952    5009067    Africa 38.52300
## 230                  Cameroon 1957    5359923    Africa 40.42800
## 231                  Cameroon 1962    5793633    Africa 42.64300
## 232                  Cameroon 1967    6335506    Africa 44.79900
## 233                  Cameroon 1972    7021028    Africa 47.04900
## 234                  Cameroon 1977    7959865    Africa 49.35500
## 235                  Cameroon 1982    9250831    Africa 52.96100
## 236                  Cameroon 1987   10780667    Africa 54.98500
## 237                  Cameroon 1992   12467171    Africa 54.31400
## 238                  Cameroon 1997   14195809    Africa 52.19900
## 239                  Cameroon 2002   15929988    Africa 49.85600
## 240                  Cameroon 2007   17696293    Africa 50.43000
## 241                    Canada 1952   14785584  Americas 68.75000
## 242                    Canada 1957   17010154  Americas 69.96000
## 243                    Canada 1962   18985849  Americas 71.30000
## 244                    Canada 1967   20819767  Americas 72.13000
## 245                    Canada 1972   22284500  Americas 72.88000
## 246                    Canada 1977   23796400  Americas 74.21000
## 247                    Canada 1982   25201900  Americas 75.76000
## 248                    Canada 1987   26549700  Americas 76.86000
## 249                    Canada 1992   28523502  Americas 77.95000
## 250                    Canada 1997   30305843  Americas 78.61000
## 251                    Canada 2002   31902268  Americas 79.77000
## 252                    Canada 2007   33390141  Americas 80.65300
## 253  Central African Republic 1952    1291695    Africa 35.46300
## 254  Central African Republic 1957    1392284    Africa 37.46400
## 255  Central African Republic 1962    1523478    Africa 39.47500
## 256  Central African Republic 1967    1733638    Africa 41.47800
## 257  Central African Republic 1972    1927260    Africa 43.45700
## 258  Central African Republic 1977    2167533    Africa 46.77500
## 259  Central African Republic 1982    2476971    Africa 48.29500
## 260  Central African Republic 1987    2840009    Africa 50.48500
## 261  Central African Republic 1992    3265124    Africa 49.39600
## 262  Central African Republic 1997    3696513    Africa 46.06600
## 263  Central African Republic 2002    4048013    Africa 43.30800
## 264  Central African Republic 2007    4369038    Africa 44.74100
## 265                      Chad 1952    2682462    Africa 38.09200
## 266                      Chad 1957    2894855    Africa 39.88100
## 267                      Chad 1962    3150417    Africa 41.71600
## 268                      Chad 1967    3495967    Africa 43.60100
## 269                      Chad 1972    3899068    Africa 45.56900
## 270                      Chad 1977    4388260    Africa 47.38300
## 271                      Chad 1982    4875118    Africa 49.51700
## 272                      Chad 1987    5498955    Africa 51.05100
## 273                      Chad 1992    6429417    Africa 51.72400
## 274                      Chad 1997    7562011    Africa 51.57300
## 275                      Chad 2002    8835739    Africa 50.52500
## 276                      Chad 2007   10238807    Africa 50.65100
## 277                     Chile 1952    6377619  Americas 54.74500
## 278                     Chile 1957    7048426  Americas 56.07400
## 279                     Chile 1962    7961258  Americas 57.92400
## 280                     Chile 1967    8858908  Americas 60.52300
## 281                     Chile 1972    9717524  Americas 63.44100
## 282                     Chile 1977   10599793  Americas 67.05200
## 283                     Chile 1982   11487112  Americas 70.56500
## 284                     Chile 1987   12463354  Americas 72.49200
## 285                     Chile 1992   13572994  Americas 74.12600
## 286                     Chile 1997   14599929  Americas 75.81600
## 287                     Chile 2002   15497046  Americas 77.86000
## 288                     Chile 2007   16284741  Americas 78.55300
## 289                     China 1952  556263528      Asia 44.00000
## 290                     China 1957  637408000      Asia 50.54896
## 291                     China 1962  665770000      Asia 44.50136
## 292                     China 1967  754550000      Asia 58.38112
## 293                     China 1972  862030000      Asia 63.11888
## 294                     China 1977  943455000      Asia 63.96736
## 295                     China 1982 1000281000      Asia 65.52500
## 296                     China 1987 1084035000      Asia 67.27400
## 297                     China 1992 1164970000      Asia 68.69000
## 298                     China 1997 1230075000      Asia 70.42600
## 299                     China 2002 1280400000      Asia 72.02800
## 300                     China 2007 1318683096      Asia 72.96100
## 301                  Colombia 1952   12350771  Americas 50.64300
## 302                  Colombia 1957   14485993  Americas 55.11800
## 303                  Colombia 1962   17009885  Americas 57.86300
## 304                  Colombia 1967   19764027  Americas 59.96300
## 305                  Colombia 1972   22542890  Americas 61.62300
## 306                  Colombia 1977   25094412  Americas 63.83700
## 307                  Colombia 1982   27764644  Americas 66.65300
## 308                  Colombia 1987   30964245  Americas 67.76800
## 309                  Colombia 1992   34202721  Americas 68.42100
## 310                  Colombia 1997   37657830  Americas 70.31300
## 311                  Colombia 2002   41008227  Americas 71.68200
## 312                  Colombia 2007   44227550  Americas 72.88900
## 313                   Comoros 1952     153936    Africa 40.71500
## 314                   Comoros 1957     170928    Africa 42.46000
## 315                   Comoros 1962     191689    Africa 44.46700
## 316                   Comoros 1967     217378    Africa 46.47200
## 317                   Comoros 1972     250027    Africa 48.94400
## 318                   Comoros 1977     304739    Africa 50.93900
## 319                   Comoros 1982     348643    Africa 52.93300
## 320                   Comoros 1987     395114    Africa 54.92600
## 321                   Comoros 1992     454429    Africa 57.93900
## 322                   Comoros 1997     527982    Africa 60.66000
## 323                   Comoros 2002     614382    Africa 62.97400
## 324                   Comoros 2007     710960    Africa 65.15200
## 325           Congo Dem. Rep. 1952   14100005    Africa 39.14300
## 326           Congo Dem. Rep. 1957   15577932    Africa 40.65200
## 327           Congo Dem. Rep. 1962   17486434    Africa 42.12200
## 328           Congo Dem. Rep. 1967   19941073    Africa 44.05600
## 329           Congo Dem. Rep. 1972   23007669    Africa 45.98900
## 330           Congo Dem. Rep. 1977   26480870    Africa 47.80400
## 331           Congo Dem. Rep. 1982   30646495    Africa 47.78400
## 332           Congo Dem. Rep. 1987   35481645    Africa 47.41200
## 333           Congo Dem. Rep. 1992   41672143    Africa 45.54800
## 334           Congo Dem. Rep. 1997   47798986    Africa 42.58700
## 335           Congo Dem. Rep. 2002   55379852    Africa 44.96600
## 336           Congo Dem. Rep. 2007   64606759    Africa 46.46200
## 337                Congo Rep. 1952     854885    Africa 42.11100
## 338                Congo Rep. 1957     940458    Africa 45.05300
## 339                Congo Rep. 1962    1047924    Africa 48.43500
## 340                Congo Rep. 1967    1179760    Africa 52.04000
## 341                Congo Rep. 1972    1340458    Africa 54.90700
## 342                Congo Rep. 1977    1536769    Africa 55.62500
## 343                Congo Rep. 1982    1774735    Africa 56.69500
## 344                Congo Rep. 1987    2064095    Africa 57.47000
## 345                Congo Rep. 1992    2409073    Africa 56.43300
## 346                Congo Rep. 1997    2800947    Africa 52.96200
## 347                Congo Rep. 2002    3328795    Africa 52.97000
## 348                Congo Rep. 2007    3800610    Africa 55.32200
## 349                Costa Rica 1952     926317  Americas 57.20600
## 350                Costa Rica 1957    1112300  Americas 60.02600
## 351                Costa Rica 1962    1345187  Americas 62.84200
## 352                Costa Rica 1967    1588717  Americas 65.42400
## 353                Costa Rica 1972    1834796  Americas 67.84900
## 354                Costa Rica 1977    2108457  Americas 70.75000
## 355                Costa Rica 1982    2424367  Americas 73.45000
## 356                Costa Rica 1987    2799811  Americas 74.75200
## 357                Costa Rica 1992    3173216  Americas 75.71300
## 358                Costa Rica 1997    3518107  Americas 77.26000
## 359                Costa Rica 2002    3834934  Americas 78.12300
## 360                Costa Rica 2007    4133884  Americas 78.78200
## 361             Cote d'Ivoire 1952    2977019    Africa 40.47700
## 362             Cote d'Ivoire 1957    3300000    Africa 42.46900
## 363             Cote d'Ivoire 1962    3832408    Africa 44.93000
## 364             Cote d'Ivoire 1967    4744870    Africa 47.35000
## 365             Cote d'Ivoire 1972    6071696    Africa 49.80100
## 366             Cote d'Ivoire 1977    7459574    Africa 52.37400
## 367             Cote d'Ivoire 1982    9025951    Africa 53.98300
## 368             Cote d'Ivoire 1987   10761098    Africa 54.65500
## 369             Cote d'Ivoire 1992   12772596    Africa 52.04400
## 370             Cote d'Ivoire 1997   14625967    Africa 47.99100
## 371             Cote d'Ivoire 2002   16252726    Africa 46.83200
## 372             Cote d'Ivoire 2007   18013409    Africa 48.32800
## 373                   Croatia 1952    3882229    Europe 61.21000
## 374                   Croatia 1957    3991242    Europe 64.77000
## 375                   Croatia 1962    4076557    Europe 67.13000
## 376                   Croatia 1967    4174366    Europe 68.50000
## 377                   Croatia 1972    4225310    Europe 69.61000
## 378                   Croatia 1977    4318673    Europe 70.64000
## 379                   Croatia 1982    4413368    Europe 70.46000
## 380                   Croatia 1987    4484310    Europe 71.52000
## 381                   Croatia 1992    4494013    Europe 72.52700
## 382                   Croatia 1997    4444595    Europe 73.68000
## 383                   Croatia 2002    4481020    Europe 74.87600
## 384                   Croatia 2007    4493312    Europe 75.74800
## 385                      Cuba 1952    6007797  Americas 59.42100
## 386                      Cuba 1957    6640752  Americas 62.32500
## 387                      Cuba 1962    7254373  Americas 65.24600
## 388                      Cuba 1967    8139332  Americas 68.29000
## 389                      Cuba 1972    8831348  Americas 70.72300
## 390                      Cuba 1977    9537988  Americas 72.64900
## 391                      Cuba 1982    9789224  Americas 73.71700
## 392                      Cuba 1987   10239839  Americas 74.17400
## 393                      Cuba 1992   10723260  Americas 74.41400
## 394                      Cuba 1997   10983007  Americas 76.15100
## 395                      Cuba 2002   11226999  Americas 77.15800
## 396                      Cuba 2007   11416987  Americas 78.27300
## 397            Czech Republic 1952    9125183    Europe 66.87000
## 398            Czech Republic 1957    9513758    Europe 69.03000
## 399            Czech Republic 1962    9620282    Europe 69.90000
## 400            Czech Republic 1967    9835109    Europe 70.38000
## 401            Czech Republic 1972    9862158    Europe 70.29000
## 402            Czech Republic 1977   10161915    Europe 70.71000
## 403            Czech Republic 1982   10303704    Europe 70.96000
## 404            Czech Republic 1987   10311597    Europe 71.58000
## 405            Czech Republic 1992   10315702    Europe 72.40000
## 406            Czech Republic 1997   10300707    Europe 74.01000
## 407            Czech Republic 2002   10256295    Europe 75.51000
## 408            Czech Republic 2007   10228744    Europe 76.48600
## 409                   Denmark 1952    4334000    Europe 70.78000
## 410                   Denmark 1957    4487831    Europe 71.81000
## 411                   Denmark 1962    4646899    Europe 72.35000
## 412                   Denmark 1967    4838800    Europe 72.96000
## 413                   Denmark 1972    4991596    Europe 73.47000
## 414                   Denmark 1977    5088419    Europe 74.69000
## 415                   Denmark 1982    5117810    Europe 74.63000
## 416                   Denmark 1987    5127024    Europe 74.80000
## 417                   Denmark 1992    5171393    Europe 75.33000
## 418                   Denmark 1997    5283663    Europe 76.11000
## 419                   Denmark 2002    5374693    Europe 77.18000
## 420                   Denmark 2007    5468120    Europe 78.33200
## 421                  Djibouti 1952      63149    Africa 34.81200
## 422                  Djibouti 1957      71851    Africa 37.32800
## 423                  Djibouti 1962      89898    Africa 39.69300
## 424                  Djibouti 1967     127617    Africa 42.07400
## 425                  Djibouti 1972     178848    Africa 44.36600
## 426                  Djibouti 1977     228694    Africa 46.51900
## 427                  Djibouti 1982     305991    Africa 48.81200
## 428                  Djibouti 1987     311025    Africa 50.04000
## 429                  Djibouti 1992     384156    Africa 51.60400
## 430                  Djibouti 1997     417908    Africa 53.15700
## 431                  Djibouti 2002     447416    Africa 53.37300
## 432                  Djibouti 2007     496374    Africa 54.79100
## 433        Dominican Republic 1952    2491346  Americas 45.92800
## 434        Dominican Republic 1957    2923186  Americas 49.82800
## 435        Dominican Republic 1962    3453434  Americas 53.45900
## 436        Dominican Republic 1967    4049146  Americas 56.75100
## 437        Dominican Republic 1972    4671329  Americas 59.63100
## 438        Dominican Republic 1977    5302800  Americas 61.78800
## 439        Dominican Republic 1982    5968349  Americas 63.72700
## 440        Dominican Republic 1987    6655297  Americas 66.04600
## 441        Dominican Republic 1992    7351181  Americas 68.45700
## 442        Dominican Republic 1997    7992357  Americas 69.95700
## 443        Dominican Republic 2002    8650322  Americas 70.84700
## 444        Dominican Republic 2007    9319622  Americas 72.23500
## 445                   Ecuador 1952    3548753  Americas 48.35700
## 446                   Ecuador 1957    4058385  Americas 51.35600
## 447                   Ecuador 1962    4681707  Americas 54.64000
## 448                   Ecuador 1967    5432424  Americas 56.67800
## 449                   Ecuador 1972    6298651  Americas 58.79600
## 450                   Ecuador 1977    7278866  Americas 61.31000
## 451                   Ecuador 1982    8365850  Americas 64.34200
## 452                   Ecuador 1987    9545158  Americas 67.23100
## 453                   Ecuador 1992   10748394  Americas 69.61300
## 454                   Ecuador 1997   11911819  Americas 72.31200
## 455                   Ecuador 2002   12921234  Americas 74.17300
## 456                   Ecuador 2007   13755680  Americas 74.99400
## 457                     Egypt 1952   22223309    Africa 41.89300
## 458                     Egypt 1957   25009741    Africa 44.44400
## 459                     Egypt 1962   28173309    Africa 46.99200
## 460                     Egypt 1967   31681188    Africa 49.29300
## 461                     Egypt 1972   34807417    Africa 51.13700
## 462                     Egypt 1977   38783863    Africa 53.31900
## 463                     Egypt 1982   45681811    Africa 56.00600
## 464                     Egypt 1987   52799062    Africa 59.79700
## 465                     Egypt 1992   59402198    Africa 63.67400
## 466                     Egypt 1997   66134291    Africa 67.21700
## 467                     Egypt 2002   73312559    Africa 69.80600
## 468                     Egypt 2007   80264543    Africa 71.33800
## 469               El Salvador 1952    2042865  Americas 45.26200
## 470               El Salvador 1957    2355805  Americas 48.57000
## 471               El Salvador 1962    2747687  Americas 52.30700
## 472               El Salvador 1967    3232927  Americas 55.85500
## 473               El Salvador 1972    3790903  Americas 58.20700
## 474               El Salvador 1977    4282586  Americas 56.69600
## 475               El Salvador 1982    4474873  Americas 56.60400
## 476               El Salvador 1987    4842194  Americas 63.15400
## 477               El Salvador 1992    5274649  Americas 66.79800
## 478               El Salvador 1997    5783439  Americas 69.53500
## 479               El Salvador 2002    6353681  Americas 70.73400
## 480               El Salvador 2007    6939688  Americas 71.87800
## 481         Equatorial Guinea 1952     216964    Africa 34.48200
## 482         Equatorial Guinea 1957     232922    Africa 35.98300
## 483         Equatorial Guinea 1962     249220    Africa 37.48500
## 484         Equatorial Guinea 1967     259864    Africa 38.98700
## 485         Equatorial Guinea 1972     277603    Africa 40.51600
## 486         Equatorial Guinea 1977     192675    Africa 42.02400
## 487         Equatorial Guinea 1982     285483    Africa 43.66200
## 488         Equatorial Guinea 1987     341244    Africa 45.66400
## 489         Equatorial Guinea 1992     387838    Africa 47.54500
## 490         Equatorial Guinea 1997     439971    Africa 48.24500
## 491         Equatorial Guinea 2002     495627    Africa 49.34800
## 492         Equatorial Guinea 2007     551201    Africa 51.57900
## 493                   Eritrea 1952    1438760    Africa 35.92800
## 494                   Eritrea 1957    1542611    Africa 38.04700
## 495                   Eritrea 1962    1666618    Africa 40.15800
## 496                   Eritrea 1967    1820319    Africa 42.18900
## 497                   Eritrea 1972    2260187    Africa 44.14200
## 498                   Eritrea 1977    2512642    Africa 44.53500
## 499                   Eritrea 1982    2637297    Africa 43.89000
## 500                   Eritrea 1987    2915959    Africa 46.45300
## 501                   Eritrea 1992    3668440    Africa 49.99100
## 502                   Eritrea 1997    4058319    Africa 53.37800
## 503                   Eritrea 2002    4414865    Africa 55.24000
## 504                   Eritrea 2007    4906585    Africa 58.04000
## 505                  Ethiopia 1952   20860941    Africa 34.07800
## 506                  Ethiopia 1957   22815614    Africa 36.66700
## 507                  Ethiopia 1962   25145372    Africa 40.05900
## 508                  Ethiopia 1967   27860297    Africa 42.11500
## 509                  Ethiopia 1972   30770372    Africa 43.51500
## 510                  Ethiopia 1977   34617799    Africa 44.51000
## 511                  Ethiopia 1982   38111756    Africa 44.91600
## 512                  Ethiopia 1987   42999530    Africa 46.68400
## 513                  Ethiopia 1992   52088559    Africa 48.09100
## 514                  Ethiopia 1997   59861301    Africa 49.40200
## 515                  Ethiopia 2002   67946797    Africa 50.72500
## 516                  Ethiopia 2007   76511887    Africa 52.94700
## 517                   Finland 1952    4090500    Europe 66.55000
## 518                   Finland 1957    4324000    Europe 67.49000
## 519                   Finland 1962    4491443    Europe 68.75000
## 520                   Finland 1967    4605744    Europe 69.83000
## 521                   Finland 1972    4639657    Europe 70.87000
## 522                   Finland 1977    4738902    Europe 72.52000
## 523                   Finland 1982    4826933    Europe 74.55000
## 524                   Finland 1987    4931729    Europe 74.83000
## 525                   Finland 1992    5041039    Europe 75.70000
## 526                   Finland 1997    5134406    Europe 77.13000
## 527                   Finland 2002    5193039    Europe 78.37000
## 528                   Finland 2007    5238460    Europe 79.31300
## 529                    France 1952   42459667    Europe 67.41000
## 530                    France 1957   44310863    Europe 68.93000
## 531                    France 1962   47124000    Europe 70.51000
## 532                    France 1967   49569000    Europe 71.55000
## 533                    France 1972   51732000    Europe 72.38000
## 534                    France 1977   53165019    Europe 73.83000
## 535                    France 1982   54433565    Europe 74.89000
## 536                    France 1987   55630100    Europe 76.34000
## 537                    France 1992   57374179    Europe 77.46000
## 538                    France 1997   58623428    Europe 78.64000
## 539                    France 2002   59925035    Europe 79.59000
## 540                    France 2007   61083916    Europe 80.65700
## 541                     Gabon 1952     420702    Africa 37.00300
## 542                     Gabon 1957     434904    Africa 38.99900
## 543                     Gabon 1962     455661    Africa 40.48900
## 544                     Gabon 1967     489004    Africa 44.59800
## 545                     Gabon 1972     537977    Africa 48.69000
## 546                     Gabon 1977     706367    Africa 52.79000
## 547                     Gabon 1982     753874    Africa 56.56400
## 548                     Gabon 1987     880397    Africa 60.19000
## 549                     Gabon 1992     985739    Africa 61.36600
## 550                     Gabon 1997    1126189    Africa 60.46100
## 551                     Gabon 2002    1299304    Africa 56.76100
## 552                     Gabon 2007    1454867    Africa 56.73500
## 553                    Gambia 1952     284320    Africa 30.00000
## 554                    Gambia 1957     323150    Africa 32.06500
## 555                    Gambia 1962     374020    Africa 33.89600
## 556                    Gambia 1967     439593    Africa 35.85700
## 557                    Gambia 1972     517101    Africa 38.30800
## 558                    Gambia 1977     608274    Africa 41.84200
## 559                    Gambia 1982     715523    Africa 45.58000
## 560                    Gambia 1987     848406    Africa 49.26500
## 561                    Gambia 1992    1025384    Africa 52.64400
## 562                    Gambia 1997    1235767    Africa 55.86100
## 563                    Gambia 2002    1457766    Africa 58.04100
## 564                    Gambia 2007    1688359    Africa 59.44800
## 565                   Germany 1952   69145952    Europe 67.50000
## 566                   Germany 1957   71019069    Europe 69.10000
## 567                   Germany 1962   73739117    Europe 70.30000
## 568                   Germany 1967   76368453    Europe 70.80000
## 569                   Germany 1972   78717088    Europe 71.00000
## 570                   Germany 1977   78160773    Europe 72.50000
## 571                   Germany 1982   78335266    Europe 73.80000
## 572                   Germany 1987   77718298    Europe 74.84700
## 573                   Germany 1992   80597764    Europe 76.07000
## 574                   Germany 1997   82011073    Europe 77.34000
## 575                   Germany 2002   82350671    Europe 78.67000
## 576                   Germany 2007   82400996    Europe 79.40600
## 577                     Ghana 1952    5581001    Africa 43.14900
## 578                     Ghana 1957    6391288    Africa 44.77900
## 579                     Ghana 1962    7355248    Africa 46.45200
## 580                     Ghana 1967    8490213    Africa 48.07200
## 581                     Ghana 1972    9354120    Africa 49.87500
## 582                     Ghana 1977   10538093    Africa 51.75600
## 583                     Ghana 1982   11400338    Africa 53.74400
## 584                     Ghana 1987   14168101    Africa 55.72900
## 585                     Ghana 1992   16278738    Africa 57.50100
## 586                     Ghana 1997   18418288    Africa 58.55600
## 587                     Ghana 2002   20550751    Africa 58.45300
## 588                     Ghana 2007   22873338    Africa 60.02200
## 589                    Greece 1952    7733250    Europe 65.86000
## 590                    Greece 1957    8096218    Europe 67.86000
## 591                    Greece 1962    8448233    Europe 69.51000
## 592                    Greece 1967    8716441    Europe 71.00000
## 593                    Greece 1972    8888628    Europe 72.34000
## 594                    Greece 1977    9308479    Europe 73.68000
## 595                    Greece 1982    9786480    Europe 75.24000
## 596                    Greece 1987    9974490    Europe 76.67000
## 597                    Greece 1992   10325429    Europe 77.03000
## 598                    Greece 1997   10502372    Europe 77.86900
## 599                    Greece 2002   10603863    Europe 78.25600
## 600                    Greece 2007   10706290    Europe 79.48300
## 601                 Guatemala 1952    3146381  Americas 42.02300
## 602                 Guatemala 1957    3640876  Americas 44.14200
## 603                 Guatemala 1962    4208858  Americas 46.95400
## 604                 Guatemala 1967    4690773  Americas 50.01600
## 605                 Guatemala 1972    5149581  Americas 53.73800
## 606                 Guatemala 1977    5703430  Americas 56.02900
## 607                 Guatemala 1982    6395630  Americas 58.13700
## 608                 Guatemala 1987    7326406  Americas 60.78200
## 609                 Guatemala 1992    8486949  Americas 63.37300
## 610                 Guatemala 1997    9803875  Americas 66.32200
## 611                 Guatemala 2002   11178650  Americas 68.97800
## 612                 Guatemala 2007   12572928  Americas 70.25900
## 613                    Guinea 1952    2664249    Africa 33.60900
## 614                    Guinea 1957    2876726    Africa 34.55800
## 615                    Guinea 1962    3140003    Africa 35.75300
## 616                    Guinea 1967    3451418    Africa 37.19700
## 617                    Guinea 1972    3811387    Africa 38.84200
## 618                    Guinea 1977    4227026    Africa 40.76200
## 619                    Guinea 1982    4710497    Africa 42.89100
## 620                    Guinea 1987    5650262    Africa 45.55200
## 621                    Guinea 1992    6990574    Africa 48.57600
## 622                    Guinea 1997    8048834    Africa 51.45500
## 623                    Guinea 2002    8807818    Africa 53.67600
## 624                    Guinea 2007    9947814    Africa 56.00700
## 625             Guinea-Bissau 1952     580653    Africa 32.50000
## 626             Guinea-Bissau 1957     601095    Africa 33.48900
## 627             Guinea-Bissau 1962     627820    Africa 34.48800
## 628             Guinea-Bissau 1967     601287    Africa 35.49200
## 629             Guinea-Bissau 1972     625361    Africa 36.48600
## 630             Guinea-Bissau 1977     745228    Africa 37.46500
## 631             Guinea-Bissau 1982     825987    Africa 39.32700
## 632             Guinea-Bissau 1987     927524    Africa 41.24500
## 633             Guinea-Bissau 1992    1050938    Africa 43.26600
## 634             Guinea-Bissau 1997    1193708    Africa 44.87300
## 635             Guinea-Bissau 2002    1332459    Africa 45.50400
## 636             Guinea-Bissau 2007    1472041    Africa 46.38800
## 637                     Haiti 1952    3201488  Americas 37.57900
## 638                     Haiti 1957    3507701  Americas 40.69600
## 639                     Haiti 1962    3880130  Americas 43.59000
## 640                     Haiti 1967    4318137  Americas 46.24300
## 641                     Haiti 1972    4698301  Americas 48.04200
## 642                     Haiti 1977    4908554  Americas 49.92300
## 643                     Haiti 1982    5198399  Americas 51.46100
## 644                     Haiti 1987    5756203  Americas 53.63600
## 645                     Haiti 1992    6326682  Americas 55.08900
## 646                     Haiti 1997    6913545  Americas 56.67100
## 647                     Haiti 2002    7607651  Americas 58.13700
## 648                     Haiti 2007    8502814  Americas 60.91600
## 649                  Honduras 1952    1517453  Americas 41.91200
## 650                  Honduras 1957    1770390  Americas 44.66500
## 651                  Honduras 1962    2090162  Americas 48.04100
## 652                  Honduras 1967    2500689  Americas 50.92400
## 653                  Honduras 1972    2965146  Americas 53.88400
## 654                  Honduras 1977    3055235  Americas 57.40200
## 655                  Honduras 1982    3669448  Americas 60.90900
## 656                  Honduras 1987    4372203  Americas 64.49200
## 657                  Honduras 1992    5077347  Americas 66.39900
## 658                  Honduras 1997    5867957  Americas 67.65900
## 659                  Honduras 2002    6677328  Americas 68.56500
## 660                  Honduras 2007    7483763  Americas 70.19800
## 661           Hong Kong China 1952    2125900      Asia 60.96000
## 662           Hong Kong China 1957    2736300      Asia 64.75000
## 663           Hong Kong China 1962    3305200      Asia 67.65000
## 664           Hong Kong China 1967    3722800      Asia 70.00000
## 665           Hong Kong China 1972    4115700      Asia 72.00000
## 666           Hong Kong China 1977    4583700      Asia 73.60000
## 667           Hong Kong China 1982    5264500      Asia 75.45000
## 668           Hong Kong China 1987    5584510      Asia 76.20000
## 669           Hong Kong China 1992    5829696      Asia 77.60100
## 670           Hong Kong China 1997    6495918      Asia 80.00000
## 671           Hong Kong China 2002    6762476      Asia 81.49500
## 672           Hong Kong China 2007    6980412      Asia 82.20800
## 673                   Hungary 1952    9504000    Europe 64.03000
## 674                   Hungary 1957    9839000    Europe 66.41000
## 675                   Hungary 1962   10063000    Europe 67.96000
## 676                   Hungary 1967   10223422    Europe 69.50000
## 677                   Hungary 1972   10394091    Europe 69.76000
## 678                   Hungary 1977   10637171    Europe 69.95000
## 679                   Hungary 1982   10705535    Europe 69.39000
## 680                   Hungary 1987   10612740    Europe 69.58000
## 681                   Hungary 1992   10348684    Europe 69.17000
## 682                   Hungary 1997   10244684    Europe 71.04000
## 683                   Hungary 2002   10083313    Europe 72.59000
## 684                   Hungary 2007    9956108    Europe 73.33800
## 685                   Iceland 1952     147962    Europe 72.49000
## 686                   Iceland 1957     165110    Europe 73.47000
## 687                   Iceland 1962     182053    Europe 73.68000
## 688                   Iceland 1967     198676    Europe 73.73000
## 689                   Iceland 1972     209275    Europe 74.46000
## 690                   Iceland 1977     221823    Europe 76.11000
## 691                   Iceland 1982     233997    Europe 76.99000
## 692                   Iceland 1987     244676    Europe 77.23000
## 693                   Iceland 1992     259012    Europe 78.77000
## 694                   Iceland 1997     271192    Europe 78.95000
## 695                   Iceland 2002     288030    Europe 80.50000
## 696                   Iceland 2007     301931    Europe 81.75700
## 697                     India 1952  372000000      Asia 37.37300
## 698                     India 1957  409000000      Asia 40.24900
## 699                     India 1962  454000000      Asia 43.60500
## 700                     India 1967  506000000      Asia 47.19300
## 701                     India 1972  567000000      Asia 50.65100
## 702                     India 1977  634000000      Asia 54.20800
## 703                     India 1982  708000000      Asia 56.59600
## 704                     India 1987  788000000      Asia 58.55300
## 705                     India 1992  872000000      Asia 60.22300
## 706                     India 1997  959000000      Asia 61.76500
## 707                     India 2002 1034172547      Asia 62.87900
## 708                     India 2007 1110396331      Asia 64.69800
## 709                 Indonesia 1952   82052000      Asia 37.46800
## 710                 Indonesia 1957   90124000      Asia 39.91800
## 711                 Indonesia 1962   99028000      Asia 42.51800
## 712                 Indonesia 1967  109343000      Asia 45.96400
## 713                 Indonesia 1972  121282000      Asia 49.20300
## 714                 Indonesia 1977  136725000      Asia 52.70200
## 715                 Indonesia 1982  153343000      Asia 56.15900
## 716                 Indonesia 1987  169276000      Asia 60.13700
## 717                 Indonesia 1992  184816000      Asia 62.68100
## 718                 Indonesia 1997  199278000      Asia 66.04100
## 719                 Indonesia 2002  211060000      Asia 68.58800
## 720                 Indonesia 2007  223547000      Asia 70.65000
## 721                      Iran 1952   17272000      Asia 44.86900
## 722                      Iran 1957   19792000      Asia 47.18100
## 723                      Iran 1962   22874000      Asia 49.32500
## 724                      Iran 1967   26538000      Asia 52.46900
## 725                      Iran 1972   30614000      Asia 55.23400
## 726                      Iran 1977   35480679      Asia 57.70200
## 727                      Iran 1982   43072751      Asia 59.62000
## 728                      Iran 1987   51889696      Asia 63.04000
## 729                      Iran 1992   60397973      Asia 65.74200
## 730                      Iran 1997   63327987      Asia 68.04200
## 731                      Iran 2002   66907826      Asia 69.45100
## 732                      Iran 2007   69453570      Asia 70.96400
## 733                      Iraq 1952    5441766      Asia 45.32000
## 734                      Iraq 1957    6248643      Asia 48.43700
## 735                      Iraq 1962    7240260      Asia 51.45700
## 736                      Iraq 1967    8519282      Asia 54.45900
## 737                      Iraq 1972   10061506      Asia 56.95000
## 738                      Iraq 1977   11882916      Asia 60.41300
## 739                      Iraq 1982   14173318      Asia 62.03800
## 740                      Iraq 1987   16543189      Asia 65.04400
## 741                      Iraq 1992   17861905      Asia 59.46100
## 742                      Iraq 1997   20775703      Asia 58.81100
## 743                      Iraq 2002   24001816      Asia 57.04600
## 744                      Iraq 2007   27499638      Asia 59.54500
## 745                   Ireland 1952    2952156    Europe 66.91000
## 746                   Ireland 1957    2878220    Europe 68.90000
## 747                   Ireland 1962    2830000    Europe 70.29000
## 748                   Ireland 1967    2900100    Europe 71.08000
## 749                   Ireland 1972    3024400    Europe 71.28000
## 750                   Ireland 1977    3271900    Europe 72.03000
## 751                   Ireland 1982    3480000    Europe 73.10000
## 752                   Ireland 1987    3539900    Europe 74.36000
## 753                   Ireland 1992    3557761    Europe 75.46700
## 754                   Ireland 1997    3667233    Europe 76.12200
## 755                   Ireland 2002    3879155    Europe 77.78300
## 756                   Ireland 2007    4109086    Europe 78.88500
## 757                    Israel 1952    1620914      Asia 65.39000
## 758                    Israel 1957    1944401      Asia 67.84000
## 759                    Israel 1962    2310904      Asia 69.39000
## 760                    Israel 1967    2693585      Asia 70.75000
## 761                    Israel 1972    3095893      Asia 71.63000
## 762                    Israel 1977    3495918      Asia 73.06000
## 763                    Israel 1982    3858421      Asia 74.45000
## 764                    Israel 1987    4203148      Asia 75.60000
## 765                    Israel 1992    4936550      Asia 76.93000
## 766                    Israel 1997    5531387      Asia 78.26900
## 767                    Israel 2002    6029529      Asia 79.69600
## 768                    Israel 2007    6426679      Asia 80.74500
## 769                     Italy 1952   47666000    Europe 65.94000
## 770                     Italy 1957   49182000    Europe 67.81000
## 771                     Italy 1962   50843200    Europe 69.24000
## 772                     Italy 1967   52667100    Europe 71.06000
## 773                     Italy 1972   54365564    Europe 72.19000
## 774                     Italy 1977   56059245    Europe 73.48000
## 775                     Italy 1982   56535636    Europe 74.98000
## 776                     Italy 1987   56729703    Europe 76.42000
## 777                     Italy 1992   56840847    Europe 77.44000
## 778                     Italy 1997   57479469    Europe 78.82000
## 779                     Italy 2002   57926999    Europe 80.24000
## 780                     Italy 2007   58147733    Europe 80.54600
## 781                   Jamaica 1952    1426095  Americas 58.53000
## 782                   Jamaica 1957    1535090  Americas 62.61000
## 783                   Jamaica 1962    1665128  Americas 65.61000
## 784                   Jamaica 1967    1861096  Americas 67.51000
## 785                   Jamaica 1972    1997616  Americas 69.00000
## 786                   Jamaica 1977    2156814  Americas 70.11000
## 787                   Jamaica 1982    2298309  Americas 71.21000
## 788                   Jamaica 1987    2326606  Americas 71.77000
## 789                   Jamaica 1992    2378618  Americas 71.76600
## 790                   Jamaica 1997    2531311  Americas 72.26200
## 791                   Jamaica 2002    2664659  Americas 72.04700
## 792                   Jamaica 2007    2780132  Americas 72.56700
## 793                     Japan 1952   86459025      Asia 63.03000
## 794                     Japan 1957   91563009      Asia 65.50000
## 795                     Japan 1962   95831757      Asia 68.73000
## 796                     Japan 1967  100825279      Asia 71.43000
## 797                     Japan 1972  107188273      Asia 73.42000
## 798                     Japan 1977  113872473      Asia 75.38000
## 799                     Japan 1982  118454974      Asia 77.11000
## 800                     Japan 1987  122091325      Asia 78.67000
## 801                     Japan 1992  124329269      Asia 79.36000
## 802                     Japan 1997  125956499      Asia 80.69000
## 803                     Japan 2002  127065841      Asia 82.00000
## 804                     Japan 2007  127467972      Asia 82.60300
## 805                    Jordan 1952     607914      Asia 43.15800
## 806                    Jordan 1957     746559      Asia 45.66900
## 807                    Jordan 1962     933559      Asia 48.12600
## 808                    Jordan 1967    1255058      Asia 51.62900
## 809                    Jordan 1972    1613551      Asia 56.52800
## 810                    Jordan 1977    1937652      Asia 61.13400
## 811                    Jordan 1982    2347031      Asia 63.73900
## 812                    Jordan 1987    2820042      Asia 65.86900
## 813                    Jordan 1992    3867409      Asia 68.01500
## 814                    Jordan 1997    4526235      Asia 69.77200
## 815                    Jordan 2002    5307470      Asia 71.26300
## 816                    Jordan 2007    6053193      Asia 72.53500
## 817                     Kenya 1952    6464046    Africa 42.27000
## 818                     Kenya 1957    7454779    Africa 44.68600
## 819                     Kenya 1962    8678557    Africa 47.94900
## 820                     Kenya 1967   10191512    Africa 50.65400
## 821                     Kenya 1972   12044785    Africa 53.55900
## 822                     Kenya 1977   14500404    Africa 56.15500
## 823                     Kenya 1982   17661452    Africa 58.76600
## 824                     Kenya 1987   21198082    Africa 59.33900
## 825                     Kenya 1992   25020539    Africa 59.28500
## 826                     Kenya 1997   28263827    Africa 54.40700
## 827                     Kenya 2002   31386842    Africa 50.99200
## 828                     Kenya 2007   35610177    Africa 54.11000
## 829           Korea Dem. Rep. 1952    8865488      Asia 50.05600
## 830           Korea Dem. Rep. 1957    9411381      Asia 54.08100
## 831           Korea Dem. Rep. 1962   10917494      Asia 56.65600
## 832           Korea Dem. Rep. 1967   12617009      Asia 59.94200
## 833           Korea Dem. Rep. 1972   14781241      Asia 63.98300
## 834           Korea Dem. Rep. 1977   16325320      Asia 67.15900
## 835           Korea Dem. Rep. 1982   17647518      Asia 69.10000
## 836           Korea Dem. Rep. 1987   19067554      Asia 70.64700
## 837           Korea Dem. Rep. 1992   20711375      Asia 69.97800
## 838           Korea Dem. Rep. 1997   21585105      Asia 67.72700
## 839           Korea Dem. Rep. 2002   22215365      Asia 66.66200
## 840           Korea Dem. Rep. 2007   23301725      Asia 67.29700
## 841                Korea Rep. 1952   20947571      Asia 47.45300
## 842                Korea Rep. 1957   22611552      Asia 52.68100
## 843                Korea Rep. 1962   26420307      Asia 55.29200
## 844                Korea Rep. 1967   30131000      Asia 57.71600
## 845                Korea Rep. 1972   33505000      Asia 62.61200
## 846                Korea Rep. 1977   36436000      Asia 64.76600
## 847                Korea Rep. 1982   39326000      Asia 67.12300
## 848                Korea Rep. 1987   41622000      Asia 69.81000
## 849                Korea Rep. 1992   43805450      Asia 72.24400
## 850                Korea Rep. 1997   46173816      Asia 74.64700
## 851                Korea Rep. 2002   47969150      Asia 77.04500
## 852                Korea Rep. 2007   49044790      Asia 78.62300
## 853                    Kuwait 1952     160000      Asia 55.56500
## 854                    Kuwait 1957     212846      Asia 58.03300
## 855                    Kuwait 1962     358266      Asia 60.47000
## 856                    Kuwait 1967     575003      Asia 64.62400
## 857                    Kuwait 1972     841934      Asia 67.71200
## 858                    Kuwait 1977    1140357      Asia 69.34300
## 859                    Kuwait 1982    1497494      Asia 71.30900
## 860                    Kuwait 1987    1891487      Asia 74.17400
## 861                    Kuwait 1992    1418095      Asia 75.19000
## 862                    Kuwait 1997    1765345      Asia 76.15600
## 863                    Kuwait 2002    2111561      Asia 76.90400
## 864                    Kuwait 2007    2505559      Asia 77.58800
## 865                   Lebanon 1952    1439529      Asia 55.92800
## 866                   Lebanon 1957    1647412      Asia 59.48900
## 867                   Lebanon 1962    1886848      Asia 62.09400
## 868                   Lebanon 1967    2186894      Asia 63.87000
## 869                   Lebanon 1972    2680018      Asia 65.42100
## 870                   Lebanon 1977    3115787      Asia 66.09900
## 871                   Lebanon 1982    3086876      Asia 66.98300
## 872                   Lebanon 1987    3089353      Asia 67.92600
## 873                   Lebanon 1992    3219994      Asia 69.29200
## 874                   Lebanon 1997    3430388      Asia 70.26500
## 875                   Lebanon 2002    3677780      Asia 71.02800
## 876                   Lebanon 2007    3921278      Asia 71.99300
## 877                   Lesotho 1952     748747    Africa 42.13800
## 878                   Lesotho 1957     813338    Africa 45.04700
## 879                   Lesotho 1962     893143    Africa 47.74700
## 880                   Lesotho 1967     996380    Africa 48.49200
## 881                   Lesotho 1972    1116779    Africa 49.76700
## 882                   Lesotho 1977    1251524    Africa 52.20800
## 883                   Lesotho 1982    1411807    Africa 55.07800
## 884                   Lesotho 1987    1599200    Africa 57.18000
## 885                   Lesotho 1992    1803195    Africa 59.68500
## 886                   Lesotho 1997    1982823    Africa 55.55800
## 887                   Lesotho 2002    2046772    Africa 44.59300
## 888                   Lesotho 2007    2012649    Africa 42.59200
## 889                   Liberia 1952     863308    Africa 38.48000
## 890                   Liberia 1957     975950    Africa 39.48600
## 891                   Liberia 1962    1112796    Africa 40.50200
## 892                   Liberia 1967    1279406    Africa 41.53600
## 893                   Liberia 1972    1482628    Africa 42.61400
## 894                   Liberia 1977    1703617    Africa 43.76400
## 895                   Liberia 1982    1956875    Africa 44.85200
## 896                   Liberia 1987    2269414    Africa 46.02700
## 897                   Liberia 1992    1912974    Africa 40.80200
## 898                   Liberia 1997    2200725    Africa 42.22100
## 899                   Liberia 2002    2814651    Africa 43.75300
## 900                   Liberia 2007    3193942    Africa 45.67800
## 901                     Libya 1952    1019729    Africa 42.72300
## 902                     Libya 1957    1201578    Africa 45.28900
## 903                     Libya 1962    1441863    Africa 47.80800
## 904                     Libya 1967    1759224    Africa 50.22700
## 905                     Libya 1972    2183877    Africa 52.77300
## 906                     Libya 1977    2721783    Africa 57.44200
## 907                     Libya 1982    3344074    Africa 62.15500
## 908                     Libya 1987    3799845    Africa 66.23400
## 909                     Libya 1992    4364501    Africa 68.75500
## 910                     Libya 1997    4759670    Africa 71.55500
## 911                     Libya 2002    5368585    Africa 72.73700
## 912                     Libya 2007    6036914    Africa 73.95200
## 913                Madagascar 1952    4762912    Africa 36.68100
## 914                Madagascar 1957    5181679    Africa 38.86500
## 915                Madagascar 1962    5703324    Africa 40.84800
## 916                Madagascar 1967    6334556    Africa 42.88100
## 917                Madagascar 1972    7082430    Africa 44.85100
## 918                Madagascar 1977    8007166    Africa 46.88100
## 919                Madagascar 1982    9171477    Africa 48.96900
## 920                Madagascar 1987   10568642    Africa 49.35000
## 921                Madagascar 1992   12210395    Africa 52.21400
## 922                Madagascar 1997   14165114    Africa 54.97800
## 923                Madagascar 2002   16473477    Africa 57.28600
## 924                Madagascar 2007   19167654    Africa 59.44300
## 925                    Malawi 1952    2917802    Africa 36.25600
## 926                    Malawi 1957    3221238    Africa 37.20700
## 927                    Malawi 1962    3628608    Africa 38.41000
## 928                    Malawi 1967    4147252    Africa 39.48700
## 929                    Malawi 1972    4730997    Africa 41.76600
## 930                    Malawi 1977    5637246    Africa 43.76700
## 931                    Malawi 1982    6502825    Africa 45.64200
## 932                    Malawi 1987    7824747    Africa 47.45700
## 933                    Malawi 1992   10014249    Africa 49.42000
## 934                    Malawi 1997   10419991    Africa 47.49500
## 935                    Malawi 2002   11824495    Africa 45.00900
## 936                    Malawi 2007   13327079    Africa 48.30300
## 937                  Malaysia 1952    6748378      Asia 48.46300
## 938                  Malaysia 1957    7739235      Asia 52.10200
## 939                  Malaysia 1962    8906385      Asia 55.73700
## 940                  Malaysia 1967   10154878      Asia 59.37100
## 941                  Malaysia 1972   11441462      Asia 63.01000
## 942                  Malaysia 1977   12845381      Asia 65.25600
## 943                  Malaysia 1982   14441916      Asia 68.00000
## 944                  Malaysia 1987   16331785      Asia 69.50000
## 945                  Malaysia 1992   18319502      Asia 70.69300
## 946                  Malaysia 1997   20476091      Asia 71.93800
## 947                  Malaysia 2002   22662365      Asia 73.04400
## 948                  Malaysia 2007   24821286      Asia 74.24100
## 949                      Mali 1952    3838168    Africa 33.68500
## 950                      Mali 1957    4241884    Africa 35.30700
## 951                      Mali 1962    4690372    Africa 36.93600
## 952                      Mali 1967    5212416    Africa 38.48700
## 953                      Mali 1972    5828158    Africa 39.97700
## 954                      Mali 1977    6491649    Africa 41.71400
## 955                      Mali 1982    6998256    Africa 43.91600
## 956                      Mali 1987    7634008    Africa 46.36400
## 957                      Mali 1992    8416215    Africa 48.38800
## 958                      Mali 1997    9384984    Africa 49.90300
## 959                      Mali 2002   10580176    Africa 51.81800
## 960                      Mali 2007   12031795    Africa 54.46700
## 961                Mauritania 1952    1022556    Africa 40.54300
## 962                Mauritania 1957    1076852    Africa 42.33800
## 963                Mauritania 1962    1146757    Africa 44.24800
## 964                Mauritania 1967    1230542    Africa 46.28900
## 965                Mauritania 1972    1332786    Africa 48.43700
## 966                Mauritania 1977    1456688    Africa 50.85200
## 967                Mauritania 1982    1622136    Africa 53.59900
## 968                Mauritania 1987    1841240    Africa 56.14500
## 969                Mauritania 1992    2119465    Africa 58.33300
## 970                Mauritania 1997    2444741    Africa 60.43000
## 971                Mauritania 2002    2828858    Africa 62.24700
## 972                Mauritania 2007    3270065    Africa 64.16400
## 973                 Mauritius 1952     516556    Africa 50.98600
## 974                 Mauritius 1957     609816    Africa 58.08900
## 975                 Mauritius 1962     701016    Africa 60.24600
## 976                 Mauritius 1967     789309    Africa 61.55700
## 977                 Mauritius 1972     851334    Africa 62.94400
## 978                 Mauritius 1977     913025    Africa 64.93000
## 979                 Mauritius 1982     992040    Africa 66.71100
## 980                 Mauritius 1987    1042663    Africa 68.74000
## 981                 Mauritius 1992    1096202    Africa 69.74500
## 982                 Mauritius 1997    1149818    Africa 70.73600
## 983                 Mauritius 2002    1200206    Africa 71.95400
## 984                 Mauritius 2007    1250882    Africa 72.80100
## 985                    Mexico 1952   30144317  Americas 50.78900
## 986                    Mexico 1957   35015548  Americas 55.19000
## 987                    Mexico 1962   41121485  Americas 58.29900
## 988                    Mexico 1967   47995559  Americas 60.11000
## 989                    Mexico 1972   55984294  Americas 62.36100
## 990                    Mexico 1977   63759976  Americas 65.03200
## 991                    Mexico 1982   71640904  Americas 67.40500
## 992                    Mexico 1987   80122492  Americas 69.49800
## 993                    Mexico 1992   88111030  Americas 71.45500
## 994                    Mexico 1997   95895146  Americas 73.67000
## 995                    Mexico 2002  102479927  Americas 74.90200
## 996                    Mexico 2007  108700891  Americas 76.19500
## 997                  Mongolia 1952     800663      Asia 42.24400
## 998                  Mongolia 1957     882134      Asia 45.24800
## 999                  Mongolia 1962    1010280      Asia 48.25100
## 1000                 Mongolia 1967    1149500      Asia 51.25300
## 1001                 Mongolia 1972    1320500      Asia 53.75400
## 1002                 Mongolia 1977    1528000      Asia 55.49100
## 1003                 Mongolia 1982    1756032      Asia 57.48900
## 1004                 Mongolia 1987    2015133      Asia 60.22200
## 1005                 Mongolia 1992    2312802      Asia 61.27100
## 1006                 Mongolia 1997    2494803      Asia 63.62500
## 1007                 Mongolia 2002    2674234      Asia 65.03300
## 1008                 Mongolia 2007    2874127      Asia 66.80300
## 1009               Montenegro 1952     413834    Europe 59.16400
## 1010               Montenegro 1957     442829    Europe 61.44800
## 1011               Montenegro 1962     474528    Europe 63.72800
## 1012               Montenegro 1967     501035    Europe 67.17800
## 1013               Montenegro 1972     527678    Europe 70.63600
## 1014               Montenegro 1977     560073    Europe 73.06600
## 1015               Montenegro 1982     562548    Europe 74.10100
## 1016               Montenegro 1987     569473    Europe 74.86500
## 1017               Montenegro 1992     621621    Europe 75.43500
## 1018               Montenegro 1997     692651    Europe 75.44500
## 1019               Montenegro 2002     720230    Europe 73.98100
## 1020               Montenegro 2007     684736    Europe 74.54300
## 1021                  Morocco 1952    9939217    Africa 42.87300
## 1022                  Morocco 1957   11406350    Africa 45.42300
## 1023                  Morocco 1962   13056604    Africa 47.92400
## 1024                  Morocco 1967   14770296    Africa 50.33500
## 1025                  Morocco 1972   16660670    Africa 52.86200
## 1026                  Morocco 1977   18396941    Africa 55.73000
## 1027                  Morocco 1982   20198730    Africa 59.65000
## 1028                  Morocco 1987   22987397    Africa 62.67700
## 1029                  Morocco 1992   25798239    Africa 65.39300
## 1030                  Morocco 1997   28529501    Africa 67.66000
## 1031                  Morocco 2002   31167783    Africa 69.61500
## 1032                  Morocco 2007   33757175    Africa 71.16400
## 1033               Mozambique 1952    6446316    Africa 31.28600
## 1034               Mozambique 1957    7038035    Africa 33.77900
## 1035               Mozambique 1962    7788944    Africa 36.16100
## 1036               Mozambique 1967    8680909    Africa 38.11300
## 1037               Mozambique 1972    9809596    Africa 40.32800
## 1038               Mozambique 1977   11127868    Africa 42.49500
## 1039               Mozambique 1982   12587223    Africa 42.79500
## 1040               Mozambique 1987   12891952    Africa 42.86100
## 1041               Mozambique 1992   13160731    Africa 44.28400
## 1042               Mozambique 1997   16603334    Africa 46.34400
## 1043               Mozambique 2002   18473780    Africa 44.02600
## 1044               Mozambique 2007   19951656    Africa 42.08200
## 1045                  Myanmar 1952   20092996      Asia 36.31900
## 1046                  Myanmar 1957   21731844      Asia 41.90500
## 1047                  Myanmar 1962   23634436      Asia 45.10800
## 1048                  Myanmar 1967   25870271      Asia 49.37900
## 1049                  Myanmar 1972   28466390      Asia 53.07000
## 1050                  Myanmar 1977   31528087      Asia 56.05900
## 1051                  Myanmar 1982   34680442      Asia 58.05600
## 1052                  Myanmar 1987   38028578      Asia 58.33900
## 1053                  Myanmar 1992   40546538      Asia 59.32000
## 1054                  Myanmar 1997   43247867      Asia 60.32800
## 1055                  Myanmar 2002   45598081      Asia 59.90800
## 1056                  Myanmar 2007   47761980      Asia 62.06900
## 1057                  Namibia 1952     485831    Africa 41.72500
## 1058                  Namibia 1957     548080    Africa 45.22600
## 1059                  Namibia 1962     621392    Africa 48.38600
## 1060                  Namibia 1967     706640    Africa 51.15900
## 1061                  Namibia 1972     821782    Africa 53.86700
## 1062                  Namibia 1977     977026    Africa 56.43700
## 1063                  Namibia 1982    1099010    Africa 58.96800
## 1064                  Namibia 1987    1278184    Africa 60.83500
## 1065                  Namibia 1992    1554253    Africa 61.99900
## 1066                  Namibia 1997    1774766    Africa 58.90900
## 1067                  Namibia 2002    1972153    Africa 51.47900
## 1068                  Namibia 2007    2055080    Africa 52.90600
## 1069                    Nepal 1952    9182536      Asia 36.15700
## 1070                    Nepal 1957    9682338      Asia 37.68600
## 1071                    Nepal 1962   10332057      Asia 39.39300
## 1072                    Nepal 1967   11261690      Asia 41.47200
## 1073                    Nepal 1972   12412593      Asia 43.97100
## 1074                    Nepal 1977   13933198      Asia 46.74800
## 1075                    Nepal 1982   15796314      Asia 49.59400
## 1076                    Nepal 1987   17917180      Asia 52.53700
## 1077                    Nepal 1992   20326209      Asia 55.72700
## 1078                    Nepal 1997   23001113      Asia 59.42600
## 1079                    Nepal 2002   25873917      Asia 61.34000
## 1080                    Nepal 2007   28901790      Asia 63.78500
## 1081              Netherlands 1952   10381988    Europe 72.13000
## 1082              Netherlands 1957   11026383    Europe 72.99000
## 1083              Netherlands 1962   11805689    Europe 73.23000
## 1084              Netherlands 1967   12596822    Europe 73.82000
## 1085              Netherlands 1972   13329874    Europe 73.75000
## 1086              Netherlands 1977   13852989    Europe 75.24000
## 1087              Netherlands 1982   14310401    Europe 76.05000
## 1088              Netherlands 1987   14665278    Europe 76.83000
## 1089              Netherlands 1992   15174244    Europe 77.42000
## 1090              Netherlands 1997   15604464    Europe 78.03000
## 1091              Netherlands 2002   16122830    Europe 78.53000
## 1092              Netherlands 2007   16570613    Europe 79.76200
## 1093              New Zealand 1952    1994794   Oceania 69.39000
## 1094              New Zealand 1957    2229407   Oceania 70.26000
## 1095              New Zealand 1962    2488550   Oceania 71.24000
## 1096              New Zealand 1967    2728150   Oceania 71.52000
## 1097              New Zealand 1972    2929100   Oceania 71.89000
## 1098              New Zealand 1977    3164900   Oceania 72.22000
## 1099              New Zealand 1982    3210650   Oceania 73.84000
## 1100              New Zealand 1987    3317166   Oceania 74.32000
## 1101              New Zealand 1992    3437674   Oceania 76.33000
## 1102              New Zealand 1997    3676187   Oceania 77.55000
## 1103              New Zealand 2002    3908037   Oceania 79.11000
## 1104              New Zealand 2007    4115771   Oceania 80.20400
## 1105                Nicaragua 1952    1165790  Americas 42.31400
## 1106                Nicaragua 1957    1358828  Americas 45.43200
## 1107                Nicaragua 1962    1590597  Americas 48.63200
## 1108                Nicaragua 1967    1865490  Americas 51.88400
## 1109                Nicaragua 1972    2182908  Americas 55.15100
## 1110                Nicaragua 1977    2554598  Americas 57.47000
## 1111                Nicaragua 1982    2979423  Americas 59.29800
## 1112                Nicaragua 1987    3344353  Americas 62.00800
## 1113                Nicaragua 1992    4017939  Americas 65.84300
## 1114                Nicaragua 1997    4609572  Americas 68.42600
## 1115                Nicaragua 2002    5146848  Americas 70.83600
## 1116                Nicaragua 2007    5675356  Americas 72.89900
## 1117                    Niger 1952    3379468    Africa 37.44400
## 1118                    Niger 1957    3692184    Africa 38.59800
## 1119                    Niger 1962    4076008    Africa 39.48700
## 1120                    Niger 1967    4534062    Africa 40.11800
## 1121                    Niger 1972    5060262    Africa 40.54600
## 1122                    Niger 1977    5682086    Africa 41.29100
## 1123                    Niger 1982    6437188    Africa 42.59800
## 1124                    Niger 1987    7332638    Africa 44.55500
## 1125                    Niger 1992    8392818    Africa 47.39100
## 1126                    Niger 1997    9666252    Africa 51.31300
## 1127                    Niger 2002   11140655    Africa 54.49600
## 1128                    Niger 2007   12894865    Africa 56.86700
## 1129                  Nigeria 1952   33119096    Africa 36.32400
## 1130                  Nigeria 1957   37173340    Africa 37.80200
## 1131                  Nigeria 1962   41871351    Africa 39.36000
## 1132                  Nigeria 1967   47287752    Africa 41.04000
## 1133                  Nigeria 1972   53740085    Africa 42.82100
## 1134                  Nigeria 1977   62209173    Africa 44.51400
## 1135                  Nigeria 1982   73039376    Africa 45.82600
## 1136                  Nigeria 1987   81551520    Africa 46.88600
## 1137                  Nigeria 1992   93364244    Africa 47.47200
## 1138                  Nigeria 1997  106207839    Africa 47.46400
## 1139                  Nigeria 2002  119901274    Africa 46.60800
## 1140                  Nigeria 2007  135031164    Africa 46.85900
## 1141                   Norway 1952    3327728    Europe 72.67000
## 1142                   Norway 1957    3491938    Europe 73.44000
## 1143                   Norway 1962    3638919    Europe 73.47000
## 1144                   Norway 1967    3786019    Europe 74.08000
## 1145                   Norway 1972    3933004    Europe 74.34000
## 1146                   Norway 1977    4043205    Europe 75.37000
## 1147                   Norway 1982    4114787    Europe 75.97000
## 1148                   Norway 1987    4186147    Europe 75.89000
## 1149                   Norway 1992    4286357    Europe 77.32000
## 1150                   Norway 1997    4405672    Europe 78.32000
## 1151                   Norway 2002    4535591    Europe 79.05000
## 1152                   Norway 2007    4627926    Europe 80.19600
## 1153                     Oman 1952     507833      Asia 37.57800
## 1154                     Oman 1957     561977      Asia 40.08000
## 1155                     Oman 1962     628164      Asia 43.16500
## 1156                     Oman 1967     714775      Asia 46.98800
## 1157                     Oman 1972     829050      Asia 52.14300
## 1158                     Oman 1977    1004533      Asia 57.36700
## 1159                     Oman 1982    1301048      Asia 62.72800
## 1160                     Oman 1987    1593882      Asia 67.73400
## 1161                     Oman 1992    1915208      Asia 71.19700
## 1162                     Oman 1997    2283635      Asia 72.49900
## 1163                     Oman 2002    2713462      Asia 74.19300
## 1164                     Oman 2007    3204897      Asia 75.64000
## 1165                 Pakistan 1952   41346560      Asia 43.43600
## 1166                 Pakistan 1957   46679944      Asia 45.55700
## 1167                 Pakistan 1962   53100671      Asia 47.67000
## 1168                 Pakistan 1967   60641899      Asia 49.80000
## 1169                 Pakistan 1972   69325921      Asia 51.92900
## 1170                 Pakistan 1977   78152686      Asia 54.04300
## 1171                 Pakistan 1982   91462088      Asia 56.15800
## 1172                 Pakistan 1987  105186881      Asia 58.24500
## 1173                 Pakistan 1992  120065004      Asia 60.83800
## 1174                 Pakistan 1997  135564834      Asia 61.81800
## 1175                 Pakistan 2002  153403524      Asia 63.61000
## 1176                 Pakistan 2007  169270617      Asia 65.48300
## 1177                   Panama 1952     940080  Americas 55.19100
## 1178                   Panama 1957    1063506  Americas 59.20100
## 1179                   Panama 1962    1215725  Americas 61.81700
## 1180                   Panama 1967    1405486  Americas 64.07100
## 1181                   Panama 1972    1616384  Americas 66.21600
## 1182                   Panama 1977    1839782  Americas 68.68100
## 1183                   Panama 1982    2036305  Americas 70.47200
## 1184                   Panama 1987    2253639  Americas 71.52300
## 1185                   Panama 1992    2484997  Americas 72.46200
## 1186                   Panama 1997    2734531  Americas 73.73800
## 1187                   Panama 2002    2990875  Americas 74.71200
## 1188                   Panama 2007    3242173  Americas 75.53700
## 1189                 Paraguay 1952    1555876  Americas 62.64900
## 1190                 Paraguay 1957    1770902  Americas 63.19600
## 1191                 Paraguay 1962    2009813  Americas 64.36100
## 1192                 Paraguay 1967    2287985  Americas 64.95100
## 1193                 Paraguay 1972    2614104  Americas 65.81500
## 1194                 Paraguay 1977    2984494  Americas 66.35300
## 1195                 Paraguay 1982    3366439  Americas 66.87400
## 1196                 Paraguay 1987    3886512  Americas 67.37800
## 1197                 Paraguay 1992    4483945  Americas 68.22500
## 1198                 Paraguay 1997    5154123  Americas 69.40000
## 1199                 Paraguay 2002    5884491  Americas 70.75500
## 1200                 Paraguay 2007    6667147  Americas 71.75200
## 1201                     Peru 1952    8025700  Americas 43.90200
## 1202                     Peru 1957    9146100  Americas 46.26300
## 1203                     Peru 1962   10516500  Americas 49.09600
## 1204                     Peru 1967   12132200  Americas 51.44500
## 1205                     Peru 1972   13954700  Americas 55.44800
## 1206                     Peru 1977   15990099  Americas 58.44700
## 1207                     Peru 1982   18125129  Americas 61.40600
## 1208                     Peru 1987   20195924  Americas 64.13400
## 1209                     Peru 1992   22430449  Americas 66.45800
## 1210                     Peru 1997   24748122  Americas 68.38600
## 1211                     Peru 2002   26769436  Americas 69.90600
## 1212                     Peru 2007   28674757  Americas 71.42100
## 1213              Philippines 1952   22438691      Asia 47.75200
## 1214              Philippines 1957   26072194      Asia 51.33400
## 1215              Philippines 1962   30325264      Asia 54.75700
## 1216              Philippines 1967   35356600      Asia 56.39300
## 1217              Philippines 1972   40850141      Asia 58.06500
## 1218              Philippines 1977   46850962      Asia 60.06000
## 1219              Philippines 1982   53456774      Asia 62.08200
## 1220              Philippines 1987   60017788      Asia 64.15100
## 1221              Philippines 1992   67185766      Asia 66.45800
## 1222              Philippines 1997   75012988      Asia 68.56400
## 1223              Philippines 2002   82995088      Asia 70.30300
## 1224              Philippines 2007   91077287      Asia 71.68800
## 1225                   Poland 1952   25730551    Europe 61.31000
## 1226                   Poland 1957   28235346    Europe 65.77000
## 1227                   Poland 1962   30329617    Europe 67.64000
## 1228                   Poland 1967   31785378    Europe 69.61000
## 1229                   Poland 1972   33039545    Europe 70.85000
## 1230                   Poland 1977   34621254    Europe 70.67000
## 1231                   Poland 1982   36227381    Europe 71.32000
## 1232                   Poland 1987   37740710    Europe 70.98000
## 1233                   Poland 1992   38370697    Europe 70.99000
## 1234                   Poland 1997   38654957    Europe 72.75000
## 1235                   Poland 2002   38625976    Europe 74.67000
## 1236                   Poland 2007   38518241    Europe 75.56300
## 1237                 Portugal 1952    8526050    Europe 59.82000
## 1238                 Portugal 1957    8817650    Europe 61.51000
## 1239                 Portugal 1962    9019800    Europe 64.39000
## 1240                 Portugal 1967    9103000    Europe 66.60000
## 1241                 Portugal 1972    8970450    Europe 69.26000
## 1242                 Portugal 1977    9662600    Europe 70.41000
## 1243                 Portugal 1982    9859650    Europe 72.77000
## 1244                 Portugal 1987    9915289    Europe 74.06000
## 1245                 Portugal 1992    9927680    Europe 74.86000
## 1246                 Portugal 1997   10156415    Europe 75.97000
## 1247                 Portugal 2002   10433867    Europe 77.29000
## 1248                 Portugal 2007   10642836    Europe 78.09800
## 1249              Puerto Rico 1952    2227000  Americas 64.28000
## 1250              Puerto Rico 1957    2260000  Americas 68.54000
## 1251              Puerto Rico 1962    2448046  Americas 69.62000
## 1252              Puerto Rico 1967    2648961  Americas 71.10000
## 1253              Puerto Rico 1972    2847132  Americas 72.16000
## 1254              Puerto Rico 1977    3080828  Americas 73.44000
## 1255              Puerto Rico 1982    3279001  Americas 73.75000
## 1256              Puerto Rico 1987    3444468  Americas 74.63000
## 1257              Puerto Rico 1992    3585176  Americas 73.91100
## 1258              Puerto Rico 1997    3759430  Americas 74.91700
## 1259              Puerto Rico 2002    3859606  Americas 77.77800
## 1260              Puerto Rico 2007    3942491  Americas 78.74600
## 1261                  Reunion 1952     257700    Africa 52.72400
## 1262                  Reunion 1957     308700    Africa 55.09000
## 1263                  Reunion 1962     358900    Africa 57.66600
## 1264                  Reunion 1967     414024    Africa 60.54200
## 1265                  Reunion 1972     461633    Africa 64.27400
## 1266                  Reunion 1977     492095    Africa 67.06400
## 1267                  Reunion 1982     517810    Africa 69.88500
## 1268                  Reunion 1987     562035    Africa 71.91300
## 1269                  Reunion 1992     622191    Africa 73.61500
## 1270                  Reunion 1997     684810    Africa 74.77200
## 1271                  Reunion 2002     743981    Africa 75.74400
## 1272                  Reunion 2007     798094    Africa 76.44200
## 1273                  Romania 1952   16630000    Europe 61.05000
## 1274                  Romania 1957   17829327    Europe 64.10000
## 1275                  Romania 1962   18680721    Europe 66.80000
## 1276                  Romania 1967   19284814    Europe 66.80000
## 1277                  Romania 1972   20662648    Europe 69.21000
## 1278                  Romania 1977   21658597    Europe 69.46000
## 1279                  Romania 1982   22356726    Europe 69.66000
## 1280                  Romania 1987   22686371    Europe 69.53000
## 1281                  Romania 1992   22797027    Europe 69.36000
## 1282                  Romania 1997   22562458    Europe 69.72000
## 1283                  Romania 2002   22404337    Europe 71.32200
## 1284                  Romania 2007   22276056    Europe 72.47600
## 1285                   Rwanda 1952    2534927    Africa 40.00000
## 1286                   Rwanda 1957    2822082    Africa 41.50000
## 1287                   Rwanda 1962    3051242    Africa 43.00000
## 1288                   Rwanda 1967    3451079    Africa 44.10000
## 1289                   Rwanda 1972    3992121    Africa 44.60000
## 1290                   Rwanda 1977    4657072    Africa 45.00000
## 1291                   Rwanda 1982    5507565    Africa 46.21800
## 1292                   Rwanda 1987    6349365    Africa 44.02000
## 1293                   Rwanda 1992    7290203    Africa 23.59900
## 1294                   Rwanda 1997    7212583    Africa 36.08700
## 1295                   Rwanda 2002    7852401    Africa 43.41300
## 1296                   Rwanda 2007    8860588    Africa 46.24200
## 1297    Sao Tome and Principe 1952      60011    Africa 46.47100
## 1298    Sao Tome and Principe 1957      61325    Africa 48.94500
## 1299    Sao Tome and Principe 1962      65345    Africa 51.89300
## 1300    Sao Tome and Principe 1967      70787    Africa 54.42500
## 1301    Sao Tome and Principe 1972      76595    Africa 56.48000
## 1302    Sao Tome and Principe 1977      86796    Africa 58.55000
## 1303    Sao Tome and Principe 1982      98593    Africa 60.35100
## 1304    Sao Tome and Principe 1987     110812    Africa 61.72800
## 1305    Sao Tome and Principe 1992     125911    Africa 62.74200
## 1306    Sao Tome and Principe 1997     145608    Africa 63.30600
## 1307    Sao Tome and Principe 2002     170372    Africa 64.33700
## 1308    Sao Tome and Principe 2007     199579    Africa 65.52800
## 1309             Saudi Arabia 1952    4005677      Asia 39.87500
## 1310             Saudi Arabia 1957    4419650      Asia 42.86800
## 1311             Saudi Arabia 1962    4943029      Asia 45.91400
## 1312             Saudi Arabia 1967    5618198      Asia 49.90100
## 1313             Saudi Arabia 1972    6472756      Asia 53.88600
## 1314             Saudi Arabia 1977    8128505      Asia 58.69000
## 1315             Saudi Arabia 1982   11254672      Asia 63.01200
## 1316             Saudi Arabia 1987   14619745      Asia 66.29500
## 1317             Saudi Arabia 1992   16945857      Asia 68.76800
## 1318             Saudi Arabia 1997   21229759      Asia 70.53300
## 1319             Saudi Arabia 2002   24501530      Asia 71.62600
## 1320             Saudi Arabia 2007   27601038      Asia 72.77700
## 1321                  Senegal 1952    2755589    Africa 37.27800
## 1322                  Senegal 1957    3054547    Africa 39.32900
## 1323                  Senegal 1962    3430243    Africa 41.45400
## 1324                  Senegal 1967    3965841    Africa 43.56300
## 1325                  Senegal 1972    4588696    Africa 45.81500
## 1326                  Senegal 1977    5260855    Africa 48.87900
## 1327                  Senegal 1982    6147783    Africa 52.37900
## 1328                  Senegal 1987    7171347    Africa 55.76900
## 1329                  Senegal 1992    8307920    Africa 58.19600
## 1330                  Senegal 1997    9535314    Africa 60.18700
## 1331                  Senegal 2002   10870037    Africa 61.60000
## 1332                  Senegal 2007   12267493    Africa 63.06200
## 1333                   Serbia 1952    6860147    Europe 57.99600
## 1334                   Serbia 1957    7271135    Europe 61.68500
## 1335                   Serbia 1962    7616060    Europe 64.53100
## 1336                   Serbia 1967    7971222    Europe 66.91400
## 1337                   Serbia 1972    8313288    Europe 68.70000
## 1338                   Serbia 1977    8686367    Europe 70.30000
## 1339                   Serbia 1982    9032824    Europe 70.16200
## 1340                   Serbia 1987    9230783    Europe 71.21800
## 1341                   Serbia 1992    9826397    Europe 71.65900
## 1342                   Serbia 1997   10336594    Europe 72.23200
## 1343                   Serbia 2002   10111559    Europe 73.21300
## 1344                   Serbia 2007   10150265    Europe 74.00200
## 1345             Sierra Leone 1952    2143249    Africa 30.33100
## 1346             Sierra Leone 1957    2295678    Africa 31.57000
## 1347             Sierra Leone 1962    2467895    Africa 32.76700
## 1348             Sierra Leone 1967    2662190    Africa 34.11300
## 1349             Sierra Leone 1972    2879013    Africa 35.40000
## 1350             Sierra Leone 1977    3140897    Africa 36.78800
## 1351             Sierra Leone 1982    3464522    Africa 38.44500
## 1352             Sierra Leone 1987    3868905    Africa 40.00600
## 1353             Sierra Leone 1992    4260884    Africa 38.33300
## 1354             Sierra Leone 1997    4578212    Africa 39.89700
## 1355             Sierra Leone 2002    5359092    Africa 41.01200
## 1356             Sierra Leone 2007    6144562    Africa 42.56800
## 1357                Singapore 1952    1127000      Asia 60.39600
## 1358                Singapore 1957    1445929      Asia 63.17900
## 1359                Singapore 1962    1750200      Asia 65.79800
## 1360                Singapore 1967    1977600      Asia 67.94600
## 1361                Singapore 1972    2152400      Asia 69.52100
## 1362                Singapore 1977    2325300      Asia 70.79500
## 1363                Singapore 1982    2651869      Asia 71.76000
## 1364                Singapore 1987    2794552      Asia 73.56000
## 1365                Singapore 1992    3235865      Asia 75.78800
## 1366                Singapore 1997    3802309      Asia 77.15800
## 1367                Singapore 2002    4197776      Asia 78.77000
## 1368                Singapore 2007    4553009      Asia 79.97200
## 1369          Slovak Republic 1952    3558137    Europe 64.36000
## 1370          Slovak Republic 1957    3844277    Europe 67.45000
## 1371          Slovak Republic 1962    4237384    Europe 70.33000
## 1372          Slovak Republic 1967    4442238    Europe 70.98000
## 1373          Slovak Republic 1972    4593433    Europe 70.35000
## 1374          Slovak Republic 1977    4827803    Europe 70.45000
## 1375          Slovak Republic 1982    5048043    Europe 70.80000
## 1376          Slovak Republic 1987    5199318    Europe 71.08000
## 1377          Slovak Republic 1992    5302888    Europe 71.38000
## 1378          Slovak Republic 1997    5383010    Europe 72.71000
## 1379          Slovak Republic 2002    5410052    Europe 73.80000
## 1380          Slovak Republic 2007    5447502    Europe 74.66300
## 1381                 Slovenia 1952    1489518    Europe 65.57000
## 1382                 Slovenia 1957    1533070    Europe 67.85000
## 1383                 Slovenia 1962    1582962    Europe 69.15000
## 1384                 Slovenia 1967    1646912    Europe 69.18000
## 1385                 Slovenia 1972    1694510    Europe 69.82000
## 1386                 Slovenia 1977    1746919    Europe 70.97000
## 1387                 Slovenia 1982    1861252    Europe 71.06300
## 1388                 Slovenia 1987    1945870    Europe 72.25000
## 1389                 Slovenia 1992    1999210    Europe 73.64000
## 1390                 Slovenia 1997    2011612    Europe 75.13000
## 1391                 Slovenia 2002    2011497    Europe 76.66000
## 1392                 Slovenia 2007    2009245    Europe 77.92600
## 1393                  Somalia 1952    2526994    Africa 32.97800
## 1394                  Somalia 1957    2780415    Africa 34.97700
## 1395                  Somalia 1962    3080153    Africa 36.98100
## 1396                  Somalia 1967    3428839    Africa 38.97700
## 1397                  Somalia 1972    3840161    Africa 40.97300
## 1398                  Somalia 1977    4353666    Africa 41.97400
## 1399                  Somalia 1982    5828892    Africa 42.95500
## 1400                  Somalia 1987    6921858    Africa 44.50100
## 1401                  Somalia 1992    6099799    Africa 39.65800
## 1402                  Somalia 1997    6633514    Africa 43.79500
## 1403                  Somalia 2002    7753310    Africa 45.93600
## 1404                  Somalia 2007    9118773    Africa 48.15900
## 1405             South Africa 1952   14264935    Africa 45.00900
## 1406             South Africa 1957   16151549    Africa 47.98500
## 1407             South Africa 1962   18356657    Africa 49.95100
## 1408             South Africa 1967   20997321    Africa 51.92700
## 1409             South Africa 1972   23935810    Africa 53.69600
## 1410             South Africa 1977   27129932    Africa 55.52700
## 1411             South Africa 1982   31140029    Africa 58.16100
## 1412             South Africa 1987   35933379    Africa 60.83400
## 1413             South Africa 1992   39964159    Africa 61.88800
## 1414             South Africa 1997   42835005    Africa 60.23600
## 1415             South Africa 2002   44433622    Africa 53.36500
## 1416             South Africa 2007   43997828    Africa 49.33900
## 1417                    Spain 1952   28549870    Europe 64.94000
## 1418                    Spain 1957   29841614    Europe 66.66000
## 1419                    Spain 1962   31158061    Europe 69.69000
## 1420                    Spain 1967   32850275    Europe 71.44000
## 1421                    Spain 1972   34513161    Europe 73.06000
## 1422                    Spain 1977   36439000    Europe 74.39000
## 1423                    Spain 1982   37983310    Europe 76.30000
## 1424                    Spain 1987   38880702    Europe 76.90000
## 1425                    Spain 1992   39549438    Europe 77.57000
## 1426                    Spain 1997   39855442    Europe 78.77000
## 1427                    Spain 2002   40152517    Europe 79.78000
## 1428                    Spain 2007   40448191    Europe 80.94100
## 1429                Sri Lanka 1952    7982342      Asia 57.59300
## 1430                Sri Lanka 1957    9128546      Asia 61.45600
## 1431                Sri Lanka 1962   10421936      Asia 62.19200
## 1432                Sri Lanka 1967   11737396      Asia 64.26600
## 1433                Sri Lanka 1972   13016733      Asia 65.04200
## 1434                Sri Lanka 1977   14116836      Asia 65.94900
## 1435                Sri Lanka 1982   15410151      Asia 68.75700
## 1436                Sri Lanka 1987   16495304      Asia 69.01100
## 1437                Sri Lanka 1992   17587060      Asia 70.37900
## 1438                Sri Lanka 1997   18698655      Asia 70.45700
## 1439                Sri Lanka 2002   19576783      Asia 70.81500
## 1440                Sri Lanka 2007   20378239      Asia 72.39600
## 1441                    Sudan 1952    8504667    Africa 38.63500
## 1442                    Sudan 1957    9753392    Africa 39.62400
## 1443                    Sudan 1962   11183227    Africa 40.87000
## 1444                    Sudan 1967   12716129    Africa 42.85800
## 1445                    Sudan 1972   14597019    Africa 45.08300
## 1446                    Sudan 1977   17104986    Africa 47.80000
## 1447                    Sudan 1982   20367053    Africa 50.33800
## 1448                    Sudan 1987   24725960    Africa 51.74400
## 1449                    Sudan 1992   28227588    Africa 53.55600
## 1450                    Sudan 1997   32160729    Africa 55.37300
## 1451                    Sudan 2002   37090298    Africa 56.36900
## 1452                    Sudan 2007   42292929    Africa 58.55600
## 1453                Swaziland 1952     290243    Africa 41.40700
## 1454                Swaziland 1957     326741    Africa 43.42400
## 1455                Swaziland 1962     370006    Africa 44.99200
## 1456                Swaziland 1967     420690    Africa 46.63300
## 1457                Swaziland 1972     480105    Africa 49.55200
## 1458                Swaziland 1977     551425    Africa 52.53700
## 1459                Swaziland 1982     649901    Africa 55.56100
## 1460                Swaziland 1987     779348    Africa 57.67800
## 1461                Swaziland 1992     962344    Africa 58.47400
## 1462                Swaziland 1997    1054486    Africa 54.28900
## 1463                Swaziland 2002    1130269    Africa 43.86900
## 1464                Swaziland 2007    1133066    Africa 39.61300
## 1465                   Sweden 1952    7124673    Europe 71.86000
## 1466                   Sweden 1957    7363802    Europe 72.49000
## 1467                   Sweden 1962    7561588    Europe 73.37000
## 1468                   Sweden 1967    7867931    Europe 74.16000
## 1469                   Sweden 1972    8122293    Europe 74.72000
## 1470                   Sweden 1977    8251648    Europe 75.44000
## 1471                   Sweden 1982    8325260    Europe 76.42000
## 1472                   Sweden 1987    8421403    Europe 77.19000
## 1473                   Sweden 1992    8718867    Europe 78.16000
## 1474                   Sweden 1997    8897619    Europe 79.39000
## 1475                   Sweden 2002    8954175    Europe 80.04000
## 1476                   Sweden 2007    9031088    Europe 80.88400
## 1477              Switzerland 1952    4815000    Europe 69.62000
## 1478              Switzerland 1957    5126000    Europe 70.56000
## 1479              Switzerland 1962    5666000    Europe 71.32000
## 1480              Switzerland 1967    6063000    Europe 72.77000
## 1481              Switzerland 1972    6401400    Europe 73.78000
## 1482              Switzerland 1977    6316424    Europe 75.39000
## 1483              Switzerland 1982    6468126    Europe 76.21000
## 1484              Switzerland 1987    6649942    Europe 77.41000
## 1485              Switzerland 1992    6995447    Europe 78.03000
## 1486              Switzerland 1997    7193761    Europe 79.37000
## 1487              Switzerland 2002    7361757    Europe 80.62000
## 1488              Switzerland 2007    7554661    Europe 81.70100
## 1489                    Syria 1952    3661549      Asia 45.88300
## 1490                    Syria 1957    4149908      Asia 48.28400
## 1491                    Syria 1962    4834621      Asia 50.30500
## 1492                    Syria 1967    5680812      Asia 53.65500
## 1493                    Syria 1972    6701172      Asia 57.29600
## 1494                    Syria 1977    7932503      Asia 61.19500
## 1495                    Syria 1982    9410494      Asia 64.59000
## 1496                    Syria 1987   11242847      Asia 66.97400
## 1497                    Syria 1992   13219062      Asia 69.24900
## 1498                    Syria 1997   15081016      Asia 71.52700
## 1499                    Syria 2002   17155814      Asia 73.05300
## 1500                    Syria 2007   19314747      Asia 74.14300
## 1501                   Taiwan 1952    8550362      Asia 58.50000
## 1502                   Taiwan 1957   10164215      Asia 62.40000
## 1503                   Taiwan 1962   11918938      Asia 65.20000
## 1504                   Taiwan 1967   13648692      Asia 67.50000
## 1505                   Taiwan 1972   15226039      Asia 69.39000
## 1506                   Taiwan 1977   16785196      Asia 70.59000
## 1507                   Taiwan 1982   18501390      Asia 72.16000
## 1508                   Taiwan 1987   19757799      Asia 73.40000
## 1509                   Taiwan 1992   20686918      Asia 74.26000
## 1510                   Taiwan 1997   21628605      Asia 75.25000
## 1511                   Taiwan 2002   22454239      Asia 76.99000
## 1512                   Taiwan 2007   23174294      Asia 78.40000
## 1513                 Tanzania 1952    8322925    Africa 41.21500
## 1514                 Tanzania 1957    9452826    Africa 42.97400
## 1515                 Tanzania 1962   10863958    Africa 44.24600
## 1516                 Tanzania 1967   12607312    Africa 45.75700
## 1517                 Tanzania 1972   14706593    Africa 47.62000
## 1518                 Tanzania 1977   17129565    Africa 49.91900
## 1519                 Tanzania 1982   19844382    Africa 50.60800
## 1520                 Tanzania 1987   23040630    Africa 51.53500
## 1521                 Tanzania 1992   26605473    Africa 50.44000
## 1522                 Tanzania 1997   30686889    Africa 48.46600
## 1523                 Tanzania 2002   34593779    Africa 49.65100
## 1524                 Tanzania 2007   38139640    Africa 52.51700
## 1525                 Thailand 1952   21289402      Asia 50.84800
## 1526                 Thailand 1957   25041917      Asia 53.63000
## 1527                 Thailand 1962   29263397      Asia 56.06100
## 1528                 Thailand 1967   34024249      Asia 58.28500
## 1529                 Thailand 1972   39276153      Asia 60.40500
## 1530                 Thailand 1977   44148285      Asia 62.49400
## 1531                 Thailand 1982   48827160      Asia 64.59700
## 1532                 Thailand 1987   52910342      Asia 66.08400
## 1533                 Thailand 1992   56667095      Asia 67.29800
## 1534                 Thailand 1997   60216677      Asia 67.52100
## 1535                 Thailand 2002   62806748      Asia 68.56400
## 1536                 Thailand 2007   65068149      Asia 70.61600
## 1537                     Togo 1952    1219113    Africa 38.59600
## 1538                     Togo 1957    1357445    Africa 41.20800
## 1539                     Togo 1962    1528098    Africa 43.92200
## 1540                     Togo 1967    1735550    Africa 46.76900
## 1541                     Togo 1972    2056351    Africa 49.75900
## 1542                     Togo 1977    2308582    Africa 52.88700
## 1543                     Togo 1982    2644765    Africa 55.47100
## 1544                     Togo 1987    3154264    Africa 56.94100
## 1545                     Togo 1992    3747553    Africa 58.06100
## 1546                     Togo 1997    4320890    Africa 58.39000
## 1547                     Togo 2002    4977378    Africa 57.56100
## 1548                     Togo 2007    5701579    Africa 58.42000
## 1549      Trinidad and Tobago 1952     662850  Americas 59.10000
## 1550      Trinidad and Tobago 1957     764900  Americas 61.80000
## 1551      Trinidad and Tobago 1962     887498  Americas 64.90000
## 1552      Trinidad and Tobago 1967     960155  Americas 65.40000
## 1553      Trinidad and Tobago 1972     975199  Americas 65.90000
## 1554      Trinidad and Tobago 1977    1039009  Americas 68.30000
## 1555      Trinidad and Tobago 1982    1116479  Americas 68.83200
## 1556      Trinidad and Tobago 1987    1191336  Americas 69.58200
## 1557      Trinidad and Tobago 1992    1183669  Americas 69.86200
## 1558      Trinidad and Tobago 1997    1138101  Americas 69.46500
## 1559      Trinidad and Tobago 2002    1101832  Americas 68.97600
## 1560      Trinidad and Tobago 2007    1056608  Americas 69.81900
## 1561                  Tunisia 1952    3647735    Africa 44.60000
## 1562                  Tunisia 1957    3950849    Africa 47.10000
## 1563                  Tunisia 1962    4286552    Africa 49.57900
## 1564                  Tunisia 1967    4786986    Africa 52.05300
## 1565                  Tunisia 1972    5303507    Africa 55.60200
## 1566                  Tunisia 1977    6005061    Africa 59.83700
## 1567                  Tunisia 1982    6734098    Africa 64.04800
## 1568                  Tunisia 1987    7724976    Africa 66.89400
## 1569                  Tunisia 1992    8523077    Africa 70.00100
## 1570                  Tunisia 1997    9231669    Africa 71.97300
## 1571                  Tunisia 2002    9770575    Africa 73.04200
## 1572                  Tunisia 2007   10276158    Africa 73.92300
## 1573                   Turkey 1952   22235677    Europe 43.58500
## 1574                   Turkey 1957   25670939    Europe 48.07900
## 1575                   Turkey 1962   29788695    Europe 52.09800
## 1576                   Turkey 1967   33411317    Europe 54.33600
## 1577                   Turkey 1972   37492953    Europe 57.00500
## 1578                   Turkey 1977   42404033    Europe 59.50700
## 1579                   Turkey 1982   47328791    Europe 61.03600
## 1580                   Turkey 1987   52881328    Europe 63.10800
## 1581                   Turkey 1992   58179144    Europe 66.14600
## 1582                   Turkey 1997   63047647    Europe 68.83500
## 1583                   Turkey 2002   67308928    Europe 70.84500
## 1584                   Turkey 2007   71158647    Europe 71.77700
## 1585                   Uganda 1952    5824797    Africa 39.97800
## 1586                   Uganda 1957    6675501    Africa 42.57100
## 1587                   Uganda 1962    7688797    Africa 45.34400
## 1588                   Uganda 1967    8900294    Africa 48.05100
## 1589                   Uganda 1972   10190285    Africa 51.01600
## 1590                   Uganda 1977   11457758    Africa 50.35000
## 1591                   Uganda 1982   12939400    Africa 49.84900
## 1592                   Uganda 1987   15283050    Africa 51.50900
## 1593                   Uganda 1992   18252190    Africa 48.82500
## 1594                   Uganda 1997   21210254    Africa 44.57800
## 1595                   Uganda 2002   24739869    Africa 47.81300
## 1596                   Uganda 2007   29170398    Africa 51.54200
## 1597           United Kingdom 1952   50430000    Europe 69.18000
## 1598           United Kingdom 1957   51430000    Europe 70.42000
## 1599           United Kingdom 1962   53292000    Europe 70.76000
## 1600           United Kingdom 1967   54959000    Europe 71.36000
## 1601           United Kingdom 1972   56079000    Europe 72.01000
## 1602           United Kingdom 1977   56179000    Europe 72.76000
## 1603           United Kingdom 1982   56339704    Europe 74.04000
## 1604           United Kingdom 1987   56981620    Europe 75.00700
## 1605           United Kingdom 1992   57866349    Europe 76.42000
## 1606           United Kingdom 1997   58808266    Europe 77.21800
## 1607           United Kingdom 2002   59912431    Europe 78.47100
## 1608           United Kingdom 2007   60776238    Europe 79.42500
## 1609            United States 1952  157553000  Americas 68.44000
## 1610            United States 1957  171984000  Americas 69.49000
## 1611            United States 1962  186538000  Americas 70.21000
## 1612            United States 1967  198712000  Americas 70.76000
## 1613            United States 1972  209896000  Americas 71.34000
## 1614            United States 1977  220239000  Americas 73.38000
## 1615            United States 1982  232187835  Americas 74.65000
## 1616            United States 1987  242803533  Americas 75.02000
## 1617            United States 1992  256894189  Americas 76.09000
## 1618            United States 1997  272911760  Americas 76.81000
## 1619            United States 2002  287675526  Americas 77.31000
## 1620            United States 2007  301139947  Americas 78.24200
## 1621                  Uruguay 1952    2252965  Americas 66.07100
## 1622                  Uruguay 1957    2424959  Americas 67.04400
## 1623                  Uruguay 1962    2598466  Americas 68.25300
## 1624                  Uruguay 1967    2748579  Americas 68.46800
## 1625                  Uruguay 1972    2829526  Americas 68.67300
## 1626                  Uruguay 1977    2873520  Americas 69.48100
## 1627                  Uruguay 1982    2953997  Americas 70.80500
## 1628                  Uruguay 1987    3045153  Americas 71.91800
## 1629                  Uruguay 1992    3149262  Americas 72.75200
## 1630                  Uruguay 1997    3262838  Americas 74.22300
## 1631                  Uruguay 2002    3363085  Americas 75.30700
## 1632                  Uruguay 2007    3447496  Americas 76.38400
## 1633                Venezuela 1952    5439568  Americas 55.08800
## 1634                Venezuela 1957    6702668  Americas 57.90700
## 1635                Venezuela 1962    8143375  Americas 60.77000
## 1636                Venezuela 1967    9709552  Americas 63.47900
## 1637                Venezuela 1972   11515649  Americas 65.71200
## 1638                Venezuela 1977   13503563  Americas 67.45600
## 1639                Venezuela 1982   15620766  Americas 68.55700
## 1640                Venezuela 1987   17910182  Americas 70.19000
## 1641                Venezuela 1992   20265563  Americas 71.15000
## 1642                Venezuela 1997   22374398  Americas 72.14600
## 1643                Venezuela 2002   24287670  Americas 72.76600
## 1644                Venezuela 2007   26084662  Americas 73.74700
## 1645                  Vietnam 1952   26246839      Asia 40.41200
## 1646                  Vietnam 1957   28998543      Asia 42.88700
## 1647                  Vietnam 1962   33796140      Asia 45.36300
## 1648                  Vietnam 1967   39463910      Asia 47.83800
## 1649                  Vietnam 1972   44655014      Asia 50.25400
## 1650                  Vietnam 1977   50533506      Asia 55.76400
## 1651                  Vietnam 1982   56142181      Asia 58.81600
## 1652                  Vietnam 1987   62826491      Asia 62.82000
## 1653                  Vietnam 1992   69940728      Asia 67.66200
## 1654                  Vietnam 1997   76048996      Asia 70.67200
## 1655                  Vietnam 2002   80908147      Asia 73.01700
## 1656                  Vietnam 2007   85262356      Asia 74.24900
## 1657       West Bank and Gaza 1952    1030585      Asia 43.16000
## 1658       West Bank and Gaza 1957    1070439      Asia 45.67100
## 1659       West Bank and Gaza 1962    1133134      Asia 48.12700
## 1660       West Bank and Gaza 1967    1142636      Asia 51.63100
## 1661       West Bank and Gaza 1972    1089572      Asia 56.53200
## 1662       West Bank and Gaza 1977    1261091      Asia 60.76500
## 1663       West Bank and Gaza 1982    1425876      Asia 64.40600
## 1664       West Bank and Gaza 1987    1691210      Asia 67.04600
## 1665       West Bank and Gaza 1992    2104779      Asia 69.71800
## 1666       West Bank and Gaza 1997    2826046      Asia 71.09600
## 1667       West Bank and Gaza 2002    3389578      Asia 72.37000
## 1668       West Bank and Gaza 2007    4018332      Asia 73.42200
## 1669               Yemen Rep. 1952    4963829      Asia 32.54800
## 1670               Yemen Rep. 1957    5498090      Asia 33.97000
## 1671               Yemen Rep. 1962    6120081      Asia 35.18000
## 1672               Yemen Rep. 1967    6740785      Asia 36.98400
## 1673               Yemen Rep. 1972    7407075      Asia 39.84800
## 1674               Yemen Rep. 1977    8403990      Asia 44.17500
## 1675               Yemen Rep. 1982    9657618      Asia 49.11300
## 1676               Yemen Rep. 1987   11219340      Asia 52.92200
## 1677               Yemen Rep. 1992   13367997      Asia 55.59900
## 1678               Yemen Rep. 1997   15826497      Asia 58.02000
## 1679               Yemen Rep. 2002   18701257      Asia 60.30800
## 1680               Yemen Rep. 2007   22211743      Asia 62.69800
## 1681                   Zambia 1952    2672000    Africa 42.03800
## 1682                   Zambia 1957    3016000    Africa 44.07700
## 1683                   Zambia 1962    3421000    Africa 46.02300
## 1684                   Zambia 1967    3900000    Africa 47.76800
## 1685                   Zambia 1972    4506497    Africa 50.10700
## 1686                   Zambia 1977    5216550    Africa 51.38600
## 1687                   Zambia 1982    6100407    Africa 51.82100
## 1688                   Zambia 1987    7272406    Africa 50.82100
## 1689                   Zambia 1992    8381163    Africa 46.10000
## 1690                   Zambia 1997    9417789    Africa 40.23800
## 1691                   Zambia 2002   10595811    Africa 39.19300
## 1692                   Zambia 2007   11746035    Africa 42.38400
## 1693                 Zimbabwe 1952    3080907    Africa 48.45100
## 1694                 Zimbabwe 1957    3646340    Africa 50.46900
## 1695                 Zimbabwe 1962    4277736    Africa 52.35800
## 1696                 Zimbabwe 1967    4995432    Africa 53.99500
## 1697                 Zimbabwe 1972    5861135    Africa 55.63500
## 1698                 Zimbabwe 1977    6642107    Africa 57.67400
## 1699                 Zimbabwe 1982    7636524    Africa 60.36300
## 1700                 Zimbabwe 1987    9216418    Africa 62.35100
## 1701                 Zimbabwe 1992   10704340    Africa 60.37700
## 1702                 Zimbabwe 1997   11404948    Africa 46.80900
## 1703                 Zimbabwe 2002   11926563    Africa 39.98900
## 1704                 Zimbabwe 2007   12311143    Africa 43.48700
##        gdpPercap
## 1       779.4453
## 2       820.8530
## 3       853.1007
## 4       836.1971
## 5       739.9811
## 6       786.1134
## 7       978.0114
## 8       852.3959
## 9       649.3414
## 10      635.3414
## 11      726.7341
## 12      974.5803
## 13     1601.0561
## 14     1942.2842
## 15     2312.8890
## 16     2760.1969
## 17     3313.4222
## 18     3533.0039
## 19     3630.8807
## 20     3738.9327
## 21     2497.4379
## 22     3193.0546
## 23     4604.2117
## 24     5937.0295
## 25     2449.0082
## 26     3013.9760
## 27     2550.8169
## 28     3246.9918
## 29     4182.6638
## 30     4910.4168
## 31     5745.1602
## 32     5681.3585
## 33     5023.2166
## 34     4797.2951
## 35     5288.0404
## 36     6223.3675
## 37     3520.6103
## 38     3827.9405
## 39     4269.2767
## 40     5522.7764
## 41     5473.2880
## 42     3008.6474
## 43     2756.9537
## 44     2430.2083
## 45     2627.8457
## 46     2277.1409
## 47     2773.2873
## 48     4797.2313
## 49     5911.3151
## 50     6856.8562
## 51     7133.1660
## 52     8052.9530
## 53     9443.0385
## 54    10079.0267
## 55     8997.8974
## 56     9139.6714
## 57     9308.4187
## 58    10967.2820
## 59     8797.6407
## 60    12779.3796
## 61    10039.5956
## 62    10949.6496
## 63    12217.2269
## 64    14526.1246
## 65    16788.6295
## 66    18334.1975
## 67    19477.0093
## 68    21888.8890
## 69    23424.7668
## 70    26997.9366
## 71    30687.7547
## 72    34435.3674
## 73     6137.0765
## 74     8842.5980
## 75    10750.7211
## 76    12834.6024
## 77    16661.6256
## 78    19749.4223
## 79    21597.0836
## 80    23687.8261
## 81    27042.0187
## 82    29095.9207
## 83    32417.6077
## 84    36126.4927
## 85     9867.0848
## 86    11635.7995
## 87    12753.2751
## 88    14804.6727
## 89    18268.6584
## 90    19340.1020
## 91    19211.1473
## 92    18524.0241
## 93    19035.5792
## 94    20292.0168
## 95    23403.5593
## 96    29796.0483
## 97      684.2442
## 98      661.6375
## 99      686.3416
## 100     721.1861
## 101     630.2336
## 102     659.8772
## 103     676.9819
## 104     751.9794
## 105     837.8102
## 106     972.7700
## 107    1136.3904
## 108    1391.2538
## 109    8343.1051
## 110    9714.9606
## 111   10991.2068
## 112   13149.0412
## 113   16672.1436
## 114   19117.9745
## 115   20979.8459
## 116   22525.5631
## 117   25575.5707
## 118   27561.1966
## 119   30485.8838
## 120   33692.6051
## 121    1062.7522
## 122     959.6011
## 123     949.4991
## 124    1035.8314
## 125    1085.7969
## 126    1029.1613
## 127    1277.8976
## 128    1225.8560
## 129    1191.2077
## 130    1232.9753
## 131    1372.8779
## 132    1441.2849
## 133    2677.3263
## 134    2127.6863
## 135    2180.9725
## 136    2586.8861
## 137    2980.3313
## 138    3548.0978
## 139    3156.5105
## 140    2753.6915
## 141    2961.6997
## 142    3326.1432
## 143    3413.2627
## 144    3822.1371
## 145     973.5332
## 146    1353.9892
## 147    1709.6837
## 148    2172.3524
## 149    2860.1698
## 150    3528.4813
## 151    4126.6132
## 152    4314.1148
## 153    2546.7814
## 154    4766.3559
## 155    6018.9752
## 156    7446.2988
## 157     851.2411
## 158     918.2325
## 159     983.6540
## 160    1214.7093
## 161    2263.6111
## 162    3214.8578
## 163    4551.1421
## 164    6205.8839
## 165    7954.1116
## 166    8647.1423
## 167   11003.6051
## 168   12569.8518
## 169    2108.9444
## 170    2487.3660
## 171    3336.5858
## 172    3429.8644
## 173    4985.7115
## 174    6660.1187
## 175    7030.8359
## 176    7807.0958
## 177    6950.2830
## 178    7957.9808
## 179    8131.2128
## 180    9065.8008
## 181    2444.2866
## 182    3008.6707
## 183    4254.3378
## 184    5577.0028
## 185    6597.4944
## 186    7612.2404
## 187    8224.1916
## 188    8239.8548
## 189    6302.6234
## 190    5970.3888
## 191    7696.7777
## 192   10680.7928
## 193     543.2552
## 194     617.1835
## 195     722.5120
## 196     794.8266
## 197     854.7360
## 198     743.3870
## 199     807.1986
## 200     912.0631
## 201     931.7528
## 202     946.2950
## 203    1037.6452
## 204    1217.0330
## 205     339.2965
## 206     379.5646
## 207     355.2032
## 208     412.9775
## 209     464.0995
## 210     556.1033
## 211     559.6032
## 212     621.8188
## 213     631.6999
## 214     463.1151
## 215     446.4035
## 216     430.0707
## 217     368.4693
## 218     434.0383
## 219     496.9136
## 220     523.4323
## 221     421.6240
## 222     524.9722
## 223     624.4755
## 224     683.8956
## 225     682.3032
## 226     734.2852
## 227     896.2260
## 228    1713.7787
## 229    1172.6677
## 230    1313.0481
## 231    1399.6074
## 232    1508.4531
## 233    1684.1465
## 234    1783.4329
## 235    2367.9833
## 236    2602.6642
## 237    1793.1633
## 238    1694.3375
## 239    1934.0114
## 240    2042.0952
## 241   11367.1611
## 242   12489.9501
## 243   13462.4855
## 244   16076.5880
## 245   18970.5709
## 246   22090.8831
## 247   22898.7921
## 248   26626.5150
## 249   26342.8843
## 250   28954.9259
## 251   33328.9651
## 252   36319.2350
## 253    1071.3107
## 254    1190.8443
## 255    1193.0688
## 256    1136.0566
## 257    1070.0133
## 258    1109.3743
## 259     956.7530
## 260     844.8764
## 261     747.9055
## 262     740.5063
## 263     738.6906
## 264     706.0165
## 265    1178.6659
## 266    1308.4956
## 267    1389.8176
## 268    1196.8106
## 269    1104.1040
## 270    1133.9850
## 271     797.9081
## 272     952.3861
## 273    1058.0643
## 274    1004.9614
## 275    1156.1819
## 276    1704.0637
## 277    3939.9788
## 278    4315.6227
## 279    4519.0943
## 280    5106.6543
## 281    5494.0244
## 282    4756.7638
## 283    5095.6657
## 284    5547.0638
## 285    7596.1260
## 286   10118.0532
## 287   10778.7838
## 288   13171.6388
## 289     400.4486
## 290     575.9870
## 291     487.6740
## 292     612.7057
## 293     676.9001
## 294     741.2375
## 295     962.4214
## 296    1378.9040
## 297    1655.7842
## 298    2289.2341
## 299    3119.2809
## 300    4959.1149
## 301    2144.1151
## 302    2323.8056
## 303    2492.3511
## 304    2678.7298
## 305    3264.6600
## 306    3815.8079
## 307    4397.5757
## 308    4903.2191
## 309    5444.6486
## 310    6117.3617
## 311    5755.2600
## 312    7006.5804
## 313    1102.9909
## 314    1211.1485
## 315    1406.6483
## 316    1876.0296
## 317    1937.5777
## 318    1172.6030
## 319    1267.1001
## 320    1315.9808
## 321    1246.9074
## 322    1173.6182
## 323    1075.8116
## 324     986.1479
## 325     780.5423
## 326     905.8602
## 327     896.3146
## 328     861.5932
## 329     904.8961
## 330     795.7573
## 331     673.7478
## 332     672.7748
## 333     457.7192
## 334     312.1884
## 335     241.1659
## 336     277.5519
## 337    2125.6214
## 338    2315.0566
## 339    2464.7832
## 340    2677.9396
## 341    3213.1527
## 342    3259.1790
## 343    4879.5075
## 344    4201.1949
## 345    4016.2395
## 346    3484.1644
## 347    3484.0620
## 348    3632.5578
## 349    2627.0095
## 350    2990.0108
## 351    3460.9370
## 352    4161.7278
## 353    5118.1469
## 354    5926.8770
## 355    5262.7348
## 356    5629.9153
## 357    6160.4163
## 358    6677.0453
## 359    7723.4472
## 360    9645.0614
## 361    1388.5947
## 362    1500.8959
## 363    1728.8694
## 364    2052.0505
## 365    2378.2011
## 366    2517.7365
## 367    2602.7102
## 368    2156.9561
## 369    1648.0738
## 370    1786.2654
## 371    1648.8008
## 372    1544.7501
## 373    3119.2365
## 374    4338.2316
## 375    5477.8900
## 376    6960.2979
## 377    9164.0901
## 378   11305.3852
## 379   13221.8218
## 380   13822.5839
## 381    8447.7949
## 382    9875.6045
## 383   11628.3890
## 384   14619.2227
## 385    5586.5388
## 386    6092.1744
## 387    5180.7559
## 388    5690.2680
## 389    5305.4453
## 390    6380.4950
## 391    7316.9181
## 392    7532.9248
## 393    5592.8440
## 394    5431.9904
## 395    6340.6467
## 396    8948.1029
## 397    6876.1403
## 398    8256.3439
## 399   10136.8671
## 400   11399.4449
## 401   13108.4536
## 402   14800.1606
## 403   15377.2285
## 404   16310.4434
## 405   14297.0212
## 406   16048.5142
## 407   17596.2102
## 408   22833.3085
## 409    9692.3852
## 410   11099.6593
## 411   13583.3135
## 412   15937.2112
## 413   18866.2072
## 414   20422.9015
## 415   21688.0405
## 416   25116.1758
## 417   26406.7399
## 418   29804.3457
## 419   32166.5001
## 420   35278.4187
## 421    2669.5295
## 422    2864.9691
## 423    3020.9893
## 424    3020.0505
## 425    3694.2124
## 426    3081.7610
## 427    2879.4681
## 428    2880.1026
## 429    2377.1562
## 430    1895.0170
## 431    1908.2609
## 432    2082.4816
## 433    1397.7171
## 434    1544.4030
## 435    1662.1374
## 436    1653.7230
## 437    2189.8745
## 438    2681.9889
## 439    2861.0924
## 440    2899.8422
## 441    3044.2142
## 442    3614.1013
## 443    4563.8082
## 444    6025.3748
## 445    3522.1107
## 446    3780.5467
## 447    4086.1141
## 448    4579.0742
## 449    5280.9947
## 450    6679.6233
## 451    7213.7913
## 452    6481.7770
## 453    7103.7026
## 454    7429.4559
## 455    5773.0445
## 456    6873.2623
## 457    1418.8224
## 458    1458.9153
## 459    1693.3359
## 460    1814.8807
## 461    2024.0081
## 462    2785.4936
## 463    3503.7296
## 464    3885.4607
## 465    3794.7552
## 466    4173.1818
## 467    4754.6044
## 468    5581.1810
## 469    3048.3029
## 470    3421.5232
## 471    3776.8036
## 472    4358.5954
## 473    4520.2460
## 474    5138.9224
## 475    4098.3442
## 476    4140.4421
## 477    4444.2317
## 478    5154.8255
## 479    5351.5687
## 480    5728.3535
## 481     375.6431
## 482     426.0964
## 483     582.8420
## 484     915.5960
## 485     672.4123
## 486     958.5668
## 487     927.8253
## 488     966.8968
## 489    1132.0550
## 490    2814.4808
## 491    7703.4959
## 492   12154.0897
## 493     328.9406
## 494     344.1619
## 495     380.9958
## 496     468.7950
## 497     514.3242
## 498     505.7538
## 499     524.8758
## 500     521.1341
## 501     582.8585
## 502     913.4708
## 503     765.3500
## 504     641.3695
## 505     362.1463
## 506     378.9042
## 507     419.4564
## 508     516.1186
## 509     566.2439
## 510     556.8084
## 511     577.8607
## 512     573.7413
## 513     421.3535
## 514     515.8894
## 515     530.0535
## 516     690.8056
## 517    6424.5191
## 518    7545.4154
## 519    9371.8426
## 520   10921.6363
## 521   14358.8759
## 522   15605.4228
## 523   18533.1576
## 524   21141.0122
## 525   20647.1650
## 526   23723.9502
## 527   28204.5906
## 528   33207.0844
## 529    7029.8093
## 530    8662.8349
## 531   10560.4855
## 532   12999.9177
## 533   16107.1917
## 534   18292.6351
## 535   20293.8975
## 536   22066.4421
## 537   24703.7961
## 538   25889.7849
## 539   28926.0323
## 540   30470.0167
## 541    4293.4765
## 542    4976.1981
## 543    6631.4592
## 544    8358.7620
## 545   11401.9484
## 546   21745.5733
## 547   15113.3619
## 548   11864.4084
## 549   13522.1575
## 550   14722.8419
## 551   12521.7139
## 552   13206.4845
## 553     485.2307
## 554     520.9267
## 555     599.6503
## 556     734.7829
## 557     756.0868
## 558     884.7553
## 559     835.8096
## 560     611.6589
## 561     665.6244
## 562     653.7302
## 563     660.5856
## 564     752.7497
## 565    7144.1144
## 566   10187.8267
## 567   12902.4629
## 568   14745.6256
## 569   18016.1803
## 570   20512.9212
## 571   22031.5327
## 572   24639.1857
## 573   26505.3032
## 574   27788.8842
## 575   30035.8020
## 576   32170.3744
## 577     911.2989
## 578    1043.5615
## 579    1190.0411
## 580    1125.6972
## 581    1178.2237
## 582     993.2240
## 583     876.0326
## 584     847.0061
## 585     925.0602
## 586    1005.2458
## 587    1111.9846
## 588    1327.6089
## 589    3530.6901
## 590    4916.2999
## 591    6017.1907
## 592    8513.0970
## 593   12724.8296
## 594   14195.5243
## 595   15268.4209
## 596   16120.5284
## 597   17541.4963
## 598   18747.6981
## 599   22514.2548
## 600   27538.4119
## 601    2428.2378
## 602    2617.1560
## 603    2750.3644
## 604    3242.5311
## 605    4031.4083
## 606    4879.9927
## 607    4820.4948
## 608    4246.4860
## 609    4439.4508
## 610    4684.3138
## 611    4858.3475
## 612    5186.0500
## 613     510.1965
## 614     576.2670
## 615     686.3737
## 616     708.7595
## 617     741.6662
## 618     874.6859
## 619     857.2504
## 620     805.5725
## 621     794.3484
## 622     869.4498
## 623     945.5836
## 624     942.6542
## 625     299.8503
## 626     431.7905
## 627     522.0344
## 628     715.5806
## 629     820.2246
## 630     764.7260
## 631     838.1240
## 632     736.4154
## 633     745.5399
## 634     796.6645
## 635     575.7047
## 636     579.2317
## 637    1840.3669
## 638    1726.8879
## 639    1796.5890
## 640    1452.0577
## 641    1654.4569
## 642    1874.2989
## 643    2011.1595
## 644    1823.0160
## 645    1456.3095
## 646    1341.7269
## 647    1270.3649
## 648    1201.6372
## 649    2194.9262
## 650    2220.4877
## 651    2291.1568
## 652    2538.2694
## 653    2529.8423
## 654    3203.2081
## 655    3121.7608
## 656    3023.0967
## 657    3081.6946
## 658    3160.4549
## 659    3099.7287
## 660    3548.3308
## 661    3054.4212
## 662    3629.0765
## 663    4692.6483
## 664    6197.9628
## 665    8315.9281
## 666   11186.1413
## 667   14560.5305
## 668   20038.4727
## 669   24757.6030
## 670   28377.6322
## 671   30209.0152
## 672   39724.9787
## 673    5263.6738
## 674    6040.1800
## 675    7550.3599
## 676    9326.6447
## 677   10168.6561
## 678   11674.8374
## 679   12545.9907
## 680   12986.4800
## 681   10535.6285
## 682   11712.7768
## 683   14843.9356
## 684   18008.9444
## 685    7267.6884
## 686    9244.0014
## 687   10350.1591
## 688   13319.8957
## 689   15798.0636
## 690   19654.9625
## 691   23269.6075
## 692   26923.2063
## 693   25144.3920
## 694   28061.0997
## 695   31163.2020
## 696   36180.7892
## 697     546.5657
## 698     590.0620
## 699     658.3472
## 700     700.7706
## 701     724.0325
## 702     813.3373
## 703     855.7235
## 704     976.5127
## 705    1164.4068
## 706    1458.8174
## 707    1746.7695
## 708    2452.2104
## 709     749.6817
## 710     858.9003
## 711     849.2898
## 712     762.4318
## 713    1111.1079
## 714    1382.7021
## 715    1516.8730
## 716    1748.3570
## 717    2383.1409
## 718    3119.3356
## 719    2873.9129
## 720    3540.6516
## 721    3035.3260
## 722    3290.2576
## 723    4187.3298
## 724    5906.7318
## 725    9613.8186
## 726   11888.5951
## 727    7608.3346
## 728    6642.8814
## 729    7235.6532
## 730    8263.5903
## 731    9240.7620
## 732   11605.7145
## 733    4129.7661
## 734    6229.3336
## 735    8341.7378
## 736    8931.4598
## 737    9576.0376
## 738   14688.2351
## 739   14517.9071
## 740   11643.5727
## 741    3745.6407
## 742    3076.2398
## 743    4390.7173
## 744    4471.0619
## 745    5210.2803
## 746    5599.0779
## 747    6631.5973
## 748    7655.5690
## 749    9530.7729
## 750   11150.9811
## 751   12618.3214
## 752   13872.8665
## 753   17558.8155
## 754   24521.9471
## 755   34077.0494
## 756   40675.9964
## 757    4086.5221
## 758    5385.2785
## 759    7105.6307
## 760    8393.7414
## 761   12786.9322
## 762   13306.6192
## 763   15367.0292
## 764   17122.4799
## 765   18051.5225
## 766   20896.6092
## 767   21905.5951
## 768   25523.2771
## 769    4931.4042
## 770    6248.6562
## 771    8243.5823
## 772   10022.4013
## 773   12269.2738
## 774   14255.9847
## 775   16537.4835
## 776   19207.2348
## 777   22013.6449
## 778   24675.0245
## 779   27968.0982
## 780   28569.7197
## 781    2898.5309
## 782    4756.5258
## 783    5246.1075
## 784    6124.7035
## 785    7433.8893
## 786    6650.1956
## 787    6068.0513
## 788    6351.2375
## 789    7404.9237
## 790    7121.9247
## 791    6994.7749
## 792    7320.8803
## 793    3216.9563
## 794    4317.6944
## 795    6576.6495
## 796    9847.7886
## 797   14778.7864
## 798   16610.3770
## 799   19384.1057
## 800   22375.9419
## 801   26824.8951
## 802   28816.5850
## 803   28604.5919
## 804   31656.0681
## 805    1546.9078
## 806    1886.0806
## 807    2348.0092
## 808    2741.7963
## 809    2110.8563
## 810    2852.3516
## 811    4161.4160
## 812    4448.6799
## 813    3431.5936
## 814    3645.3796
## 815    3844.9172
## 816    4519.4612
## 817     853.5409
## 818     944.4383
## 819     896.9664
## 820    1056.7365
## 821    1222.3600
## 822    1267.6132
## 823    1348.2258
## 824    1361.9369
## 825    1341.9217
## 826    1360.4850
## 827    1287.5147
## 828    1463.2493
## 829    1088.2778
## 830    1571.1347
## 831    1621.6936
## 832    2143.5406
## 833    3701.6215
## 834    4106.3012
## 835    4106.5253
## 836    4106.4923
## 837    3726.0635
## 838    1690.7568
## 839    1646.7582
## 840    1593.0655
## 841    1030.5922
## 842    1487.5935
## 843    1536.3444
## 844    2029.2281
## 845    3030.8767
## 846    4657.2210
## 847    5622.9425
## 848    8533.0888
## 849   12104.2787
## 850   15993.5280
## 851   19233.9882
## 852   23348.1397
## 853  108382.3529
## 854  113523.1329
## 855   95458.1118
## 856   80894.8833
## 857  109347.8670
## 858   59265.4771
## 859   31354.0357
## 860   28118.4300
## 861   34932.9196
## 862   40300.6200
## 863   35110.1057
## 864   47306.9898
## 865    4834.8041
## 866    6089.7869
## 867    5714.5606
## 868    6006.9830
## 869    7486.3843
## 870    8659.6968
## 871    7640.5195
## 872    5377.0913
## 873    6890.8069
## 874    8754.9639
## 875    9313.9388
## 876   10461.0587
## 877     298.8462
## 878     335.9971
## 879     411.8006
## 880     498.6390
## 881     496.5816
## 882     745.3695
## 883     797.2631
## 884     773.9932
## 885     977.4863
## 886    1186.1480
## 887    1275.1846
## 888    1569.3314
## 889     575.5730
## 890     620.9700
## 891     634.1952
## 892     713.6036
## 893     803.0055
## 894     640.3224
## 895     572.1996
## 896     506.1139
## 897     636.6229
## 898     609.1740
## 899     531.4824
## 900     414.5073
## 901    2387.5481
## 902    3448.2844
## 903    6757.0308
## 904   18772.7517
## 905   21011.4972
## 906   21951.2118
## 907   17364.2754
## 908   11770.5898
## 909    9640.1385
## 910    9467.4461
## 911    9534.6775
## 912   12057.4993
## 913    1443.0117
## 914    1589.2027
## 915    1643.3871
## 916    1634.0473
## 917    1748.5630
## 918    1544.2286
## 919    1302.8787
## 920    1155.4419
## 921    1040.6762
## 922     986.2959
## 923     894.6371
## 924    1044.7701
## 925     369.1651
## 926     416.3698
## 927     427.9011
## 928     495.5148
## 929     584.6220
## 930     663.2237
## 931     632.8039
## 932     635.5174
## 933     563.2000
## 934     692.2758
## 935     665.4231
## 936     759.3499
## 937    1831.1329
## 938    1810.0670
## 939    2036.8849
## 940    2277.7424
## 941    2849.0948
## 942    3827.9216
## 943    4920.3560
## 944    5249.8027
## 945    7277.9128
## 946   10132.9096
## 947   10206.9779
## 948   12451.6558
## 949     452.3370
## 950     490.3822
## 951     496.1743
## 952     545.0099
## 953     581.3689
## 954     686.3953
## 955     618.0141
## 956     684.1716
## 957     739.0144
## 958     790.2580
## 959     951.4098
## 960    1042.5816
## 961     743.1159
## 962     846.1203
## 963    1055.8960
## 964    1421.1452
## 965    1586.8518
## 966    1497.4922
## 967    1481.1502
## 968    1421.6036
## 969    1361.3698
## 970    1483.1361
## 971    1579.0195
## 972    1803.1515
## 973    1967.9557
## 974    2034.0380
## 975    2529.0675
## 976    2475.3876
## 977    2575.4842
## 978    3710.9830
## 979    3688.0377
## 980    4783.5869
## 981    6058.2538
## 982    7425.7053
## 983    9021.8159
## 984   10956.9911
## 985    3478.1255
## 986    4131.5466
## 987    4581.6094
## 988    5754.7339
## 989    6809.4067
## 990    7674.9291
## 991    9611.1475
## 992    8688.1560
## 993    9472.3843
## 994    9767.2975
## 995   10742.4405
## 996   11977.5750
## 997     786.5669
## 998     912.6626
## 999    1056.3540
## 1000   1226.0411
## 1001   1421.7420
## 1002   1647.5117
## 1003   2000.6031
## 1004   2338.0083
## 1005   1785.4020
## 1006   1902.2521
## 1007   2140.7393
## 1008   3095.7723
## 1009   2647.5856
## 1010   3682.2599
## 1011   4649.5938
## 1012   5907.8509
## 1013   7778.4140
## 1014   9595.9299
## 1015  11222.5876
## 1016  11732.5102
## 1017   7003.3390
## 1018   6465.6133
## 1019   6557.1943
## 1020   9253.8961
## 1021   1688.2036
## 1022   1642.0023
## 1023   1566.3535
## 1024   1711.0448
## 1025   1930.1950
## 1026   2370.6200
## 1027   2702.6204
## 1028   2755.0470
## 1029   2948.0473
## 1030   2982.1019
## 1031   3258.4956
## 1032   3820.1752
## 1033    468.5260
## 1034    495.5868
## 1035    556.6864
## 1036    566.6692
## 1037    724.9178
## 1038    502.3197
## 1039    462.2114
## 1040    389.8762
## 1041    410.8968
## 1042    472.3461
## 1043    633.6179
## 1044    823.6856
## 1045    331.0000
## 1046    350.0000
## 1047    388.0000
## 1048    349.0000
## 1049    357.0000
## 1050    371.0000
## 1051    424.0000
## 1052    385.0000
## 1053    347.0000
## 1054    415.0000
## 1055    611.0000
## 1056    944.0000
## 1057   2423.7804
## 1058   2621.4481
## 1059   3173.2156
## 1060   3793.6948
## 1061   3746.0809
## 1062   3876.4860
## 1063   4191.1005
## 1064   3693.7313
## 1065   3804.5380
## 1066   3899.5243
## 1067   4072.3248
## 1068   4811.0604
## 1069    545.8657
## 1070    597.9364
## 1071    652.3969
## 1072    676.4422
## 1073    674.7881
## 1074    694.1124
## 1075    718.3731
## 1076    775.6325
## 1077    897.7404
## 1078   1010.8921
## 1079   1057.2063
## 1080   1091.3598
## 1081   8941.5719
## 1082  11276.1934
## 1083  12790.8496
## 1084  15363.2514
## 1085  18794.7457
## 1086  21209.0592
## 1087  21399.4605
## 1088  23651.3236
## 1089  26790.9496
## 1090  30246.1306
## 1091  33724.7578
## 1092  36797.9333
## 1093  10556.5757
## 1094  12247.3953
## 1095  13175.6780
## 1096  14463.9189
## 1097  16046.0373
## 1098  16233.7177
## 1099  17632.4104
## 1100  19007.1913
## 1101  18363.3249
## 1102  21050.4138
## 1103  23189.8014
## 1104  25185.0091
## 1105   3112.3639
## 1106   3457.4159
## 1107   3634.3644
## 1108   4643.3935
## 1109   4688.5933
## 1110   5486.3711
## 1111   3470.3382
## 1112   2955.9844
## 1113   2170.1517
## 1114   2253.0230
## 1115   2474.5488
## 1116   2749.3210
## 1117    761.8794
## 1118    835.5234
## 1119    997.7661
## 1120   1054.3849
## 1121    954.2092
## 1122    808.8971
## 1123    909.7221
## 1124    668.3000
## 1125    581.1827
## 1126    580.3052
## 1127    601.0745
## 1128    619.6769
## 1129   1077.2819
## 1130   1100.5926
## 1131   1150.9275
## 1132   1014.5141
## 1133   1698.3888
## 1134   1981.9518
## 1135   1576.9738
## 1136   1385.0296
## 1137   1619.8482
## 1138   1624.9413
## 1139   1615.2864
## 1140   2013.9773
## 1141  10095.4217
## 1142  11653.9730
## 1143  13450.4015
## 1144  16361.8765
## 1145  18965.0555
## 1146  23311.3494
## 1147  26298.6353
## 1148  31540.9748
## 1149  33965.6611
## 1150  41283.1643
## 1151  44683.9753
## 1152  49357.1902
## 1153   1828.2303
## 1154   2242.7466
## 1155   2924.6381
## 1156   4720.9427
## 1157  10618.0385
## 1158  11848.3439
## 1159  12954.7910
## 1160  18115.2231
## 1161  18616.7069
## 1162  19702.0558
## 1163  19774.8369
## 1164  22316.1929
## 1165    684.5971
## 1166    747.0835
## 1167    803.3427
## 1168    942.4083
## 1169   1049.9390
## 1170   1175.9212
## 1171   1443.4298
## 1172   1704.6866
## 1173   1971.8295
## 1174   2049.3505
## 1175   2092.7124
## 1176   2605.9476
## 1177   2480.3803
## 1178   2961.8009
## 1179   3536.5403
## 1180   4421.0091
## 1181   5364.2497
## 1182   5351.9121
## 1183   7009.6016
## 1184   7034.7792
## 1185   6618.7431
## 1186   7113.6923
## 1187   7356.0319
## 1188   9809.1856
## 1189   1952.3087
## 1190   2046.1547
## 1191   2148.0271
## 1192   2299.3763
## 1193   2523.3380
## 1194   3248.3733
## 1195   4258.5036
## 1196   3998.8757
## 1197   4196.4111
## 1198   4247.4003
## 1199   3783.6742
## 1200   4172.8385
## 1201   3758.5234
## 1202   4245.2567
## 1203   4957.0380
## 1204   5788.0933
## 1205   5937.8273
## 1206   6281.2909
## 1207   6434.5018
## 1208   6360.9434
## 1209   4446.3809
## 1210   5838.3477
## 1211   5909.0201
## 1212   7408.9056
## 1213   1272.8810
## 1214   1547.9448
## 1215   1649.5522
## 1216   1814.1274
## 1217   1989.3741
## 1218   2373.2043
## 1219   2603.2738
## 1220   2189.6350
## 1221   2279.3240
## 1222   2536.5349
## 1223   2650.9211
## 1224   3190.4810
## 1225   4029.3297
## 1226   4734.2530
## 1227   5338.7521
## 1228   6557.1528
## 1229   8006.5070
## 1230   9508.1415
## 1231   8451.5310
## 1232   9082.3512
## 1233   7738.8812
## 1234  10159.5837
## 1235  12002.2391
## 1236  15389.9247
## 1237   3068.3199
## 1238   3774.5717
## 1239   4727.9549
## 1240   6361.5180
## 1241   9022.2474
## 1242  10172.4857
## 1243  11753.8429
## 1244  13039.3088
## 1245  16207.2666
## 1246  17641.0316
## 1247  19970.9079
## 1248  20509.6478
## 1249   3081.9598
## 1250   3907.1562
## 1251   5108.3446
## 1252   6929.2777
## 1253   9123.0417
## 1254   9770.5249
## 1255  10330.9891
## 1256  12281.3419
## 1257  14641.5871
## 1258  16999.4333
## 1259  18855.6062
## 1260  19328.7090
## 1261   2718.8853
## 1262   2769.4518
## 1263   3173.7233
## 1264   4021.1757
## 1265   5047.6586
## 1266   4319.8041
## 1267   5267.2194
## 1268   5303.3775
## 1269   6101.2558
## 1270   6071.9414
## 1271   6316.1652
## 1272   7670.1226
## 1273   3144.6132
## 1274   3943.3702
## 1275   4734.9976
## 1276   6470.8665
## 1277   8011.4144
## 1278   9356.3972
## 1279   9605.3141
## 1280   9696.2733
## 1281   6598.4099
## 1282   7346.5476
## 1283   7885.3601
## 1284  10808.4756
## 1285    493.3239
## 1286    540.2894
## 1287    597.4731
## 1288    510.9637
## 1289    590.5807
## 1290    670.0806
## 1291    881.5706
## 1292    847.9912
## 1293    737.0686
## 1294    589.9445
## 1295    785.6538
## 1296    863.0885
## 1297    879.5836
## 1298    860.7369
## 1299   1071.5511
## 1300   1384.8406
## 1301   1532.9853
## 1302   1737.5617
## 1303   1890.2181
## 1304   1516.5255
## 1305   1428.7778
## 1306   1339.0760
## 1307   1353.0924
## 1308   1598.4351
## 1309   6459.5548
## 1310   8157.5912
## 1311  11626.4197
## 1312  16903.0489
## 1313  24837.4287
## 1314  34167.7626
## 1315  33693.1753
## 1316  21198.2614
## 1317  24841.6178
## 1318  20586.6902
## 1319  19014.5412
## 1320  21654.8319
## 1321   1450.3570
## 1322   1567.6530
## 1323   1654.9887
## 1324   1612.4046
## 1325   1597.7121
## 1326   1561.7691
## 1327   1518.4800
## 1328   1441.7207
## 1329   1367.8994
## 1330   1392.3683
## 1331   1519.6353
## 1332   1712.4721
## 1333   3581.4594
## 1334   4981.0909
## 1335   6289.6292
## 1336   7991.7071
## 1337  10522.0675
## 1338  12980.6696
## 1339  15181.0927
## 1340  15870.8785
## 1341   9325.0682
## 1342   7914.3203
## 1343   7236.0753
## 1344   9786.5347
## 1345    879.7877
## 1346   1004.4844
## 1347   1116.6399
## 1348   1206.0435
## 1349   1353.7598
## 1350   1348.2852
## 1351   1465.0108
## 1352   1294.4478
## 1353   1068.6963
## 1354    574.6482
## 1355    699.4897
## 1356    862.5408
## 1357   2315.1382
## 1358   2843.1044
## 1359   3674.7356
## 1360   4977.4185
## 1361   8597.7562
## 1362  11210.0895
## 1363  15169.1611
## 1364  18861.5308
## 1365  24769.8912
## 1366  33519.4766
## 1367  36023.1054
## 1368  47143.1796
## 1369   5074.6591
## 1370   6093.2630
## 1371   7481.1076
## 1372   8412.9024
## 1373   9674.1676
## 1374  10922.6640
## 1375  11348.5459
## 1376  12037.2676
## 1377   9498.4677
## 1378  12126.2306
## 1379  13638.7784
## 1380  18678.3144
## 1381   4215.0417
## 1382   5862.2766
## 1383   7402.3034
## 1384   9405.4894
## 1385  12383.4862
## 1386  15277.0302
## 1387  17866.7218
## 1388  18678.5349
## 1389  14214.7168
## 1390  17161.1073
## 1391  20660.0194
## 1392  25768.2576
## 1393   1135.7498
## 1394   1258.1474
## 1395   1369.4883
## 1396   1284.7332
## 1397   1254.5761
## 1398   1450.9925
## 1399   1176.8070
## 1400   1093.2450
## 1401    926.9603
## 1402    930.5964
## 1403    882.0818
## 1404    926.1411
## 1405   4725.2955
## 1406   5487.1042
## 1407   5768.7297
## 1408   7114.4780
## 1409   7765.9626
## 1410   8028.6514
## 1411   8568.2662
## 1412   7825.8234
## 1413   7225.0693
## 1414   7479.1882
## 1415   7710.9464
## 1416   9269.6578
## 1417   3834.0347
## 1418   4564.8024
## 1419   5693.8439
## 1420   7993.5123
## 1421  10638.7513
## 1422  13236.9212
## 1423  13926.1700
## 1424  15764.9831
## 1425  18603.0645
## 1426  20445.2990
## 1427  24835.4717
## 1428  28821.0637
## 1429   1083.5320
## 1430   1072.5466
## 1431   1074.4720
## 1432   1135.5143
## 1433   1213.3955
## 1434   1348.7757
## 1435   1648.0798
## 1436   1876.7668
## 1437   2153.7392
## 1438   2664.4773
## 1439   3015.3788
## 1440   3970.0954
## 1441   1615.9911
## 1442   1770.3371
## 1443   1959.5938
## 1444   1687.9976
## 1445   1659.6528
## 1446   2202.9884
## 1447   1895.5441
## 1448   1507.8192
## 1449   1492.1970
## 1450   1632.2108
## 1451   1993.3983
## 1452   2602.3950
## 1453   1148.3766
## 1454   1244.7084
## 1455   1856.1821
## 1456   2613.1017
## 1457   3364.8366
## 1458   3781.4106
## 1459   3895.3840
## 1460   3984.8398
## 1461   3553.0224
## 1462   3876.7685
## 1463   4128.1169
## 1464   4513.4806
## 1465   8527.8447
## 1466   9911.8782
## 1467  12329.4419
## 1468  15258.2970
## 1469  17832.0246
## 1470  18855.7252
## 1471  20667.3812
## 1472  23586.9293
## 1473  23880.0168
## 1474  25266.5950
## 1475  29341.6309
## 1476  33859.7484
## 1477  14734.2327
## 1478  17909.4897
## 1479  20431.0927
## 1480  22966.1443
## 1481  27195.1130
## 1482  26982.2905
## 1483  28397.7151
## 1484  30281.7046
## 1485  31871.5303
## 1486  32135.3230
## 1487  34480.9577
## 1488  37506.4191
## 1489   1643.4854
## 1490   2117.2349
## 1491   2193.0371
## 1492   1881.9236
## 1493   2571.4230
## 1494   3195.4846
## 1495   3761.8377
## 1496   3116.7743
## 1497   3340.5428
## 1498   4014.2390
## 1499   4090.9253
## 1500   4184.5481
## 1501   1206.9479
## 1502   1507.8613
## 1503   1822.8790
## 1504   2643.8587
## 1505   4062.5239
## 1506   5596.5198
## 1507   7426.3548
## 1508  11054.5618
## 1509  15215.6579
## 1510  20206.8210
## 1511  23235.4233
## 1512  28718.2768
## 1513    716.6501
## 1514    698.5356
## 1515    722.0038
## 1516    848.2187
## 1517    915.9851
## 1518    962.4923
## 1519    874.2426
## 1520    831.8221
## 1521    825.6825
## 1522    789.1862
## 1523    899.0742
## 1524   1107.4822
## 1525    757.7974
## 1526    793.5774
## 1527   1002.1992
## 1528   1295.4607
## 1529   1524.3589
## 1530   1961.2246
## 1531   2393.2198
## 1532   2982.6538
## 1533   4616.8965
## 1534   5852.6255
## 1535   5913.1875
## 1536   7458.3963
## 1537    859.8087
## 1538    925.9083
## 1539   1067.5348
## 1540   1477.5968
## 1541   1649.6602
## 1542   1532.7770
## 1543   1344.5780
## 1544   1202.2014
## 1545   1034.2989
## 1546    982.2869
## 1547    886.2206
## 1548    882.9699
## 1549   3023.2719
## 1550   4100.3934
## 1551   4997.5240
## 1552   5621.3685
## 1553   6619.5514
## 1554   7899.5542
## 1555   9119.5286
## 1556   7388.5978
## 1557   7370.9909
## 1558   8792.5731
## 1559  11460.6002
## 1560  18008.5092
## 1561   1468.4756
## 1562   1395.2325
## 1563   1660.3032
## 1564   1932.3602
## 1565   2753.2860
## 1566   3120.8768
## 1567   3560.2332
## 1568   3810.4193
## 1569   4332.7202
## 1570   4876.7986
## 1571   5722.8957
## 1572   7092.9230
## 1573   1969.1010
## 1574   2218.7543
## 1575   2322.8699
## 1576   2826.3564
## 1577   3450.6964
## 1578   4269.1223
## 1579   4241.3563
## 1580   5089.0437
## 1581   5678.3483
## 1582   6601.4299
## 1583   6508.0857
## 1584   8458.2764
## 1585    734.7535
## 1586    774.3711
## 1587    767.2717
## 1588    908.9185
## 1589    950.7359
## 1590    843.7331
## 1591    682.2662
## 1592    617.7244
## 1593    644.1708
## 1594    816.5591
## 1595    927.7210
## 1596   1056.3801
## 1597   9979.5085
## 1598  11283.1779
## 1599  12477.1771
## 1600  14142.8509
## 1601  15895.1164
## 1602  17428.7485
## 1603  18232.4245
## 1604  21664.7877
## 1605  22705.0925
## 1606  26074.5314
## 1607  29478.9992
## 1608  33203.2613
## 1609  13990.4821
## 1610  14847.1271
## 1611  16173.1459
## 1612  19530.3656
## 1613  21806.0359
## 1614  24072.6321
## 1615  25009.5591
## 1616  29884.3504
## 1617  32003.9322
## 1618  35767.4330
## 1619  39097.0995
## 1620  42951.6531
## 1621   5716.7667
## 1622   6150.7730
## 1623   5603.3577
## 1624   5444.6196
## 1625   5703.4089
## 1626   6504.3397
## 1627   6920.2231
## 1628   7452.3990
## 1629   8137.0048
## 1630   9230.2407
## 1631   7727.0020
## 1632  10611.4630
## 1633   7689.7998
## 1634   9802.4665
## 1635   8422.9742
## 1636   9541.4742
## 1637  10505.2597
## 1638  13143.9510
## 1639  11152.4101
## 1640   9883.5846
## 1641  10733.9263
## 1642  10165.4952
## 1643   8605.0478
## 1644  11415.8057
## 1645    605.0665
## 1646    676.2854
## 1647    772.0492
## 1648    637.1233
## 1649    699.5016
## 1650    713.5371
## 1651    707.2358
## 1652    820.7994
## 1653    989.0231
## 1654   1385.8968
## 1655   1764.4567
## 1656   2441.5764
## 1657   1515.5923
## 1658   1827.0677
## 1659   2198.9563
## 1660   2649.7150
## 1661   3133.4093
## 1662   3682.8315
## 1663   4336.0321
## 1664   5107.1974
## 1665   6017.6548
## 1666   7110.6676
## 1667   4515.4876
## 1668   3025.3498
## 1669    781.7176
## 1670    804.8305
## 1671    825.6232
## 1672    862.4421
## 1673   1265.0470
## 1674   1829.7652
## 1675   1977.5570
## 1676   1971.7415
## 1677   1879.4967
## 1678   2117.4845
## 1679   2234.8208
## 1680   2280.7699
## 1681   1147.3888
## 1682   1311.9568
## 1683   1452.7258
## 1684   1777.0773
## 1685   1773.4983
## 1686   1588.6883
## 1687   1408.6786
## 1688   1213.3151
## 1689   1210.8846
## 1690   1071.3538
## 1691   1071.6139
## 1692   1271.2116
## 1693    406.8841
## 1694    518.7643
## 1695    527.2722
## 1696    569.7951
## 1697    799.3622
## 1698    685.5877
## 1699    788.8550
## 1700    706.1573
## 1701    693.4208
## 1702    792.4500
## 1703    672.0386
## 1704    469.7093
```

### How about a Data Repository?

* You can read from the Web like above with a repository (find the url to the data and copy into R), but many data repositories offer APIs (Application Protocol Interfaces) that let us grab data by other information (dois, authors, organization, etc)
* R has reposirtory packages for: [dataverse](https://cran.r-project.org/web/packages/dataverse/index.html), [figshare](https://cran.r-project.org/web/packages/rfigshare/index.html), [ICPSR](https://cran.r-project.org/web/packages/icpsrdata/index.html), [dataone](https://cran.r-project.org/web/packages/dataone/index.html), rentrez, Pew
* [ROpenScience](https://ropensci.org/) makes a number of repositories available to access scientific data

**We will focus on dataverse today**

### Let's get some data from dataverse


```r
#install.packages('dataverse') # we need to install the package
library("dataverse")
get_dataset("doi:10.7910/DVN/GJQNEQ") #we see two datasets that are .tab
```

```
## Dataset (127660): 
## Version: 1.1, RELEASED
## Release Date: 2017-07-23T17:27:22Z
## License: NONE
## 17 Files:
##                        label version      id               contentType
## 1 gapminder-FiveYearData.tab       2 3037713 text/tab-separated-values
## 2         gapminder_wide.tab       2 3037712 text/tab-separated-values
```

* We can pull the file metadata.


```r
file_metadata <- get_file_metadata('gapminder-FiveYearData.tab', 'doi:10.7910/DVN/GJQNEQ')
```

* And print it out:


```r
file_metadata
```

```
## [1] "<?xml version='1.0' encoding='UTF-8'?><codeBook xmlns=\"http://www.icpsr.umich.edu/DDI\" version=\"2.0\"><stdyDscr><citation><titlStmt><titl>Gapminder</titl><IDNo agency=\"doi\">10.7910/DVN/GJQNEQ</IDNo></titlStmt><rspStmt><AuthEnty>DENNIS, Tim</AuthEnty></rspStmt><biblCit>DENNIS, Tim, 2017, \"Gapminder\", doi:10.7910/DVN/GJQNEQ, Harvard Dataverse, V1, UNF:6:NEKJa+hemgnpmRHJMFVKKA==</biblCit></citation></stdyDscr><fileDscr ID=\"f3037713\"><fileTxt><fileName>gapminder-FiveYearData.tab</fileName><dimensns><caseQnty>1704</caseQnty><varQnty>6</varQnty></dimensns><fileType>text/tab-separated-values</fileType></fileTxt><notes level=\"file\" type=\"VDC:UNF\" subject=\"Universal Numeric Fingerprint\">UNF:6:YgJwbX4q7QQs9c3rYlHDSA==</notes></fileDscr><dataDscr><var ID=\"v17836803\" name=\"country\" intrvl=\"discrete\"><location fileid=\"f3037713\"/><labl level=\"variable\">country</labl><varFormat type=\"character\"/><notes subject=\"Universal Numeric Fingerprint\" level=\"variable\" type=\"VDC:UNF\">UNF:6:jdlCaWjCsmdSeTNdCUdJkg==</notes></var><var ID=\"v17836801\" name=\"year\" intrvl=\"discrete\"><location fileid=\"f3037713\"/><labl level=\"variable\">year</labl><sumStat type=\"min\">1952.0</sumStat><sumStat type=\"mode\">.</sumStat><sumStat type=\"invd\">0.0</sumStat><sumStat type=\"stdev\">17.265329508973615</sumStat><sumStat type=\"medn\">1979.5</sumStat><sumStat type=\"vald\">1704.0</sumStat><sumStat type=\"mean\">1979.5</sumStat><sumStat type=\"max\">2007.0</sumStat><varFormat type=\"numeric\"/><notes subject=\"Universal Numeric Fingerprint\" level=\"variable\" type=\"VDC:UNF\">UNF:6:OQcH2L2+ovNxdgZZkTFzSg==</notes></var><var ID=\"v17836798\" name=\"pop\" intrvl=\"contin\"><location fileid=\"f3037713\"/><labl level=\"variable\">pop</labl><sumStat type=\"min\">60011.0</sumStat><sumStat type=\"invd\">0.0</sumStat><sumStat type=\"vald\">1704.0</sumStat><sumStat type=\"medn\">7023595.5</sumStat><sumStat type=\"max\">1.318683096E9</sumStat><sumStat type=\"stdev\">1.0615789674682796E8</sumStat><sumStat type=\"mode\">.</sumStat><sumStat type=\"mean\">2.960121232511743E7</sumStat><varFormat type=\"numeric\"/><notes subject=\"Universal Numeric Fingerprint\" level=\"variable\" type=\"VDC:UNF\">UNF:6:ZxKnUqly3P/7ishEOn3bKg==</notes></var><var ID=\"v17836800\" name=\"continent\" intrvl=\"discrete\"><location fileid=\"f3037713\"/><labl level=\"variable\">continent</labl><varFormat type=\"character\"/><notes subject=\"Universal Numeric Fingerprint\" level=\"variable\" type=\"VDC:UNF\">UNF:6:3wye374McxoKigUhZG9NtQ==</notes></var><var ID=\"v17836802\" name=\"lifeExp\" intrvl=\"contin\"><location fileid=\"f3037713\"/><labl level=\"variable\">lifeExp</labl><sumStat type=\"medn\">60.7125</sumStat><sumStat type=\"mean\">59.47443936619718</sumStat><sumStat type=\"stdev\">12.917107415241194</sumStat><sumStat type=\"min\">23.599</sumStat><sumStat type=\"vald\">1704.0</sumStat><sumStat type=\"invd\">0.0</sumStat><sumStat type=\"mode\">.</sumStat><sumStat type=\"max\">82.603</sumStat><varFormat type=\"numeric\"/><notes subject=\"Universal Numeric Fingerprint\" level=\"variable\" type=\"VDC:UNF\">UNF:6:0TDHekEtVqurUXRHpwj+6A==</notes></var><var ID=\"v17836799\" name=\"gdpPercap\" intrvl=\"contin\"><location fileid=\"f3037713\"/><labl level=\"variable\">gdpPercap</labl><sumStat type=\"mean\">7215.327081211972</sumStat><sumStat type=\"mode\">.</sumStat><sumStat type=\"vald\">1704.0</sumStat><sumStat type=\"max\">113523.1329</sumStat><sumStat type=\"medn\">3531.8469885</sumStat><sumStat type=\"min\">241.1658765</sumStat><sumStat type=\"invd\">0.0</sumStat><sumStat type=\"stdev\">9857.45454254157</sumStat><varFormat type=\"numeric\"/><notes subject=\"Universal Numeric Fingerprint\" level=\"variable\" type=\"VDC:UNF\">UNF:6:EqYFFOSWBOkRGByVGT7ijQ==</notes></var></dataDscr></codeBook>"
```
* Finally, we can use the function `writeBin` to write the `gapminder` data to our local file system.


```r
writeBin(get_file("gapminder-FiveYearData.tab", "doi:10.7910/DVN/GJQNEQ"),
         "data/gapminder-FiveYearData-dvn.csv")
```

You can also query Dataverse on other criteria and even publish a dataset from within R (you'll have to get a API key for that).
