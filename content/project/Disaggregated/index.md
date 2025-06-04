---
title: "Disaggregated data from surveys"
subtitle: "How to analyze survey data."
excerpt: ""
date: 2024-10-24
author: "Kelvin Kiprono"
draft: false
# layout options: single, single-sidebar
layout: single
categories:
- R Data Analysis
---


Disaggregated data from surveys involves breaking down survey responses into smaller, more specific groups based on different characteristics or categories. This allows for more detailed analysis and helps to identify patterns, trends, or disparities that may not be visible in the aggregated data. The process of disaggregation can reveal important insights, particularly when working with diverse populations or when the goal is to make data-driven decisions that are inclusive and representative of different groups.

### How Disaggregated Data is Created from Surveys

- Survey Design:

Before collecting data, the survey needs to be designed with questions that allow for the segmentation of responses. These questions should ask for variables that can be categorized, such as age, gender, region, or income.

- Data Collection:

During data collection, responses are recorded in a way that each respondent's answers can be associated with specific demographic or other contextual variables.

- Data Segmentation:

After the survey is completed, the data is analyzed by dividing it into sub-groups. This can be done by categorizing respondents according to different criteria:
  - Demographic Variables: Age, gender, ethnicity, education, occupation, etc.
  - Geographic Variables: Region, urban vs. rural, country, etc.
  - Behavioral Variables: Employment status, health behaviors, or purchasing patterns.

- Analysis of Disaggregated Data:

Once the data is segmented, it is analyzed to reveal how different groups within the survey sample respond to specific questions. This allows for comparisons to be made between groups. For example, you might compare how men and women responded to a question on workplace satisfaction or how different income groups feel about healthcare access.

## Examples of Disaggregated Data from Surveys

- Income and Education Level in a Survey about Access to Technology:

   - Aggregated Data: 70% of survey respondents report having access to a computer.
   - Disaggregated Data:
   
     - 85% of individuals with a high school education or less report having access to a computer.
     - 95% of individuals with a college degree or higher report having access to a computer.
     - 60% of respondents with an annual income under $20,000 report having access to a computer, while 80% of those earning above $50,000 have access.

## Why Disaggregate Survey Data?

- Identifying Inequalities and Disparities:

Disaggregation allows you to identify differences between groups that might not be evident in the overall data. For example, if there are significant gaps in satisfaction between men and women, or if rural populations have less access to services, this can inform targeted interventions.

- Targeted Decision Making:

Policy makers and businesses can use disaggregated data to make decisions that are more specific to the needs of certain groups. For instance, a government might use disaggregated survey data on healthcare to allocate more resources to underserved areas.

- Improving Program Design:

Disaggregated data helps organizations tailor their programs to meet the needs of specific sub-groups. For example, a nonprofit working on educational programs might disaggregate data by age or socioeconomic status to design programs that address the unique challenges of different populations.

- Transparency and Accountability:

Disaggregation can help ensure that all groups, especially marginalized or underrepresented populations, are considered in the data analysis and that they are not overlooked in decision-making processes.

## Common Variables for Disaggregation in Survey Data
- Demographic Variables: Age, gender, income level, educational attainment, family status.
- Geographic Variables: Urban vs. rural, region, country, neighborhood.
- Health and Disability Variables: Chronic conditions, disability status.
- Ethnic or Cultural Background: Race, ethnicity, or cultural affiliation.
- Socioeconomic Variables: Employment status, income level, job sector.


## Preparing data for analysis


``` r
library(readxl)
sample_data_1<- read_excel("C:/Users/hp/Downloads/sample_data_1_1_.xlsx")
```

## Exploring the data

``` r
library(tidyverse)
```

```
## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
## ✔ dplyr     1.1.4     ✔ readr     2.1.5
## ✔ forcats   1.0.0     ✔ stringr   1.5.1
## ✔ ggplot2   3.5.1     ✔ tibble    3.2.1
## ✔ lubridate 1.9.3     ✔ tidyr     1.3.1
## ✔ purrr     1.0.2     
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors
```

``` r
library(dplyr)
library(haven)
```
Using glimpse form the dplyr package we are able to see how our data looks like.Also using head() and tail() we can see the first five rows and last 5 rows.


