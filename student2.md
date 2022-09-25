student2
================
Kar Ng
2022-09

-   <a href="#1-r-packages" id="toc-1-r-packages">1 R PACKAGES</a>
-   <a href="#2-introduction" id="toc-2-introduction">2 INTRODUCTION</a>
-   <a href="#3-data-prepraration" id="toc-3-data-prepraration">3 DATA
    PREPRARATION</a>
    -   <a href="#31-data-import" id="toc-31-data-import">3.1 Data import</a>
    -   <a href="#32-data-description" id="toc-32-data-description">3.2 Data
        description</a>
    -   <a href="#33-data-exploration" id="toc-33-data-exploration">3.3 Data
        exploration</a>
-   <a href="#4-data-processing" id="toc-4-data-processing">4 DATA
    PROCESSING</a>
    -   <a href="#41-factor-conversion" id="toc-41-factor-conversion">4.1 Factor
        Conversion</a>
        -   <a href="#411-getting-overall-grade"
            id="toc-411-getting-overall-grade">4.1.1 Getting Overall Grade</a>
        -   <a href="#412-normalisation" id="toc-412-normalisation">4.1.2
            Normalisation</a>
-   <a href="#5-visualisation" id="toc-5-visualisation">5 VISUALISATION</a>
-   <a href="#6-conclusion" id="toc-6-conclusion">6 CONCLUSION</a>
-   <a href="#7-reference" id="toc-7-reference">7 REFERENCE</a>

# 1 R PACKAGES

``` r
library(tidyverse)
library(kableExtra)
library(skimr)
```

# 2 INTRODUCTION

This project explores a highly-comprehensive dataset in relation to the
performance of nearly 400 mathematics students. The data were obtained
in secondary school setting.

This dataset contains numerous interesting social, gender and study
information about these students. Students’ grades of mathematics are
relocated in three categories:

-   G1 - first period grade (numeric: from 0 to 20)  
-   G2 - second period grade (numeric: from 0 to 20)  
-   G3 - final grade (numeric: from 0 to 20, output target)

# 3 DATA PREPRARATION

