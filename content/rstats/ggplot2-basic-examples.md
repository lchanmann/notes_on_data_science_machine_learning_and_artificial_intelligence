Title: Basic ggplot2 examples
Slug: ggplot2-basic-examples
Summary: Basic ggplot2 examples
Date: 2016-05-01 12:00
Category: R Stats
Tags: Data Visualization
Authors: Chris Albon


Original source: https://github.com/patilv/3graphs/blob/master/ggplot2Page/index.md

Want to learn more? I recommend working through: [R for Data Science](http://amzn.to/2myxnhi), [R Cookbook](http://amzn.to/2lF6hkb), and [R Graphics Cookbook](http://amzn.to/2m0fcPL).

```R
# make sure the graphic displays in RStudio by turning off external devices
dev.cur()
dev.off()
```




    pdf
      2






    null device
              1



## Create some simulated data


```R
## create three factor variables of length 50.
FacVar1 = as.factor(rep(c("level1", "level2"), 25))
FacVar2 = as.factor(rep(c("levelA", "levelB", "levelC"), 17)[-51])
FacVar3 = as.factor(rep(c("levelI", "levelII", "levelIII", "levelIV"), 13)[-c(51:52)])
```

## Create four numeric variables frpm different distributions


```R
## normal distribution
set.seed(123)
NumVar1 = round(rnorm(n = 50, mean = 1000, sd = 50), digits = 2)  
set.seed(123)
```


```R
## uniform distribution
NumVar2 = round(runif(n = 50, min = 500, max = 1500), digits = 2)
```


```R
## exponential distribution
set.seed(123)
NumVar3 = round(rexp(n = 50, rate = 0.001))
```


```R
## sequence
NumVar4 = 2001:2050
```


```R
## merge all the variables in a dataframe
simData = data.frame(FacVar1, FacVar2, FacVar3, NumVar1, NumVar2, NumVar3, NumVar4)
```


```R
## load required packages
library(ggplot2)
library(reshape2)
```

## One variable plots


```R
# create a plot of NumVar1's values and their row number
ggplot(simData, aes(y = NumVar1, x = 1:nrow(simData), group = "NumVar1")) + geom_point() + geom_line() + xlab("")
```


    Error in nrow(simData): object 'simData' not found




```R
# create a histogram of NumVar1
ggplot(simData, aes(x = NumVar1)) + geom_histogram()
```

    stat_bin: binwidth defaulted to range/30. Use 'binwidth = x' to adjust this.










![png]({filename}/images/ggplot2-basic-examples_files/ggplot2-basic-examples_13_2.png)



```R
# create a density plot of NumVar1
ggplot(simData, aes(x = NumVar1)) + geom_density()
```









![png]({filename}/images/ggplot2-basic-examples_files/ggplot2-basic-examples_14_1.png)



```R
# create a boxplot of NumVar1
ggplot(simData, aes(x = factor(""), y = NumVar1)) + geom_boxplot() + xlab("")
```









![png]({filename}/images/ggplot2-basic-examples_files/ggplot2-basic-examples_15_1.png)



```R
# create a barplot of FacVar3
ggplot(simData, aes(x = FacVar3)) + geom_bar()
```









![png]({filename}/images/ggplot2-basic-examples_files/ggplot2-basic-examples_16_1.png)



```R
# create a scatterplot of NumVar1 and NumVar 2
ggplot(simData, aes(x = NumVar1, y = NumVar2)) + geom_point()
```









![png]({filename}/images/ggplot2-basic-examples_files/ggplot2-basic-examples_17_1.png)



```R
# create a crosstab of FacVar2 and FacVar3 to get the Freq data
bartabledat = as.data.frame(table(simData$FacVar2, simData$FacVar3))
```


```R
# create a barplot of Var2's frequency, colored by Var1
ggplot(bartabledat, aes(x = Var2, y = Freq, fill = Var1)) + geom_bar(position = "dodge")
```









![png]({filename}/images/ggplot2-basic-examples_files/ggplot2-basic-examples_19_1.png)



```R
# create a stacked barplot of var2's frequency, colored by Var1
ggplot(bartabledat, aes(x = Var2, y = Freq, fill = Var1)) + geom_bar()
```









![png]({filename}/images/ggplot2-basic-examples_files/ggplot2-basic-examples_20_1.png)



```R
# create a proportion table of each combo's propotion of the total
bartableprop = as.data.frame(prop.table(table(simData$FacVar2, simData$FacVar3), 2) * 100)
```


```R
# create a bar plot of each combination's proportion of the total
ggplot(bartableprop, aes(x = Var2, y = Freq, fill = Var1)) + geom_bar()
```









![png]({filename}/images/ggplot2-basic-examples_files/ggplot2-basic-examples_22_1.png)



```R
# create a scatterplot, with each dot colored by a third variable
ggplot(simData, aes(x = NumVar1, y = NumVar2, color = FacVar1)) + geom_point()
```









![png]({filename}/images/ggplot2-basic-examples_files/ggplot2-basic-examples_23_1.png)



```R
# create a scatterplot with each dot sized by a third variable
ggplot(simData, aes(x = NumVar1, y = NumVar2, size = NumVar3)) + geom_point()
```









![png]({filename}/images/ggplot2-basic-examples_files/ggplot2-basic-examples_24_1.png)



```R
# Turn off external devices
dev.off()
```




    null device
              1