``` r
glimpse(sample_data_1)
```

```
## Rows: 2,677
## Columns: 21
## $ id     <dbl> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, …
## $ psu    <dbl> 1427, 1859, 891, 1652, 20, 1962, 1618, 1063, 1567, 536, 1454, 1…
## $ weight <dbl> 1.253567, 0.187608, 1.889372, 0.788736, 0.358671, 1.354536, 0.7…
## $ strata <chr> "south kalimantan rural", "maluku rural", "central java urban",…
## $ v012   <dbl> 31, 24, 37, 26, 37, 34, 32, 35, 24, 31, 42, 36, 34, 39, 30, 28,…
## $ v025   <chr> "rural", "rural", "urban", "rural", "rural", "rural", "urban", …
## $ v149   <chr> "incomplete primary", "incomplete secondary", "incomplete secon…
## $ v190   <chr> "poorest", "poorest", "middle", "poorest", "poorer", "poorest",…
## $ b4     <chr> "female", "female", "female", "male", "male", "male", "female",…
## $ b5     <chr> "yes", "yes", "yes", "yes", "yes", "yes", "yes", "yes", "yes", …
## $ b19    <dbl> 28, 27, 26, 50, 29, 19, 59, 1, 4, 6, 49, 48, 28, 40, 31, 33, 15…
## $ m3a    <chr> "no", "no", "no", "no", "no", "no", "no", "no", "no", "no", "no…
## $ m3b    <chr> "no", "no", "no", "no", "yes", "no", "no", "no", "no", "yes", "…
## $ m3c    <chr> "no", "no", "no", "no", "no", "no", "yes", "no", "no", "yes", "…
## $ m3d    <chr> "no", "no", "no", "yes", "no", "no", "yes", "no", "no", "no", "…
## $ m3e    <chr> "no", "no", "no", "no", "no", "yes", "no", "yes", "yes", "no", …
## $ m3g    <chr> "yes", "yes", "yes", "no", "no", "no", "no", "yes", "no", "no",…
## $ m3h    <chr> "no", "no", "yes", "yes", "no", "yes", "no", "no", "no", "no", …
## $ m3k    <chr> "no", "no", "no", "no", "no", "no", "no", "no", "no", "no", "no…
## $ m3n    <chr> "no: some assistance", "no: some assistance", "no: some assista…
## $ h7     <chr> "vaccination date on card", "reported by mother", "no", NA, "re…
```

``` r
head(sample_data_1,5)
```

```
## # A tibble: 5 × 21
##      id   psu weight strata       v012 v025  v149  v190  b4    b5      b19 m3a  
##   <dbl> <dbl>  <dbl> <chr>       <dbl> <chr> <chr> <chr> <chr> <chr> <dbl> <chr>
## 1     1  1427  1.25  south kali…    31 rural inco… poor… fema… yes      28 no   
## 2     2  1859  0.188 maluku rur…    24 rural inco… poor… fema… yes      27 no   
## 3     3   891  1.89  central ja…    37 urban inco… midd… fema… yes      26 no   
## 4     4  1652  0.789 south sula…    26 rural inco… poor… male  yes      50 no   
## 5     5    20  0.359 aceh rural     37 rural comp… poor… male  yes      29 no   
## # ℹ 9 more variables: m3b <chr>, m3c <chr>, m3d <chr>, m3e <chr>, m3g <chr>,
## #   m3h <chr>, m3k <chr>, m3n <chr>, h7 <chr>
```

``` r
tail(sample_data_1,5)
```

```
## # A tibble: 5 × 21
##      id   psu weight strata       v012 v025  v149  v190  b4    b5      b19 m3a  
##   <dbl> <dbl>  <dbl> <chr>       <dbl> <chr> <chr> <chr> <chr> <chr> <dbl> <chr>
## 1  2673  1366  1.07  west kalim…    36 rural comp… poor… male  yes      24 no   
## 2  2674  1294  0.360 east nusa …    29 rural comp… poor… male  yes      28 no   
## 3  2675   346  1.99  south suma…    32 rural inco… rich… fema… yes      10 no   
## 4  2676  1734  0.375 gorontalo …    28 rural comp… poor… male  yes      26 no   
## 5  2677   812  1.78  central ja…    36 urban comp… rich… fema… yes      52 no   
## # ℹ 9 more variables: m3b <chr>, m3c <chr>, m3d <chr>, m3e <chr>, m3g <chr>,
## #   m3h <chr>, m3k <chr>, m3n <chr>, h7 <chr>
```