Data set used in this project is a publicly available dataset available
and sourced from Kaggle website, please visit this
[link](https://www.kaggle.com/datasets/uciml/student-alcohol-consumption).

## 3.1 Data import

Following code download the dataset.

``` r
student <- read.csv("student-mat.csv",
                    header = T, 
                    stringsAsFactors = T, 
                    fileEncoding = "UTF-8-BOM")
```

## 3.2 Data description

``` r
Variable <- c("school", 
               "sex",
               "age",
               "address",
               "famsize",
               "Pstatus",
               "Medu",
               "Fedu",
               "Mjob",
               "Fjob",
               "reason",
               "guardian",
               "traveltime",
               "studytime",
               "failures",
               "schoolsup",
               "famsup",
               "paid",
               "activities",
               "nursery",
               "higher",
               "internet",
               "romantic",
               "famrel",
               "freetime",
               "goout",
               "Dalc",
               "Walc",
               "health",
               "absences",
               "G1",
               "G2",
               "G3")
       
Description <- c("student's school (binary: 'GP' - Gabriel Pereira or 'MS' - Mousinho da Silveira)",
                 "student's sex (binary: 'F' - female or 'M' - male)",
                 "student's age (numeric: from 15 to 22)",
                 "student's home address type (binary: 'U' - urban or 'R' - rural)",
                 "family size (binary: 'LE3' - less or equal to 3 or 'GT3' - greater than 3)",
                 "parent's cohabitation status (binary: 'T' - living together or 'A' - apart)",
                 "mother's education (numeric: 0 - none, 1 - primary education (4th grade), 2 – 5th to 9th grade, 3 – secondary education or 4 – higher education)",
                 "father's education (numeric: 0 - none, 1 - primary education (4th grade), 2 – 5th to 9th grade, 3 – secondary education or 4 – higher education)",
                 "mother's job (nominal: 'teacher', 'health' care related, civil 'services' (e.g. administrative or police), 'at_home' or 'other')",
                 " father's job (nominal: 'teacher', 'health' care related, civil 'services' (e.g. administrative or police), 'at_home' or 'other')",
                 "reason to choose this school (nominal: close to 'home', school 'reputation', 'course' preference or 'other')",
                 "student's guardian (nominal: 'mother', 'father' or 'other')",
                 "home to school travel time (numeric: 1 - <15 min., 2 - 15 to 30 min., 3 - 30 min. to 1 hour, or 4 - >1 hour)",
                 "weekly study time (numeric: 1 - <2 hours, 2 - 2 to 5 hours, 3 - 5 to 10 hours, or 4 - >10 hours)",
                 "number of past class failures (numeric: n if 1<=n<3, else 4)",
                 "extra educational support (binary: yes or no)",
                 "family educational support (binary: yes or no)",
                 "extra paid classes within the course subject (Math or Portuguese) (binary: yes or no)",
                 "extra-curricular activities (binary: yes or no)",
                 "attended nursery school (binary: yes or no)",
                 "wants to take higher education (binary: yes or no)",
                 "Internet access at home (binary: yes or no)",
                 "with a romantic relationship (binary: yes or no)",
                 "quality of family relationships (numeric: from 1 - very bad to 5 - excellent)",
                 "free time after school (numeric: from 1 - very low to 5 - very high)",
                 "going out with friends (numeric: from 1 - very low to 5 - very high)",
                 "workday alcohol consumption (numeric: from 1 - very low to 5 - very high)",
                 "weekend alcohol consumption (numeric: from 1 - very low to 5 - very high)",
                 "current health status (numeric: from 1 - very bad to 5 - very good)",
                 "number of school absences (numeric: from 0 to 93)",
                 "first period grade (numeric: from 0 to 20)",
                 "second period grade (numeric: from 0 to 20)",
                 "final grade (numeric: from 0 to 20, output target)"
                 )


data.frame(Variable, Description) %>% 
  kbl() %>% 
  kable_styling(bootstrap_options = c("hover", "stripped", "bordered"))
```

<table class="table table-hover table-bordered" style="margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">

Variable

</th>
<th style="text-align:left;">

Description

</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">

school

</td>
<td style="text-align:left;">

student’s school (binary: ‘GP’ - Gabriel Pereira or ‘MS’ - Mousinho da
Silveira)

</td>
</tr>
<tr>
<td style="text-align:left;">

sex

</td>
<td style="text-align:left;">

student’s sex (binary: ‘F’ - female or ‘M’ - male)

</td>
</tr>
<tr>
<td style="text-align:left;">

age

</td>
<td style="text-align:left;">

student’s age (numeric: from 15 to 22)

</td>
</tr>
<tr>
<td style="text-align:left;">

address

</td>
<td style="text-align:left;">

student’s home address type (binary: ‘U’ - urban or ‘R’ - rural)

</td>
</tr>
<tr>
<td style="text-align:left;">

famsize

</td>
<td style="text-align:left;">

family size (binary: ‘LE3’ - less or equal to 3 or ‘GT3’ - greater than
3)

</td>
</tr>
<tr>
<td style="text-align:left;">

Pstatus

</td>
<td style="text-align:left;">

parent’s cohabitation status (binary: ‘T’ - living together or ‘A’ -
apart)

</td>
</tr>
<tr>
<td style="text-align:left;">

Medu

</td>
<td style="text-align:left;">

mother’s education (numeric: 0 - none, 1 - primary education (4th
grade), 2 – 5th to 9th grade, 3 – secondary education or 4 – higher
education)

</td>
</tr>
<tr>
<td style="text-align:left;">

Fedu

</td>
<td style="text-align:left;">

father’s education (numeric: 0 - none, 1 - primary education (4th
grade), 2 – 5th to 9th grade, 3 – secondary education or 4 – higher
education)

</td>
</tr>
<tr>
<td style="text-align:left;">

Mjob

</td>
<td style="text-align:left;">

mother’s job (nominal: ‘teacher’, ‘health’ care related, civil
‘services’ (e.g. administrative or police), ‘at_home’ or ‘other’)

</td>
</tr>
<tr>
<td style="text-align:left;">

Fjob

</td>
<td style="text-align:left;">

father’s job (nominal: ‘teacher’, ‘health’ care related, civil
‘services’ (e.g. administrative or police), ‘at_home’ or ‘other’)

</td>
</tr>
<tr>
<td style="text-align:left;">

reason

</td>
<td style="text-align:left;">

reason to choose this school (nominal: close to ‘home’, school
‘reputation’, ‘course’ preference or ‘other’)

</td>
</tr>
<tr>
<td style="text-align:left;">

guardian

</td>
<td style="text-align:left;">

student’s guardian (nominal: ‘mother’, ‘father’ or ‘other’)

</td>
</tr>
<tr>
<td style="text-align:left;">

traveltime

</td>
<td style="text-align:left;">

home to school travel time (numeric: 1 - \<15 min., 2 - 15 to 30 min.,
3 - 30 min. to 1 hour, or 4 - \>1 hour)

</td>
</tr>
<tr>
<td style="text-align:left;">

studytime

</td>
<td style="text-align:left;">

weekly study time (numeric: 1 - \<2 hours, 2 - 2 to 5 hours, 3 - 5 to 10
hours, or 4 - \>10 hours)

</td>
</tr>
<tr>
<td style="text-align:left;">

failures

</td>
<td style="text-align:left;">

number of past class failures (numeric: n if 1\<=n\<3, else 4)

</td>
</tr>
<tr>
<td style="text-align:left;">

schoolsup

</td>
<td style="text-align:left;">

extra educational support (binary: yes or no)

</td>
</tr>
<tr>
<td style="text-align:left;">

famsup

</td>
<td style="text-align:left;">

family educational support (binary: yes or no)

</td>
</tr>
<tr>
<td style="text-align:left;">

paid

</td>
<td style="text-align:left;">

extra paid classes within the course subject (Math or Portuguese)
(binary: yes or no)

</td>
</tr>
<tr>
<td style="text-align:left;">

activities

</td>
<td style="text-align:left;">

extra-curricular activities (binary: yes or no)

</td>
</tr>
<tr>
<td style="text-align:left;">

nursery

</td>
<td style="text-align:left;">

attended nursery school (binary: yes or no)

</td>
</tr>
<tr>
<td style="text-align:left;">

higher

</td>
<td style="text-align:left;">

wants to take higher education (binary: yes or no)

</td>
</tr>
<tr>
<td style="text-align:left;">

internet

</td>
<td style="text-align:left;">

Internet access at home (binary: yes or no)

</td>
</tr>
<tr>
<td style="text-align:left;">

romantic

</td>
<td style="text-align:left;">

with a romantic relationship (binary: yes or no)

</td>
</tr>
<tr>
<td style="text-align:left;">

famrel

</td>
<td style="text-align:left;">

quality of family relationships (numeric: from 1 - very bad to 5 -
excellent)

</td>
</tr>
<tr>
<td style="text-align:left;">

freetime

</td>
<td style="text-align:left;">

free time after school (numeric: from 1 - very low to 5 - very high)

</td>
</tr>
<tr>
<td style="text-align:left;">

goout

</td>
<td style="text-align:left;">

going out with friends (numeric: from 1 - very low to 5 - very high)

</td>
</tr>
<tr>
<td style="text-align:left;">

Dalc

</td>
<td style="text-align:left;">

workday alcohol consumption (numeric: from 1 - very low to 5 - very
high)

</td>
</tr>
<tr>
<td style="text-align:left;">

Walc

</td>
<td style="text-align:left;">

weekend alcohol consumption (numeric: from 1 - very low to 5 - very
high)

</td>
</tr>
<tr>
<td style="text-align:left;">

health

</td>
<td style="text-align:left;">

current health status (numeric: from 1 - very bad to 5 - very good)

</td>
</tr>
<tr>
<td style="text-align:left;">

absences

</td>
<td style="text-align:left;">

number of school absences (numeric: from 0 to 93)

</td>
</tr>
<tr>
<td style="text-align:left;">

G1

</td>
<td style="text-align:left;">

first period grade (numeric: from 0 to 20)

</td>
</tr>
<tr>
<td style="text-align:left;">

G2

</td>
<td style="text-align:left;">

second period grade (numeric: from 0 to 20)

</td>
</tr>
<tr>
<td style="text-align:left;">

G3

</td>
<td style="text-align:left;">

final grade (numeric: from 0 to 20, output target)

</td>
</tr>
</tbody>
</table>

## 3.3 Data exploration

This dataset has 395 rows of observation (number of students) and 33
columns of variables.

``` r
dim(student)
```

    ## [1] 395  33

Randomly select 10 rows of observations from the dataset.

``` r
sample_n(student, 10) %>% 
  kbl() %>% 
  kable_styling(bootstrap_options = c("hover", "stripped", "bordered"))
```

<table class="table table-hover table-bordered" style="margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">

school

</th>
<th style="text-align:left;">

sex

</th>
<th style="text-align:right;">

age

</th>
<th style="text-align:left;">

address

</th>
<th style="text-align:left;">

famsize

</th>
<th style="text-align:left;">

Pstatus

</th>
<th style="text-align:right;">

Medu

</th>
<th style="text-align:right;">

Fedu

</th>
<th style="text-align:left;">

Mjob

</th>
<th style="text-align:left;">

Fjob

</th>
<th style="text-align:left;">

reason

</th>
<th style="text-align:left;">

guardian

</th>
<th style="text-align:right;">

traveltime

</th>
<th style="text-align:right;">

studytime

</th>
<th style="text-align:right;">

failures

</th>
<th style="text-align:left;">

schoolsup

</th>
<th style="text-align:left;">

famsup

</th>
<th style="text-align:left;">

paid

</th>
<th style="text-align:left;">

activities

</th>
<th style="text-align:left;">

nursery

</th>
<th style="text-align:left;">

higher

</th>
<th style="text-align:left;">

internet

</th>
<th style="text-align:left;">

romantic

</th>
<th style="text-align:right;">

famrel

</th>
<th style="text-align:right;">

freetime

</th>
<th style="text-align:right;">

goout

</th>
<th style="text-align:right;">

Dalc

</th>
<th style="text-align:right;">

Walc

</th>
<th style="text-align:right;">

health

</th>
<th style="text-align:right;">

absences

</th>
<th style="text-align:right;">

G1

</th>
<th style="text-align:right;">

G2

</th>
<th style="text-align:right;">

G3

</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">

GP

</td>
<td style="text-align:left;">

F

</td>
<td style="text-align:right;">

16

</td>
<td style="text-align:left;">

U

</td>
<td style="text-align:left;">

GT3

</td>
<td style="text-align:left;">

T

</td>
<td style="text-align:right;">

2

</td>
<td style="text-align:right;">

3

</td>
<td style="text-align:left;">

other

</td>
<td style="text-align:left;">

other

</td>
<td style="text-align:left;">

reputation

</td>
<td style="text-align:left;">

mother

</td>
<td style="text-align:right;">

1

</td>
<td style="text-align:right;">

2

</td>
<td style="text-align:right;">

0

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

no

</td>
<td style="text-align:left;">

no

</td>
<td style="text-align:right;">

4

</td>
<td style="text-align:right;">

4

</td>
<td style="text-align:right;">

3

</td>
<td style="text-align:right;">

1

</td>
<td style="text-align:right;">

3

</td>
<td style="text-align:right;">

4

</td>
<td style="text-align:right;">

6

</td>
<td style="text-align:right;">

8

</td>
<td style="text-align:right;">

10

</td>
<td style="text-align:right;">

10

</td>
</tr>
<tr>
<td style="text-align:left;">

GP

</td>
<td style="text-align:left;">

M

</td>
<td style="text-align:right;">

16

</td>
<td style="text-align:left;">

U

</td>
<td style="text-align:left;">

LE3

</td>
<td style="text-align:left;">

A

</td>
<td style="text-align:right;">

3

</td>
<td style="text-align:right;">

4

</td>
<td style="text-align:left;">

services

</td>
<td style="text-align:left;">

other

</td>
<td style="text-align:left;">

home

</td>
<td style="text-align:left;">

mother

</td>
<td style="text-align:right;">

1

</td>
<td style="text-align:right;">

2

</td>
<td style="text-align:right;">

0

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

no

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

no

</td>
<td style="text-align:right;">

5

</td>
<td style="text-align:right;">

3

</td>
<td style="text-align:right;">

3

</td>
<td style="text-align:right;">

1

</td>
<td style="text-align:right;">

1

</td>
<td style="text-align:right;">

5

</td>
<td style="text-align:right;">

4

</td>
<td style="text-align:right;">

11

</td>
<td style="text-align:right;">

11

</td>
<td style="text-align:right;">

11

</td>
</tr>
<tr>
<td style="text-align:left;">

GP

</td>
<td style="text-align:left;">

F

</td>
<td style="text-align:right;">

16

</td>
<td style="text-align:left;">

U

</td>
<td style="text-align:left;">

GT3

</td>
<td style="text-align:left;">

T

</td>
<td style="text-align:right;">

2

</td>
<td style="text-align:right;">

2

</td>
<td style="text-align:left;">

other

</td>
<td style="text-align:left;">

other

</td>
<td style="text-align:left;">

home

</td>
<td style="text-align:left;">

mother

</td>
<td style="text-align:right;">

1

</td>
<td style="text-align:right;">

2

</td>
<td style="text-align:right;">

0

</td>
<td style="text-align:left;">

no

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

no

</td>
<td style="text-align:left;">

no

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

no

</td>
<td style="text-align:right;">

5

</td>
<td style="text-align:right;">

1

</td>
<td style="text-align:right;">

5

</td>
<td style="text-align:right;">

1

</td>
<td style="text-align:right;">

1

</td>
<td style="text-align:right;">

4

</td>
<td style="text-align:right;">

0

</td>
<td style="text-align:right;">

6

</td>
<td style="text-align:right;">

7

</td>
<td style="text-align:right;">

0

</td>
</tr>
<tr>
<td style="text-align:left;">

GP

</td>
<td style="text-align:left;">

M

</td>
<td style="text-align:right;">

16

</td>
<td style="text-align:left;">

U

</td>
<td style="text-align:left;">

LE3

</td>
<td style="text-align:left;">

T

</td>
<td style="text-align:right;">

1

</td>
<td style="text-align:right;">

1

</td>
<td style="text-align:left;">

services

</td>
<td style="text-align:left;">

other

</td>
<td style="text-align:left;">

course

</td>
<td style="text-align:left;">

mother

</td>
<td style="text-align:right;">

1

</td>
<td style="text-align:right;">

2

</td>
<td style="text-align:right;">

1

</td>
<td style="text-align:left;">

no

</td>
<td style="text-align:left;">

no

</td>
<td style="text-align:left;">

no

</td>
<td style="text-align:left;">

no

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

no

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:right;">

4

</td>
<td style="text-align:right;">

4

</td>
<td style="text-align:right;">

4

</td>
<td style="text-align:right;">

1

</td>
<td style="text-align:right;">

3

</td>
<td style="text-align:right;">

5

</td>
<td style="text-align:right;">

0

</td>
<td style="text-align:right;">

14

</td>
<td style="text-align:right;">

12

</td>
<td style="text-align:right;">

12

</td>
</tr>
<tr>
<td style="text-align:left;">

GP

</td>
<td style="text-align:left;">

M

</td>
<td style="text-align:right;">

15

</td>
<td style="text-align:left;">

U

</td>
<td style="text-align:left;">

GT3

</td>
<td style="text-align:left;">

T

</td>
<td style="text-align:right;">

3

</td>
<td style="text-align:right;">

4

</td>
<td style="text-align:left;">

other

</td>
<td style="text-align:left;">

other

</td>
<td style="text-align:left;">

reputation

</td>
<td style="text-align:left;">

father

</td>
<td style="text-align:right;">

1

</td>
<td style="text-align:right;">

1

</td>
<td style="text-align:right;">

0

</td>
<td style="text-align:left;">

no

</td>
<td style="text-align:left;">

no

</td>
<td style="text-align:left;">

no

</td>
<td style="text-align:left;">

no

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

no

</td>
<td style="text-align:right;">

3

</td>
<td style="text-align:right;">

4

</td>
<td style="text-align:right;">

3

</td>
<td style="text-align:right;">

1

</td>
<td style="text-align:right;">

2

</td>
<td style="text-align:right;">

4

</td>
<td style="text-align:right;">

6

</td>
<td style="text-align:right;">

14

</td>
<td style="text-align:right;">

13

</td>
<td style="text-align:right;">

13

</td>
</tr>
<tr>
<td style="text-align:left;">

GP

</td>
<td style="text-align:left;">

F

</td>
<td style="text-align:right;">

17

</td>
<td style="text-align:left;">

U

</td>
<td style="text-align:left;">

LE3

</td>
<td style="text-align:left;">

T

</td>
<td style="text-align:right;">

2

</td>
<td style="text-align:right;">

2

</td>
<td style="text-align:left;">

services

</td>
<td style="text-align:left;">

services

</td>
<td style="text-align:left;">

course

</td>
<td style="text-align:left;">

father

</td>
<td style="text-align:right;">

1

</td>
<td style="text-align:right;">

4

</td>
<td style="text-align:right;">

0

</td>
<td style="text-align:left;">

no

</td>
<td style="text-align:left;">

no

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:right;">

3

</td>
<td style="text-align:right;">

4

</td>
<td style="text-align:right;">

1

</td>
<td style="text-align:right;">

1

</td>
<td style="text-align:right;">

1

</td>
<td style="text-align:right;">

2

</td>
<td style="text-align:right;">

0

</td>
<td style="text-align:right;">

10

</td>
<td style="text-align:right;">

9

</td>
<td style="text-align:right;">

0

</td>
</tr>
<tr>
<td style="text-align:left;">

GP

</td>
<td style="text-align:left;">

F

</td>
<td style="text-align:right;">

16

</td>
<td style="text-align:left;">

R

</td>
<td style="text-align:left;">

GT3

</td>
<td style="text-align:left;">

T

</td>
<td style="text-align:right;">

4

</td>
<td style="text-align:right;">

4

</td>
<td style="text-align:left;">

health

</td>
<td style="text-align:left;">

teacher

</td>
<td style="text-align:left;">

other

</td>
<td style="text-align:left;">

mother

</td>
<td style="text-align:right;">

1

</td>
<td style="text-align:right;">

2

</td>
<td style="text-align:right;">

0

</td>
<td style="text-align:left;">

no

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

no

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

no

</td>
<td style="text-align:left;">

no

</td>
<td style="text-align:right;">

2

</td>
<td style="text-align:right;">

4

</td>
<td style="text-align:right;">

4

</td>
<td style="text-align:right;">

2

</td>
<td style="text-align:right;">

3

</td>
<td style="text-align:right;">

4

</td>
<td style="text-align:right;">

6

</td>
<td style="text-align:right;">

10

</td>
<td style="text-align:right;">

11

</td>
<td style="text-align:right;">

11

</td>
</tr>
<tr>
<td style="text-align:left;">

MS

</td>
<td style="text-align:left;">

F

</td>
<td style="text-align:right;">

17

</td>
<td style="text-align:left;">

R

</td>
<td style="text-align:left;">

GT3

</td>
<td style="text-align:left;">

T

</td>
<td style="text-align:right;">

1

</td>
<td style="text-align:right;">

2

</td>
<td style="text-align:left;">

other

</td>
<td style="text-align:left;">

other

</td>
<td style="text-align:left;">

course

</td>
<td style="text-align:left;">

mother

</td>
<td style="text-align:right;">

1

</td>
<td style="text-align:right;">

1

</td>
<td style="text-align:right;">

0

</td>
<td style="text-align:left;">

no

</td>
<td style="text-align:left;">

no

</td>
<td style="text-align:left;">

no

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

no

</td>
<td style="text-align:right;">

3

</td>
<td style="text-align:right;">

5

</td>
<td style="text-align:right;">

5

</td>
<td style="text-align:right;">

1

</td>
<td style="text-align:right;">

3

</td>
<td style="text-align:right;">

1

</td>
<td style="text-align:right;">

14

</td>
<td style="text-align:right;">

6

</td>
<td style="text-align:right;">

5

</td>
<td style="text-align:right;">

5

</td>
</tr>
<tr>
<td style="text-align:left;">

GP

</td>
<td style="text-align:left;">

F

</td>
<td style="text-align:right;">

16

</td>
<td style="text-align:left;">

U

</td>
<td style="text-align:left;">

GT3

</td>
<td style="text-align:left;">

T

</td>
<td style="text-align:right;">

4

</td>
<td style="text-align:right;">

3

</td>
<td style="text-align:left;">

teacher

</td>
<td style="text-align:left;">

health

</td>
<td style="text-align:left;">

home

</td>
<td style="text-align:left;">

mother

</td>
<td style="text-align:right;">

1

</td>
<td style="text-align:right;">

3

</td>
<td style="text-align:right;">

0

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

no

</td>
<td style="text-align:right;">

3

</td>
<td style="text-align:right;">

4

</td>
<td style="text-align:right;">

4

</td>
<td style="text-align:right;">

2

</td>
<td style="text-align:right;">

4

</td>
<td style="text-align:right;">

4

</td>
<td style="text-align:right;">

2

</td>
<td style="text-align:right;">

10

</td>
<td style="text-align:right;">

9

</td>
<td style="text-align:right;">

9

</td>
</tr>
<tr>
<td style="text-align:left;">

GP

</td>
<td style="text-align:left;">

M

</td>
<td style="text-align:right;">

15

</td>
<td style="text-align:left;">

R

</td>
<td style="text-align:left;">

GT3

</td>
<td style="text-align:left;">

T

</td>
<td style="text-align:right;">

3

</td>
<td style="text-align:right;">

4

</td>
<td style="text-align:left;">

at_home

</td>
<td style="text-align:left;">

teacher

</td>
<td style="text-align:left;">

course

</td>
<td style="text-align:left;">

mother

</td>
<td style="text-align:right;">

4

</td>
<td style="text-align:right;">

2

</td>
<td style="text-align:right;">

0

</td>
<td style="text-align:left;">

no

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

no

</td>
<td style="text-align:left;">

no

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:left;">

no

</td>
<td style="text-align:left;">

yes

</td>
<td style="text-align:right;">

5

</td>
<td style="text-align:right;">

3

</td>
<td style="text-align:right;">

3

</td>
<td style="text-align:right;">

1

</td>
<td style="text-align:right;">

1

</td>
<td style="text-align:right;">

5

</td>
<td style="text-align:right;">

0

</td>
<td style="text-align:right;">

9

</td>
<td style="text-align:right;">

0

</td>
<td style="text-align:right;">

0

</td>
</tr>
</tbody>
</table>

The data set seems quite complete. Let’s check NA.

**Vertical NA scanning**

``` r
colSums(is.na(student))
```

    ##     school        sex        age    address    famsize    Pstatus       Medu 
    ##          0          0          0          0          0          0          0 
    ##       Fedu       Mjob       Fjob     reason   guardian traveltime  studytime 
    ##          0          0          0          0          0          0          0 
    ##   failures  schoolsup     famsup       paid activities    nursery     higher 
    ##          0          0          0          0          0          0          0 
    ##   internet   romantic     famrel   freetime      goout       Dalc       Walc 
    ##          0          0          0          0          0          0          0 
    ##     health   absences         G1         G2         G3 
    ##          0          0          0          0          0

There is no missing values in each columns.

**Horizontal NA scanning:**

Also, fore sure, there is no missing values is doing a horizontal NA
scanning.

``` r
student %>% 
  gather(key = "variables", value = "values") %>% 
  filter(is.na(values))
```

    ## Warning: attributes are not identical across measure variables;
    ## they will be dropped

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["variables"],"name":[1],"type":["chr"],"align":["left"]},{"label":["values"],"name":[2],"type":["chr"],"align":["left"]}],"data":[],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

