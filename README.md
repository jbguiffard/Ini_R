---
title: "Quantitative Analysis Training - Introduction and Applications on R"
author: "Jean-Baptiste Guiffard"
date: "2022-11-16"
output: 
  html_document:
    toc: true
    toc_depth: 2
    theme: united
    highlight: tango
---


```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = FALSE)
library(flextable)
library(magrittr)
```


# Course structure



## Sessions


```{r, echo=F}

planning_R_M1 <- data.frame(Sessions = c("Session 1","Session 2","Session 3","Session 4","Session 5"),
           Dates = c("16/11","23/11","30/11","05/12","07/12"),
           Topics = c("The Basics of R","Measurement and Descriptive Statistics","Inference and Statistical Tests (I)","Inference and Statistical Tests (II)","Simple and Multiple Regressions"))

planning_R_M1 %>% regulartable() %>% autofit() %>% 
  width(j=~Sessions,width=0.9) %>% width(j=~Dates,width=0.5) %>% width(j=~Topics,width=3)
```


# Introducing R

## R software

R is:

- a platform for the object-oriented statistical programming language S

- Freely distributed by the CRAN (Comprehensive R Archive Network).

- and Open-source

S is a very high level programming language (a programming language with a high level of abstraction that allows to write programs using common natural language words - very often English - and familiar mathematical symbols) and a data analysis environment designed in the 1970s by John Chambers (statistician at Harvard) $\rightarrow$ the two modern implementation of S are R and S-PLUS.


## Getting R and RStudio

- To obtain R for any operating system, just go to CRAN at the following address: https://cran.r-project.org/

- The installation of R is simple by following the instructions.

- The use of R software is facilitated by the use of an integrated development environment (IDE) $\rightarrow$ RStudio

- After having installed R beforehand, you can download and install RStudio from the following site: https://posit.co/.


## RStudio


![RStudio, a free and open source IDE for R](Figures/1_RStudio_IDE_screenshot.png)



The RStudio environment is presented as a global window divided into 4 distinct sub-windows:

- The script window

- The console

- The environment and history window

- The files, graphs, packages and help window.



## A few Resources

Help on a function:
```{r echo=TRUE, eval=F}
?mean
help(mean)
```

Other resources are interesting:

- the help section in RStudio

- The CRAN site has manuals, mailing lists, FAQ's to facilitate exploration...

- do a direct web search using a search engine with the keywords R and CRAN.

- the site www.r-bloggers.com.

- Books...








# The basics of the R language

## R, a calculator (I)


```{r echo=TRUE}
2+2.5
7*5
100/25
```


## R, a calculator (II)

\centering
```{r echo=FALSE}
df_maths_symb <- data.frame(Operators = c('+','-','*','/','^','sqrt','log','exp','abs','...'),
                            Definitions = c('Addition','Substraction','Multiplication','Division','Exponent','Square Root','Logarithm','Exponential','Absolute Value','...'))

df_maths_symb %>% regulartable() %>% autofit() %>% 
  width(j=~Operators,width=0.5) %>% width(j=~Definitions,width=1.3)
```


## R, a calculator (III)

\centering
```{r echo=FALSE}
df_logical_statement <- data.frame(Operators = c('<','<=','>','>=','==','!=','&','|'),
                            Definitions = c('Less than','Less than or equal to','Greater than','Greater than or equal to','Equal to','Not equal to','And','Or'))

df_logical_statement %>% regulartable() %>% autofit() %>% 
  width(j=~Operators,width=0.5) %>% width(j=~Definitions,width=1.3)
```







## Some basic instructions about R environment

This instruction gives a list of all objects in a working environment:
```{r echo=TRUE, eval=F}
objects()
ls()
```

If I want to completely clear the environment, I can write the following command:

```{r echo=TRUE, eval=F}
rm(list=ls(all=TRUE))
```

To delete a particular object:
```{r echo=TRUE, eval=F}
rm(oneobject)

```

And to quit R...
```{r echo=TRUE, eval=F}
q()
```


## Load data 


### Working Directory

```{r echo=TRUE, eval=F}
setwd("C://Folder")
```


### Upload the data

```{r echo=TRUE, eval=F}
data <- read.csv2('DATA/afro_s6.csv')
```


## Packages

A package (or library) is a set of programs that completes and increases the functionalities of R $\rightarrow$ generally dedicated to a particular method or to a specific application domain.