Obtaining the summary to get the picture of our data


``` r
summary(sample_data_1)
```

```
##        id            psu             weight           strata         
##  Min.   :   1   Min.   :   1.0   Min.   :0.06359   Length:2677       
##  1st Qu.: 670   1st Qu.: 451.0   1st Qu.:0.35909   Class :character  
##  Median :1339   Median :1022.0   Median :0.84843   Mode  :character  
##  Mean   :1339   Mean   : 993.2   Mean   :0.94872                     
##  3rd Qu.:2008   3rd Qu.:1522.0   3rd Qu.:1.41101                     
##  Max.   :2677   Max.   :1970.0   Max.   :5.40138                     
##       v012           v025               v149               v190          
##  Min.   :15.00   Length:2677        Length:2677        Length:2677       
##  1st Qu.:26.00   Class :character   Class :character   Class :character  
##  Median :31.00   Mode  :character   Mode  :character   Mode  :character  
##  Mean   :30.91                                                           
##  3rd Qu.:36.00                                                           
##  Max.   :49.00                                                           
##       b4                 b5                 b19            m3a           
##  Length:2677        Length:2677        Min.   : 0.00   Length:2677       
##  Class :character   Class :character   1st Qu.:15.00   Class :character  
##  Mode  :character   Mode  :character   Median :30.00   Mode  :character  
##                                        Mean   :29.97                     
##                                        3rd Qu.:45.00                     
##                                        Max.   :59.00                     
##      m3b                m3c                m3d                m3e           
##  Length:2677        Length:2677        Length:2677        Length:2677       
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      m3g                m3h                m3k                m3n           
##  Length:2677        Length:2677        Length:2677        Length:2677       
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##       h7           
##  Length:2677       
##  Class :character  
##  Mode  :character  
##                    
##                    
## 
```

## Sample sizes for education subgroup


``` r
sample_data_1 %>%
  group_by(v149) %>%
  summarise(n())
```

```
## # A tibble: 6 × 2
##   v149                 `n()`
##   <chr>                <int>
## 1 complete primary       469
## 2 complete secondary     805
## 3 higher                 493
## 4 incomplete primary     216
## 5 incomplete secondary   647
## 6 no education            47
```

## Sample sizes and proportion of records for education subgroup


``` r
sample_data_1 %>%
  group_by(v149) %>%
  summarise(n = n()) %>%
  mutate(p = n/sum(n))
```

```
## # A tibble: 6 × 3
##   v149                     n      p
##   <chr>                <int>  <dbl>
## 1 complete primary       469 0.175 
## 2 complete secondary     805 0.301 
## 3 higher                 493 0.184 
## 4 incomplete primary     216 0.0807
## 5 incomplete secondary   647 0.242 
## 6 no education            47 0.0176
```

## Constructing health indicators (skilled birth attendance)

``` r
sample_data_1a <- sample_data_1 %>%
  mutate(sba =
           if_else(m3a == "yes"|
                   m3b == "yes"|
                   m3c == "yes"|
                   m3d == "yes",
                   1,0)
         )
```

# Tabulate *sba* variable (skilled birth attendance)

``` r
count(sample_data_1a, sba)
```

```
## # A tibble: 3 × 2
##     sba     n
##   <dbl> <int>
## 1     0   594
## 2     1  2072
## 3    NA    11
```

# # Replacing missing values in *sba* with zeros and inspecting results

``` r
sample_data_1b <- sample_data_1a %>%
  mutate(sba =
           if_else(m3a == "yes"|
                   m3b == "yes"|
                   m3c == "yes"|
                   m3d == "yes",
                   1,0,0)
         )
count(sample_data_1b, sba)
```