Following shows variable types that are allocated to each variables by
R, such as “Factor” and “int”.

``` r
str(student)
```

    ## 'data.frame':    395 obs. of  33 variables:
    ##  $ school    : Factor w/ 2 levels "GP","MS": 1 1 1 1 1 1 1 1 1 1 ...
    ##  $ sex       : Factor w/ 2 levels "F","M": 1 1 1 1 1 2 2 1 2 2 ...
    ##  $ age       : int  18 17 15 15 16 16 16 17 15 15 ...
    ##  $ address   : Factor w/ 2 levels "R","U": 2 2 2 2 2 2 2 2 2 2 ...
    ##  $ famsize   : Factor w/ 2 levels "GT3","LE3": 1 1 2 1 1 2 2 1 2 1 ...
    ##  $ Pstatus   : Factor w/ 2 levels "A","T": 1 2 2 2 2 2 2 1 1 2 ...
    ##  $ Medu      : int  4 1 1 4 3 4 2 4 3 3 ...
    ##  $ Fedu      : int  4 1 1 2 3 3 2 4 2 4 ...
    ##  $ Mjob      : Factor w/ 5 levels "at_home","health",..: 1 1 1 2 3 4 3 3 4 3 ...
    ##  $ Fjob      : Factor w/ 5 levels "at_home","health",..: 5 3 3 4 3 3 3 5 3 3 ...
    ##  $ reason    : Factor w/ 4 levels "course","home",..: 1 1 3 2 2 4 2 2 2 2 ...
    ##  $ guardian  : Factor w/ 3 levels "father","mother",..: 2 1 2 2 1 2 2 2 2 2 ...
    ##  $ traveltime: int  2 1 1 1 1 1 1 2 1 1 ...
    ##  $ studytime : int  2 2 2 3 2 2 2 2 2 2 ...
    ##  $ failures  : int  0 0 3 0 0 0 0 0 0 0 ...
    ##  $ schoolsup : Factor w/ 2 levels "no","yes": 2 1 2 1 1 1 1 2 1 1 ...
    ##  $ famsup    : Factor w/ 2 levels "no","yes": 1 2 1 2 2 2 1 2 2 2 ...
    ##  $ paid      : Factor w/ 2 levels "no","yes": 1 1 2 2 2 2 1 1 2 2 ...
    ##  $ activities: Factor w/ 2 levels "no","yes": 1 1 1 2 1 2 1 1 1 2 ...
    ##  $ nursery   : Factor w/ 2 levels "no","yes": 2 1 2 2 2 2 2 2 2 2 ...
    ##  $ higher    : Factor w/ 2 levels "no","yes": 2 2 2 2 2 2 2 2 2 2 ...
    ##  $ internet  : Factor w/ 2 levels "no","yes": 1 2 2 2 1 2 2 1 2 2 ...
    ##  $ romantic  : Factor w/ 2 levels "no","yes": 1 1 1 2 1 1 1 1 1 1 ...
    ##  $ famrel    : int  4 5 4 3 4 5 4 4 4 5 ...
    ##  $ freetime  : int  3 3 3 2 3 4 4 1 2 5 ...
    ##  $ goout     : int  4 3 2 2 2 2 4 4 2 1 ...
    ##  $ Dalc      : int  1 1 2 1 1 1 1 1 1 1 ...
    ##  $ Walc      : int  1 1 3 1 2 2 1 1 1 1 ...
    ##  $ health    : int  3 3 3 5 5 5 3 1 1 5 ...
    ##  $ absences  : int  6 4 10 2 4 10 0 6 0 0 ...
    ##  $ G1        : int  5 5 7 15 6 15 12 6 16 14 ...
    ##  $ G2        : int  6 5 8 14 10 15 12 5 18 15 ...
    ##  $ G3        : int  6 6 10 15 10 15 11 6 19 15 ...