Downloading a package 

```{r echo=TRUE, eval=F}
install.package('haven')
```

Using a package
```{r echo=TRUE, eval=F}
library(haven)
require(haven)
```


# Objects in R

## The scalar

An object of type "scalar" can be :

- null

- logical

- numeric

- complex

- character

```{r echo=T, eval=F}
#Scalar
a <- 1
b <- "Le Séminaire Automat"
b1 <- FALSE
```

To know the class of an object:

```{r echo=T, eval=F}
class(object)
mode(object)
```


## Vector

\small

Numeric vector:
```{r echo=T, eval=F}
#Vecteur
c <- c(3, 4, 5, 6)
d <- c(7, 8, 9, 10)
```

Build a numerical vector:
```{r echo=T}
seq(1,10,by=1)
```

```{r echo=T}
rep(1,8)
```


Character vector:
```{r echo=T, eval=F}
e <- c("Initiation", "_", "R")
```


## Matrix and list

Matrix $\rightarrow$ atomic objects i.e. same mode or type for all values.
```{r echo=T, eval=F}
#Matrix
matrix_1 <- matrix(1, nrow = 4, ncol=1)

length(matrix_1)
dim(matrix_1)

```


List $\rightarrow$ a heterogeneous object i.e. an ordered set of objects that do not always have the same mode or the same length.
```{r echo=T, eval=F}
#Liste 
i <- list(b, d, matrix_1, "h")
j <- list(i, "Poupée russe de liste")
```



## Data-frame

Data-frame $\rightarrow$ particular list whose components are of the same length, but whose modes can differ (quantative and qualitative variables measured on the same individuals).

```{r echo=T}
#Data frame
taille <- c(152, 156, 160, 160, 163, 167, 169, 173, 174, 174)
masse <- c(51, 51, 54, 60, 61, 64, 70, 71, 72, 73)
sexe <-c("M","F","F","M", "M","F","F","M", "F", "F")
df <- data.frame(taille,masse,sexe)
print(df)
```

## Functions (I)

- An R object, many of which are already predefined in R, but which can also be created.

- A function admits arguments as input and returns a result as output.

Functions mean and sd : 

```{r echo=T}
mean(df$taille)
var(df$taille)
sd(df$taille)
```

## Functions (II)

Function rnorm : 

- Generates random numbers following a normal distribution

- Takes three arguments: n the number of values, mean the mean (default =0) and sd the standard deviation of the law (default =1).

```{r echo=T}
set.seed(140) # fixer la graine du générateur ... permet de retrouver les mêmes résultats d'une simulation à l'autre.
rnorm(n=4)
```


# Exercice

## Write his first R function

\begin{equation}
\bar{x} = \frac{1}{n} \times \sum_{i=1}^{n} x_i
\end{equation}

```{r echo=T}
my_function1 <- function(var_x){
  sum_x <- sum(var_x)
  n_x <- length(var_x)
  mean_x = sum_x/n_x
  mean_x
}

my_function1(df$taille)
```

## Now, it's your turn (I)

The calculation of the sample variance

\begin{equation}
V(x) = \frac{1}{n-1} \times \sum_{i=1}^{n} (x_i - \bar{x})^2
\end{equation}

Find the same results as the Variance function by writing the function yourself.



## Solution (I)

```{r echo=T}
my_function2 <- function(var_x){
  mean_x <- my_function1(var_x)
  n_x <- length(var_x)
  sum_diff_2 <- sum((var_x-mean_x)^2)
  Variance_x <- (sum_diff_2/(n_x-1))
  Variance_x
}

my_function2(df$taille)
```


## Now, it's your turn (II)

The calculation of the covariance

\begin{equation}
Cov(x,y) = \sum_{i=1}^{n} \frac{(x_i - \bar{x})(y_i - \bar{y})}{n-1}
\end{equation}

```{r echo=T}
cov(df$taille, df$masse)
```

## Solution (II)

```{r echo=T}
my_function3 <- function(var_x, var_y){
  mean_x <- my_function1(var_x)
  mean_y <- my_function1(var_y)
  n_x <- length(var_x)
  Covar_x_y <- sum((var_x-mean_x)*(var_y-mean_y)/(n_x-1))
  Covar_x_y
}

my_function3(df$taille,df$masse)
```