```
## # A tibble: 2 × 2
##     sba     n
##   <dbl> <int>
## 1     0   605
## 2     1  2072
```

# Inspecting R objects

``` r
sample_data_1b
```

```
## # A tibble: 2,677 × 22
##       id   psu weight strata      v012 v025  v149  v190  b4    b5      b19 m3a  
##    <dbl> <dbl>  <dbl> <chr>      <dbl> <chr> <chr> <chr> <chr> <chr> <dbl> <chr>
##  1     1  1427  1.25  south kal…    31 rural inco… poor… fema… yes      28 no   
##  2     2  1859  0.188 maluku ru…    24 rural inco… poor… fema… yes      27 no   
##  3     3   891  1.89  central j…    37 urban inco… midd… fema… yes      26 no   
##  4     4  1652  0.789 south sul…    26 rural inco… poor… male  yes      50 no   
##  5     5    20  0.359 aceh rural    37 rural comp… poor… male  yes      29 no   
##  6     6  1962  1.35  papua rur…    34 rural inco… poor… male  yes      19 no   
##  7     7  1618  0.782 south sul…    32 urban high… midd… fema… yes      59 no   
##  8     8  1063  2.36  east java…    35 rural inco… poor… male  yes       1 no   
##  9     9  1567  0.348 central s…    24 rural comp… rich… male  yes       4 no   
## 10    10   536  0.977 jakarta u…    31 urban high… rich… male  yes       6 no   
## # ℹ 2,667 more rows
## # ℹ 10 more variables: m3b <chr>, m3c <chr>, m3d <chr>, m3e <chr>, m3g <chr>,
## #   m3h <chr>, m3k <chr>, m3n <chr>, h7 <chr>, sba <dbl>
```

``` r
head(sample_data_1b$sba , n = 10)
```

```
##  [1] 0 0 0 1 1 0 1 0 0 1
```

## Constructing inequality dimensions

# Mother's age categories (variable v012)

``` r
summary(sample_data_1b$v012)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##   15.00   26.00   31.00   30.91   36.00   49.00
```

``` r
sample_data_1c <- sample_data_1b %>%
  mutate(mage =
           as.factor(case_when(
             v012 < 20 ~ '15-19 years',
             v012 >= 20 & v012 <= 34 ~ '20-34 years',
             v012 >= 35 & v012 <= 49 ~ '35-49 years')
           )
  )

levels(sample_data_1c$mage)
```

```
## [1] "15-19 years" "20-34 years" "35-49 years"
```

``` r
count(sample_data_1c, mage)
```

```
## # A tibble: 3 × 2
##   mage            n
##   <fct>       <int>
## 1 15-19 years    72
## 2 20-34 years  1793
## 3 35-49 years   812
```

## Socioeconomic status (variable v190)

``` r
sample_data_1d <- sample_data_1c %>%
  mutate(quintile =
           fct_recode(v190,
                      "Quintile 1 (poorest)" = "poorest",
                      "Quintile 2" = "poorer",
                      "Quintile 3" = "middle",
                      "Quintile 4" = "richer",
                      "Quintile 5 (richest)" = "richest")
  )

count(sample_data_1d, quintile)
```

```
## # A tibble: 5 × 2
##   quintile                 n
##   <fct>                <int>
## 1 Quintile 3             491
## 2 Quintile 2             508
## 3 Quintile 1 (poorest)   747
## 4 Quintile 4             476
## 5 Quintile 5 (richest)   455
```
## Mother's education (variable v149)

``` r
count(sample_data_1d, v149)
```

```
## # A tibble: 6 × 2
##   v149                     n
##   <chr>                <int>
## 1 complete primary       469
## 2 complete secondary     805
## 3 higher                 493
## 4 incomplete primary     216
## 5 incomplete secondary   647
## 6 no education            47
```

``` r
sample_data_1e <- sample_data_1d %>%
  mutate(educatt =
           fct_recode(v149,
                      "No or primary education" = "no education",
                      "No or primary education" = "incomplete primary",
                      "No or primary education" = "complete primary",
                      "Secondary or higher education" = "incomplete secondary",
                      "Secondary or higher education" = "complete secondary",
                      "Secondary or higher education" = "higher")
  )

count(sample_data_1e, educatt)
```