There are numerous numerical variables need to be converted into factor
variable type because of their categorical nature. This conversion is an
important for specific visualisation. These factors are Medu, Fedu,
traveltime, studytime, failures, famrel, freetime, goout, Dalc, Walc,
health, and absences. This conversion will be done in next data
processing section.

# 4 DATA PROCESSING

## 4.1 Factor Conversion

Following code convert numerical variables that has categorical nature
into factor type.

``` r
s2 <- student %>% 
  mutate(Medu = as.factor(Medu),
         Fedu = as.factor(Fedu),
         traveltime = as.factor(traveltime),
         studytime  = as.factor(studytime),
         failures = as.factor(failures ),
         famrel = as.factor(famrel),
         freetime = as.factor(freetime),
         goout = as.factor(goout),
         Dalc = as.factor(Dalc),
         Walc = as.factor(Walc),
         health = as.factor(health),
         absences = as.factor(absences))
```

Let’s check the conversion:

``` r
glimpse(s2)
```

    ## Rows: 395
    ## Columns: 33
    ## $ school     <fct> GP, GP, GP, GP, GP, GP, GP, GP, GP, GP, GP, GP, GP, GP, GP,…
    ## $ sex        <fct> F, F, F, F, F, M, M, F, M, M, F, F, M, M, M, F, F, F, M, M,…
    ## $ age        <int> 18, 17, 15, 15, 16, 16, 16, 17, 15, 15, 15, 15, 15, 15, 15,…
    ## $ address    <fct> U, U, U, U, U, U, U, U, U, U, U, U, U, U, U, U, U, U, U, U,…
    ## $ famsize    <fct> GT3, GT3, LE3, GT3, GT3, LE3, LE3, GT3, LE3, GT3, GT3, GT3,…
    ## $ Pstatus    <fct> A, T, T, T, T, T, T, A, A, T, T, T, T, T, A, T, T, T, T, T,…
    ## $ Medu       <fct> 4, 1, 1, 4, 3, 4, 2, 4, 3, 3, 4, 2, 4, 4, 2, 4, 4, 3, 3, 4,…
    ## $ Fedu       <fct> 4, 1, 1, 2, 3, 3, 2, 4, 2, 4, 4, 1, 4, 3, 2, 4, 4, 3, 2, 3,…
    ## $ Mjob       <fct> at_home, at_home, at_home, health, other, services, other, …
    ## $ Fjob       <fct> teacher, other, other, services, other, other, other, teach…
    ## $ reason     <fct> course, course, other, home, home, reputation, home, home, …
    ## $ guardian   <fct> mother, father, mother, mother, father, mother, mother, mot…
    ## $ traveltime <fct> 2, 1, 1, 1, 1, 1, 1, 2, 1, 1, 1, 3, 1, 2, 1, 1, 1, 3, 1, 1,…
    ## $ studytime  <fct> 2, 2, 2, 3, 2, 2, 2, 2, 2, 2, 2, 3, 1, 2, 3, 1, 3, 2, 1, 1,…
    ## $ failures   <fct> 0, 0, 3, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 3, 0,…
    ## $ schoolsup  <fct> yes, no, yes, no, no, no, no, yes, no, no, no, no, no, no, …
    ## $ famsup     <fct> no, yes, no, yes, yes, yes, no, yes, yes, yes, yes, yes, ye…
    ## $ paid       <fct> no, no, yes, yes, yes, yes, no, no, yes, yes, yes, no, yes,…
    ## $ activities <fct> no, no, no, yes, no, yes, no, no, no, yes, no, yes, yes, no…
    ## $ nursery    <fct> yes, no, yes, yes, yes, yes, yes, yes, yes, yes, yes, yes, …
    ## $ higher     <fct> yes, yes, yes, yes, yes, yes, yes, yes, yes, yes, yes, yes,…
    ## $ internet   <fct> no, yes, yes, yes, no, yes, yes, no, yes, yes, yes, yes, ye…
    ## $ romantic   <fct> no, no, no, yes, no, no, no, no, no, no, no, no, no, no, ye…
    ## $ famrel     <fct> 4, 5, 4, 3, 4, 5, 4, 4, 4, 5, 3, 5, 4, 5, 4, 4, 3, 5, 5, 3,…
    ## $ freetime   <fct> 3, 3, 3, 2, 3, 4, 4, 1, 2, 5, 3, 2, 3, 4, 5, 4, 2, 3, 5, 1,…
    ## $ goout      <fct> 4, 3, 2, 2, 2, 2, 4, 4, 2, 1, 3, 2, 3, 3, 2, 4, 3, 2, 5, 3,…
    ## $ Dalc       <fct> 1, 1, 2, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 2, 1,…
    ## $ Walc       <fct> 1, 1, 3, 1, 2, 2, 1, 1, 1, 1, 2, 1, 3, 2, 1, 2, 2, 1, 4, 3,…
    ## $ health     <fct> 3, 3, 3, 5, 5, 5, 3, 1, 1, 5, 2, 4, 5, 3, 3, 2, 2, 4, 5, 5,…
    ## $ absences   <fct> 6, 4, 10, 2, 4, 10, 0, 6, 0, 0, 0, 4, 2, 2, 0, 4, 6, 4, 16,…
    ## $ G1         <int> 5, 5, 7, 15, 6, 15, 12, 6, 16, 14, 10, 10, 14, 10, 14, 14, …
    ## $ G2         <int> 6, 5, 8, 14, 10, 15, 12, 5, 18, 15, 8, 12, 14, 10, 16, 14, …
    ## $ G3         <int> 6, 6, 10, 15, 10, 15, 11, 6, 19, 15, 9, 12, 14, 11, 16, 14,…

