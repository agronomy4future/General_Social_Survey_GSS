<!-- README.md is generated from README.Rmd. Please edit that file -->
From the website https://gssdataexplorer.norc.org/gss_data, I downloaded the 2025 Data Files (GSS years 1972–2024) and summarized the variables according to my preferences.
The PoliticsJob dataset contains the following columns: year, age, sex, polviews, partyid, and indus10.

``` r
if(!require(readr)) install.packages("readr")
library(readr)

github="https://raw.githubusercontent.com/agronomy4future/General-Social-Survey-GSS-/refs/heads/main/General_Social_Survey_GSS_Sumamry1.csv"
PoliticsJob=data.frame(read_csv(url(github),show_col_types = FALSE))
set.seed(100)

print(df[sample(nrow(PoliticsJob),5),])
        id year age sex polviews partyid indus10
16607 1138 1986  35   1       NA       4    9080
15068 1133 1985  18   1        2       4    8680
13855 1393 1984  59   2        5       5    9290
44329  936 2006  45   2        1       2    4970
29191 2920 1994  45   2       NA      NA      NA
.
.
.
```

## Adding labels 

``` r
if(!require(dplyr)) install.packages("dplyr")
library(dplyr)

PoliticsJob= PoliticsJob %>%
  mutate(
    sex_lbl = case_when(
      sex == 1 ~ "Male",
      sex == 2 ~ "Female",
      TRUE ~ NA_character_
    ),
    
    polviews_lbl = case_when(
      polviews == 1 ~ "Extremely liberal",
      polviews == 2 ~ "Liberal",
      polviews == 3 ~ "Slightly liberal",
      polviews == 4 ~ "Moderate",
      polviews == 5 ~ "Slightly conservative",
      polviews == 6 ~ "Conservative",
      polviews == 7 ~ "Extremely conservative",
      TRUE ~ NA_character_
    ),
    
    partyid_lbl = case_when(
      partyid == 0 ~ "Strong Democrat",
      partyid == 1 ~ "Not strong Democrat",
      partyid == 2 ~ "Independent-Democrat",
      partyid == 3 ~ "Independent",
      partyid == 4 ~ "Independent-Republican",
      partyid == 5 ~ "Not strong Republican",
      partyid == 6 ~ "Strong Republican",
      partyid == 7 ~ "Other",
      TRUE ~ NA_character_
    )
  )

To add labels to the indus10 variable (Industry and Occupation Code Lists), please refer to the website below:
https://www.census.gov/topics/employment/industry-occupation/guidance/code-lists.html
