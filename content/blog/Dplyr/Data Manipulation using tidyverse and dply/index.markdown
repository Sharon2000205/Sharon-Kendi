---
title: "Data Manipulation using tidyverse and dplyr"
weight: 3
subtitle: ""
excerpt: "Data manipulation is a crucial step in data analysis, and R offers powerful packages like dplyr and tidyverse to simplify this process. These packages provide intuitive functions for filtering, transforming, and summarizing data efficiently."
date: 2024-09-09
draft: false
---
**Tidyverse** is a collection of R packages designed for data science, providing tools for data manipulation, visualization, and analysis. It includes packages like ggplot2 (for plotting), dplyr (for data manipulation), tidyr (for reshaping data), and more, all built around a consistent design philosophy.

**dplyr** is a package within the tidyverse focused specifically on data manipulation. It provides a set of intuitive functions like filter(), select(), mutate(), summarize(), and arrange() to perform operations such as filtering, selecting, transforming, summarizing, and sorting data in a straightforward and readable way.


``` r
library(dplyr)
```

```
## 
## Attaching package: 'dplyr'
```

```
## The following objects are masked from 'package:stats':
## 
##     filter, lag
```

```
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

``` r
library(tidyverse)  # `tidyverse` includes `dplyr` and other helpful packages
```

```
## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
## ✔ forcats   1.0.0     ✔ readr     2.1.5
## ✔ ggplot2   3.5.1     ✔ stringr   1.5.1
## ✔ lubridate 1.9.3     ✔ tibble    3.2.1
## ✔ purrr     1.0.2     ✔ tidyr     1.3.1
```

```
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors
```


``` r
#Create a dummy dataset
data <- data.frame(
  name = c("Alice", "Bob", "Charlie", "David", "Eva", "Frank", "Grace", "Hannah", "Ian", "Jack"),
  age = c(23, 35, 45, 29, 33, 50, 28, 41, 36, 27),
  gender = c("F", "M", "M", "M", "F", "M", "F", "F", "M", "M"),
  income = c(50000, 60000, 80000, 55000, 65000, 90000, 45000, 70000, 75000, 48000)
)
print(head(data))
```

```
##      name age gender income
## 1   Alice  23      F  50000
## 2     Bob  35      M  60000
## 3 Charlie  45      M  80000
## 4   David  29      M  55000
## 5     Eva  33      F  65000
## 6   Frank  50      M  90000
```
## Filtering Data

Use filter() to subset rows based on conditions.


``` r
# Filter rows where age is greater than 30
filtered_data <- data %>% 
  filter(age > 30)
filtered_data
```

```
##      name age gender income
## 1     Bob  35      M  60000
## 2 Charlie  45      M  80000
## 3     Eva  33      F  65000
## 4   Frank  50      M  90000
## 5  Hannah  41      F  70000
## 6     Ian  36      M  75000
```
## Selecting Columns

Use select() to pick specific columns.

``` r
# Select only the 'name' and 'age' columns
selected_data <- data %>% 
  select(name, age)

selected_data
```

```
##       name age
## 1    Alice  23
## 2      Bob  35
## 3  Charlie  45
## 4    David  29
## 5      Eva  33
## 6    Frank  50
## 7    Grace  28
## 8   Hannah  41
## 9      Ian  36
## 10    Jack  27
```
## Mutating (Adding New Columns)

Use mutate() to create new columns or modify existing ones.

``` r
# Add a new column 'age_in_5_years'
mutated_data <- data %>% 
  mutate(age_in_5_years = age + 5)
mutated_data
```

```
##       name age gender income age_in_5_years
## 1    Alice  23      F  50000             28
## 2      Bob  35      M  60000             40
## 3  Charlie  45      M  80000             50
## 4    David  29      M  55000             34
## 5      Eva  33      F  65000             38
## 6    Frank  50      M  90000             55
## 7    Grace  28      F  45000             33
## 8   Hannah  41      F  70000             46
## 9      Ian  36      M  75000             41
## 10    Jack  27      M  48000             32
```
## Arranging (Sorting) Data

Use arrange() to sort data.

``` r
# Sort data by age in descending order
sorted_data <- data %>% 
  arrange(desc(age))
sorted_data
```

```
##       name age gender income
## 1    Frank  50      M  90000
## 2  Charlie  45      M  80000
## 3   Hannah  41      F  70000
## 4      Ian  36      M  75000
## 5      Bob  35      M  60000
## 6      Eva  33      F  65000
## 7    David  29      M  55000
## 8    Grace  28      F  45000
## 9     Jack  27      M  48000
## 10   Alice  23      F  50000
```
## Summarizing Data

Use summarize() to calculate summary statistics, often with group_by() to aggregate data.

``` r
# Calculate the average income
average_income <- data %>% 
  summarize(avg_income = mean(income, na.rm = TRUE))
print(average_income)
```

```
##   avg_income
## 1      63800
```

``` r
# Group by gender and calculate average income for each gender
grouped_data <- data %>% 
  group_by(gender) %>% 
  summarize(avg_income = mean(income, na.rm = TRUE))
print(grouped_data)
```

```
## # A tibble: 2 × 2
##   gender avg_income
##   <chr>       <dbl>
## 1 F           57500
## 2 M           68000
```
## Combining Operations

You can chain multiple operations together using the pipe operator (%>%).

``` r
# Filter for age greater than 30, select name and income, and sort by income
combined_data <- data %>%
  filter(age > 30) %>%
  select(name, income) %>%
  arrange(desc(income))
print(combined_data)
```

```
##      name income
## 1   Frank  90000
## 2 Charlie  80000
## 3     Ian  75000
## 4  Hannah  70000
## 5     Eva  65000
## 6     Bob  60000
```
## Other Helpful Functions

- distinct(): Removes duplicate rows.
- rename(): Renames columns.
- join(): Combines two data frames by a common column.

## Rename a column


``` r
renamed_data <- data %>% rename(annual_income = income)
print(renamed_data)
```

```
##       name age gender annual_income
## 1    Alice  23      F         50000
## 2      Bob  35      M         60000
## 3  Charlie  45      M         80000
## 4    David  29      M         55000
## 5      Eva  33      F         65000
## 6    Frank  50      M         90000
## 7    Grace  28      F         45000
## 8   Hannah  41      F         70000
## 9      Ian  36      M         75000
## 10    Jack  27      M         48000
```

## Remove duplicates based on specific columns


``` r
distinct_data <- data %>% distinct(name, .keep_all = TRUE)
print(distinct_data)
```

```
##       name age gender income
## 1    Alice  23      F  50000
## 2      Bob  35      M  60000
## 3  Charlie  45      M  80000
## 4    David  29      M  55000
## 5      Eva  33      F  65000
## 6    Frank  50      M  90000
## 7    Grace  28      F  45000
## 8   Hannah  41      F  70000
## 9      Ian  36      M  75000
## 10    Jack  27      M  48000
```

### Summary

Using tidyverse and dplyr, you can efficiently manipulate data by filtering, transforming, summarizing, and sorting it. These functions are concise, and work seamlessly together, allowing for clean and readable code.