Therefore, current numerical variables are age and the three
grades-related variables.

``` r
s2 %>% select(is.numeric) %>% glimpse()
```

    ## Warning: Predicate functions must be wrapped in `where()`.
    ## 
    ##   # Bad
    ##   data %>% select(is.numeric)
    ## 
    ##   # Good
    ##   data %>% select(where(is.numeric))
    ## 
    ## ℹ Please update your code.
    ## This message is displayed once per session.

    ## Rows: 395
    ## Columns: 4
    ## $ age <int> 18, 17, 15, 15, 16, 16, 16, 17, 15, 15, 15, 15, 15, 15, 15, 16, 16…
    ## $ G1  <int> 5, 5, 7, 15, 6, 15, 12, 6, 16, 14, 10, 10, 14, 10, 14, 14, 13, 8, …
    ## $ G2  <int> 6, 5, 8, 14, 10, 15, 12, 5, 18, 15, 8, 12, 14, 10, 16, 14, 14, 10,…
    ## $ G3  <int> 6, 6, 10, 15, 10, 15, 11, 6, 19, 15, 9, 12, 14, 11, 16, 14, 14, 10…

### 4.1.1 Getting Overall Grade

This section creates an overall grade - “G”, by using the average of G1,
G2, and G3. This new variable can help me to analyse what is the overall
performance of a single student.