```
## # A tibble: 2 × 2
##   educatt                           n
##   <fct>                         <int>
## 1 No or primary education         732
## 2 Secondary or higher education  1945
```

## Place of residence (variable v025)


``` r
sample_data_1f <- sample_data_1e %>%
  mutate(urban =
           fct_recode(v025,
                      "Urban" = "urban",
                      "Rural" = "rural")
  )

count(sample_data_1f, urban)
```

```
## # A tibble: 2 × 2
##   urban     n
##   <fct> <int>
## 1 Rural  1353
## 2 Urban  1324
```
## Finalizing data object preparation by selecting specified variables


``` r
sample_data_2 <- sample_data_1f %>%
  select(psu,
         weight,
         strata,
         sba,
         mage,
         quintile,
         educatt,
         urban)
```

## Calculating disaggregated estimates using R


``` r
library(survey)
```

```
## Loading required package: grid
```

```
## Loading required package: Matrix
```

```
## 
## Attaching package: 'Matrix'
```

```
## The following objects are masked from 'package:tidyr':
## 
##     expand, pack, unpack
```

```
## Loading required package: survival
```

```
## 
## Attaching package: 'survey'
```

```
## The following object is masked from 'package:graphics':
## 
##     dotchart
```

# Specifying complex survey design using svydesign() function

``` r
sample_data_2_design <- svydesign(id = ~ psu,
                                  weights = ~ weight,
                                  strata = ~ strata,
                                  data = sample_data_2)

summary(sample_data_2_design)
```

```
## Stratified 1 - level Cluster Sampling design (with replacement)
## With (1436) clusters.
## svydesign(id = ~psu, weights = ~weight, strata = ~strata, data = sample_data_2)
## Probabilities:
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##  0.1851  0.7087  1.1786  2.1163  2.7848 15.7252 
## Stratum Sizes: 
##            aceh rural aceh urban bali rural bali urban bangka belitung rural
## obs               104         45          8         23                    18
## design.PSU         52         22          7         14                     8
## actual.PSU         52         22          7         14                     8
##            bangka belitung urban banten rural banten urban bengkulu rural
## obs                           23           28           67             31
## design.PSU                    13           16           35             17
## actual.PSU                    13           16           35             17
##            bengkulu urban central java rural central java urban
## obs                    13                 71                 76
## design.PSU              6                 47                 48
## actual.PSU              6                 47                 48
##            central kalimantan rural central kalimantan urban
## obs                              19                       17
## design.PSU                       11                        8
## actual.PSU                       11                        8
##            central sulawesi rural central sulawesi urban east java rural
## obs                            42                     26              73
## design.PSU                     25                     12              46
## actual.PSU                     25                     12              46
##            east java urban east kalimantan rural east kalimantan urban
## obs                     79                    20                    54
## design.PSU              55                    11                    29
## actual.PSU              55                    11                    29
##            east nusa tenggara rural east nusa tenggara urban gorontalo rural
## obs                             120                       30              16
## design.PSU                       57                       16               8
## actual.PSU                       57                       16               8
##            gorontalo urban jakarta urban jambi rural jambi urban lampung rural
## obs                     19            96          17          12            51
## design.PSU               7            49          10           9            28
## actual.PSU               7            49          10           9            28
##            lampung urban maluku rural maluku urban north kalimantan rural
## obs                   19           66           44                     27
## design.PSU            12           31           25                     10
## actual.PSU            12           31           25                     10
##            north kalimantan urban north maluku rural north maluku urban
## obs                            23                 56                 15
## design.PSU                     10                 25                  9
## actual.PSU                     10                 25                  9
##            north sulawesi rural north sulawesi urban north sumatera rural
## obs                           7                   10                   94
## design.PSU                    7                    7                   38
## actual.PSU                    7                    7                   38
##            north sumatera urban papua rural papua urban riau islands rural
## obs                          79          33           9                  3
## design.PSU                   39          17           6                  2
## actual.PSU                   39          17           6                  2
##            riau islands urban riau rural riau urban south kalimantan rural
## obs                        50         29         21                     18
## design.PSU                 25         17          9                     13
## actual.PSU                 25         17          9                     13
##            south kalimantan urban south sulawesi rural south sulawesi urban
## obs                            24                   44                   44
## design.PSU                     13                   25                   20
## actual.PSU                     13                   25                   20
##            south sumatera rural south sumatera urban southeast sulawesi rural
## obs                          41                   21                       59
## design.PSU                   22                   10                       32
## actual.PSU                   22                   10                       32
##            southeast sulawesi urban west java rural west java urban
## obs                              36              57             209
## design.PSU                       18              31             110
## actual.PSU                       18              31             110
##            west kalimantan rural west kalimantan urban west nusa tenggara rural
## obs                           35                    17                       30
## design.PSU                    20                     8                       20
## actual.PSU                    20                     8                       20
##            west nusa tenggara urban west papua rural west papua urban
## obs                              40               25               13
## design.PSU                       19                9                5
## actual.PSU                       19                9                5
##            west sulawesi rural west sulawesi urban west sumatera rural
## obs                         61                  25                  45
## design.PSU                  36                  15                  21
## actual.PSU                  36                  15                  21
##            west sumatera urban yogyakarta rural yogyakarta urban
## obs                         25                5               20
## design.PSU                  14                3               17
## actual.PSU                  14                3               17
## Data variables:
## [1] "psu"      "weight"   "strata"   "sba"      "mage"     "quintile" "educatt" 
## [8] "urban"
```
## Calculating  national averages and corresponding confidence intervals using svymean


