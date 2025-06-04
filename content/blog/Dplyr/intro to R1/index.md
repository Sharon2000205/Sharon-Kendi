---
title: "Introduction to Statistical Data Analysis using R"
weight: 1
subtitle: "Introduction to R"
excerpt: "R is a programming language used for statistical analysis, data visualization, and data science. It’s known for its powerful data manipulation capabilities, extensive libraries, and active community, making it ideal for handling complex data and creating visual reports."
date: 2024-09-01
draft: false
---
## Introduction

### Basic Syntax in R:

- Commands: R uses functions and commands written directly in the console or script files.
- Comments: Use # to write comments in your code (e.g., # This is a comment).
- Assignment: The assignment operator <- is commonly used to assign values (e.g., x <- 5).
- Printing: Use print() or simply type the variable name to display its value (e.g., print(x) or x).


``` r
#This is a comment
x <- 5
print(x)
```

```
## [1] 5
```

## Common Data Types in R:

- Numeric: Numbers with decimals (e.g., 5.3, 2.0).
- Integer: Whole numbers, defined by appending L (e.g., 3L).
- Character: Strings or text (e.g., "Hello, R").
- Logical: Boolean values (TRUE, FALSE).
- Complex: Complex numbers (e.g., 1 + 2i).


``` r
#Numeric
y <- c(5.8,10,0.1)
is.numeric(y)
```

```
## [1] TRUE
```

``` r
#character
z<- ('Hello')
is.character(z)
```

```
## [1] TRUE
```

``` r
#complex
a <-  1 + 2i
is.complex(a)
```

```
## [1] TRUE
```

``` r
log_var <- TRUE
is.logical(log_var)
```

```
## [1] TRUE
```

## Basic Data Structures:

- Vector: A sequence of elements of the same type (e.g., c(1, 2, 3)).
- List: A collection that can hold different types (e.g., list(1, "text", TRUE)).
- Matrix: A 2D array with elements of the same type (e.g., matrix(1:6, nrow = 2)).
- Data Frame: A table-like structure with columns of different types (e.g., data.frame(name = c("A", "B"), age = c(25, 30))).


``` r
# Vector
vec <- c(1, 2, 3, 4)
print(vec)    
```

```
## [1] 1 2 3 4
```

``` r
#list
lst <- list(1, "R", TRUE, 3 + 2i)
print(lst) 
```

```
## [[1]]
## [1] 1
## 
## [[2]]
## [1] "R"
## 
## [[3]]
## [1] TRUE
## 
## [[4]]
## [1] 3+2i
```

``` r
#matrix
mat <- matrix(1:6, nrow = 2)
print(mat)
```

```
##      [,1] [,2] [,3]
## [1,]    1    3    5
## [2,]    2    4    6
```

``` r
#dataframe
df <- data.frame(name = c("Alice", "Bob"), 
                 age = c(25, 30))
print(df)
```

```
##    name age
## 1 Alice  25
## 2   Bob  30
```