``` r
s2 <- s2 %>% 
  mutate(G = round((G1 + G2 + G3)/3, 1))
```

Exaiming the column:

``` r
head(s2$G, 10)
```

    ##  [1]  5.7  5.3  8.3 14.7  8.7 15.0 11.7  5.7 17.7 14.7

### 4.1.2 Normalisation

This step is optional but I would like to perform.

The range of grade variables G1, G2, G3, and G are between 0 and 20. I
found that it is a bit counter-intuitive because I am not studying under
the education system that these students had.

Therefore, I would love a range of between 0 and 10 for these variables.

Following code will perform the task.

``` r
# Create function

Normalise <- function(x){
  res = (x - min(x))/(max(x) - min(x))
  return(res)
}

# scaling the G1, G2, G3, and G

S2 <- s2 %>% 
  mutate(G1 = round(Normalise(G1)*10,1),
         G2 = round(Normalise(G2)*10,1),
         G3 = round(Normalise(G3)*10,1),
         G = round(Normalise(G)*10,1))
```

Checking the conversion result:

``` r
S2 %>% select(G1, G2, G3, G) %>% summary()
```

    ##        G1               G2               G3               G        
    ##  Min.   : 0.000   Min.   : 0.000   Min.   : 0.000   Min.   : 0.00  
    ##  1st Qu.: 3.100   1st Qu.: 4.700   1st Qu.: 4.000   1st Qu.: 3.90  
    ##  Median : 5.000   Median : 5.800   Median : 5.500   Median : 5.20  
    ##  Mean   : 4.944   Mean   : 5.636   Mean   : 5.208   Mean   : 5.21  
    ##  3rd Qu.: 6.200   3rd Qu.: 6.800   3rd Qu.: 7.000   3rd Qu.: 6.70  
    ##  Max.   :10.000   Max.   :10.000   Max.   :10.000   Max.   :10.00

# 5 VISUALISATION

# 6 CONCLUSION

# 7 REFERENCE

UCI Machine Learning 2017, *Student Alcohol Consumption*, viewed 25
September 2022,
<https://www.kaggle.com/datasets/uciml/student-alcohol-consumption>