``` r
svymean1 <- svymean(~ sba,
                    design = sample_data_2_design)

confint(svymean1)
```

```
##         2.5 %    97.5 %
## sba 0.7852454 0.8272781
```

# Calculating national averages and corresponding confidencce intervals using svyciprop


``` r
svyciprop(~ sba,
          design = sample_data_2_design)
```

```
##            2.5% 97.5%
## sba 0.806 0.784 0.826
```

## Calculating disaggregated estimates for *sba* by wealth quintile

``` r
svyby(~ sba,
      by = ~ quintile,
      design = sample_data_2_design,
      FUN = svymean,
      vartype = c("se", "ci"),
      keep.names = F)
```

```
##               quintile       sba         se      ci_l      ci_u
## 1           Quintile 3 0.8734299 0.01748832 0.8391534 0.9077064
## 2           Quintile 2 0.7439339 0.02677458 0.6914567 0.7964111
## 3 Quintile 1 (poorest) 0.5733626 0.02838101 0.5177368 0.6289884
## 4           Quintile 4 0.9048578 0.01742623 0.8707030 0.9390126
## 5 Quintile 5 (richest) 0.9547576 0.01142862 0.9323579 0.9771573
```
## Calculating disaggregated estimates for *sba* by education level

``` r
svyby(~ sba,
      by = ~ educatt,
      design = sample_data_2_design,
      FUN = svymean,
      vartype = c("se", "ci"),
      keep.names = F)
```

```
##                         educatt       sba         se      ci_l      ci_u
## 1       No or primary education 0.6459142 0.02560354 0.5957322 0.6960962
## 2 Secondary or higher education 0.8703938 0.00937096 0.8520270 0.8887605
```
## Calculating disaggregated estimates for *sba* by place of residence

``` r
svyby(~ sba,
      by = ~ urban,
      design = sample_data_2_design,
      FUN = svymean,
      vartype = c("se", "ci"),
      keep.names = F)
```

```
##   urban       sba         se      ci_l      ci_u
## 1 Rural 0.7027926 0.01827014 0.6669838 0.7386014
## 2 Urban 0.9137114 0.01006922 0.8939761 0.9334467
```
## Calculating disaggregated estimates for a specific subgroup (e.g. urban areas)

``` r
urban_subset_design <- subset(sample_data_2_design, urban == 'Urban')

urban_subset_calc <- svyby(~ sba,
                           by = ~ urban,
                           design = urban_subset_design,
                           FUN = svymean,
                           vartype = c("se", "ci"),
                           keep.names = F)

urban_subset_calc
```

```
##   urban       sba         se      ci_l      ci_u
## 1 Urban 0.9137114 0.01006922 0.8939761 0.9334467
```
## Disaggregation by two dimensions of inequality (double disaggregation)

``` r
svyby(~ sba,
      by = ~ urban + educatt,
      design = sample_data_2_design,
      FUN = svymean,
      vartype = c("se", "ci"),
      keep.names = F)
```

```
##   urban                       educatt       sba         se      ci_l      ci_u
## 1 Rural       No or primary education 0.5452402 0.03449799 0.4776254 0.6128550
## 2 Urban       No or primary education 0.8381728 0.02806428 0.7831679 0.8931778
## 3 Rural Secondary or higher education 0.7945583 0.01692552 0.7613849 0.8277317
## 4 Urban Secondary or higher education 0.9326135 0.01005420 0.9129077 0.9523194
```
# Unweighted sample size

``` r
nrow(sample_data_2)
```

```
## [1] 2677
```
# Unweighted sample sizes for dimension of inequality subgroups

``` r
count(sample_data_2, quintile)
```

```
## # A tibble: 5 × 2
##   quintile                 n
##   <fct>                <int>
## 1 Quintile 3             491
## 2 Quintile 2             508
## 3 Quintile 1 (poorest)   747
## 4 Quintile 4             476
## 5 Quintile 5 (richest)   455
```
# National average weighted population sizes

``` r
sample_data_2 <- sample_data_2 %>%
  mutate(size = 1)
```

``` r
sample_data_2_design <- svydesign(id = ~ psu,
                                  weights = ~ weight,
                                  strata = ~ strata,
                                  data = sample_data_2)

svytotal(~ size,
         design = sample_data_2_design)
```

```
##       total     SE
## size 2539.7 47.081
```
# Weighted population sizes for dimension of inequality subgroups

``` r
sba_urban <- svyby(~ sba,
                   by = ~ urban,
                   design = sample_data_2_design,
                   FUN = svymean,
                   vartype = c("se", "ci")
                   )
```


## Creating a function to calculate disaggregated estimates for several dimensions of inequality

``` r
svyby_disaggregated <- function(variables){
  svyby(~ sba,
        by = reformulate(variables),
        design = sample_data_2_design,
        FUN = svymean,
        vartype = c("se", "ci"),
        keep.names = F)
}
```
## Identify list of dimension of inequality variables

``` r
variables <- c('urban', 'quintile', 'educatt', 'mage')
```

## Apply function svyby_disaggregated() to list of dimension of inequality variables

``` r
lapply(variables, svyby_disaggregated)
```

```
## [[1]]
##   urban       sba         se      ci_l      ci_u
## 1 Rural 0.7027926 0.01827014 0.6669838 0.7386014
## 2 Urban 0.9137114 0.01006922 0.8939761 0.9334467
## 
## [[2]]
##               quintile       sba         se      ci_l      ci_u
## 1           Quintile 3 0.8734299 0.01748832 0.8391534 0.9077064
## 2           Quintile 2 0.7439339 0.02677458 0.6914567 0.7964111
## 3 Quintile 1 (poorest) 0.5733626 0.02838101 0.5177368 0.6289884
## 4           Quintile 4 0.9048578 0.01742623 0.8707030 0.9390126
## 5 Quintile 5 (richest) 0.9547576 0.01142862 0.9323579 0.9771573
## 
## [[3]]
##                         educatt       sba         se      ci_l      ci_u
## 1       No or primary education 0.6459142 0.02560354 0.5957322 0.6960962
## 2 Secondary or higher education 0.8703938 0.00937096 0.8520270 0.8887605
## 
## [[4]]
##          mage       sba         se      ci_l      ci_u
## 1 15-19 years 0.6996830 0.06906272 0.5643226 0.8350434
## 2 20-34 years 0.8012016 0.01262522 0.7764566 0.8259466
## 3 35-49 years 0.8265312 0.01707401 0.7930667 0.8599956
```
## Conclusion

In summary, disaggregated data from surveys enables more in-depth analysis and understanding, leading to more informed decisions, targeted interventions, and fairer policies.
