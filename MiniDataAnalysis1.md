# Mini Data-Analysis: Deliverable 1
Rosemary Joseph

Total points available: 74

# Part 0: Getting Set Up

Let’s get ready to work on this assignment!

**0.1: Install Packages**

- Install the [`diversedata`](https://diverse-data-hub.github.io/)
  package by typing the following into your **R console**:

<!-- -->

    install.packages("pak")
    library(pak)
    pak::pak("diverse-data-hub/diversedata")

**0.2: Load Packages**

Typically, R Packages are loaded in at the very beginning of the
analysis. If you later want to use other packages, please come back and
add them here:

``` r
library(tidyverse)
library(diversedata)
library(moderndive)
#--- Add any other packages below this line ---#
```

# Task 1: Choose a Data Set and Research Question

You may use one of the datasets from class or one of the datasets from
`diversedatahub`.

- **boulder-housing**: This data set contains housing information for
  the Boulder, Colorado area. *\[Add a second sentence here describing
  what the data covers — e.g., the variables included or what question
  it was collected to answer.\]*

- **squirrel-census**: Thes\[[great NYC squirrel
  census](https://www.thesquirrelcensus.com/),`squirrel-data.csv` –
  squirrel sightings recorded around Manhattan and Brooklyn parks.

- **rolling stone**: A [new visual
  essay](https://pudding.cool/2024/03/greatest-music/) from The Pudding
  compares Rolling Stone’s “500 Greatest Albums of All Time” lists from
  2003, 2012, and 2020. A methodology note says the project began with a
  spreadsheet by Chris Eckert and eventually led the authors to develop
  a dataset of their own. Theirs lists every album in the rankings — its
  name, genre, release year, 2003/2012/2020 rank, the artist’s name,
  birth year, gender, and more — plus each year’s voters. \[h/t Jason
  Kottke\]

- **coffee census**: In 2023, [British
  YouTuber](https://www.youtube.com/channel/UCMb0O2CdPBNi-QqPk5T3gsQ)
  (and former [World Barista
  Champion](https://www.jameshoffmann.co.uk/work#/coffee-competitions/))
  James Hoffman virtually hosted the [Great American Coffee Taste
  Test](https://www.youtube.com/watch?v=1fN_z4-EcOU), during which
  thousands of people simultaneously blind-tasted the same four coffees.
  Hoffman has published a [video summarizing the
  results](https://www.youtube.com/watch?v=bMOOQfeloH0), as well as [a
  spreadsheet of anonymized survey
  responses](https://bit.ly/gacttCSV+)from 4,000+ participants. It
  includes tasters’ demographics, general coffee drinking habits and
  preferences, assessments of the four coffees, and more. \[h/t Dan
  Brady\] (via
  [data-is-plural](https://www.data-is-plural.com/archive/2023-11-15-edition/))

- **wildfire**: This data set contains information on wildfires in
  Canada, compiled from official government sources under the Open
  Government Licence – Alberta. The data was gathered to monitor,
  assess, and respond to wildfire risks across different regions.
  Wildfires have far-reaching environmental, social, and economic
  consequences. From an equity and inclusion perspective, analyzing
  wildfire data can reveal geographic and resource-based disparities in
  detection and containment efforts, and highlight how certain
  populations face greater risks due to climate change and limited
  infrastructure. There are 26551 rows and 35 columns.

- **genderassessment**: Collected in 2023, the data allows for
  comparative evaluation across countries, sectors, and ownership types
  (e.g., Public, Private, Government). Each record represents a company
  and its corresponding evaluation across 28 detailed gender related
  indicators, offering a comprehensive snapshot of corporate gender
  equity worldwide. There are 2000 rows and 29 variables

- **hcmst**: This data set is adapted from the original data set [How
  Couples Meet and Stay Together 2017,
  2022](https://data.stanford.edu/hcmst2017). This study, led by
  researchers from Stanford University, surveyed 1,722 U.S. adults in
  2022 to explore how relationships form and change with time and
  focused on dating habits and the impact of the COVID-19 pandemic on
  relationships. This adapted data set focuses on variables that may
  affect the quality of the relationship, considering demographic
  characteristics of the subjects, couple dynamics, as well as
  COVID-19-related variables. The COVID-19 pandemic had a [significant
  impact](https://pmc.ncbi.nlm.nih.gov/articles/PMC10009005/) on
  romantic relationships in the United States. This data set enables
  exploration of how external factors, like the health of the subjects
  and changes in income, as well as personal behaviors, like conflict
  and intimate dynamics, relate to an individual’s perception of the
  quality of the relationship. There are 1328 rows and 21 columns.

- **womensmarchmadness**: This adapted data set contains historical
  records of every NCAA Division I Women’s Basketball Tournament
  appearance since the tournament began in 1982 up until 2018, capturing
  tournament results across more than four decades of collegiate women’s
  basketball. All data is sourced from the NCAA and contains the data
  behind the story [The Rise and Fall Of Women’s NCAA Tournament
  Dynasties](https://fivethirtyeight.com/features/louisiana-tech-was-the-uconn-of-the-80s/).
  The rise in popularity of the NCAA Women’s March Madness, fueled by
  athletes like Caitlin Clark and Paige Bueckers, reflects a broader
  cultural shift in the recognition of women’s sports. Beyond
  entertainment and athletic achievement, women’s participation in sport
  has social and professional benefits. There are 2092 rows and 20
  columns.

*Note: We encourage you to use one of the options above, but if you have
a data set that you’d really like to use, please check with a member of
the teaching team to see whether the data set is of appropriate
complexity. If approved, please add a brief description of the data
here.*

### 1.1: Choose 2 data sets **(2 points)**

Out of the 5 data sets listed above, choose **2** that appeal to you
based on their description. Write your choices below:

<!-------------------------- Start your work below ---------------------------->

1: genderassessments

2: hcmst

<!----------------------------------------------------------------------------->

### 1.2: Explore the Data **(12 points)**

One way to narrowing down your selection is to *explore* the data sets.
Use your knowledge of `dplyr` to summarize three variables in each of
the data sets (for example, listing what levels of a categorical
variable exist, or calculating the mean of a continuous variable of
interest). Write a sentence that describes your findings for each
variable explored. You may use multiple R code chunks if preferred.

<!-------------------------- Start your work below ---------------------------->

#### Data Set 1

``` r
### Explore 3 variables of data set 1 ###
genderassessment |>
  filter(ownership %in% c("Government", "Public"), year == 2024) |>
  group_by(ownership) |>
  summarize(mean_paidleave = mean(carer_leave_paid, na.rm = TRUE))
```

    # A tibble: 2 × 2
      ownership  mean_paidleave
      <chr>               <dbl>
    1 Government         0.0547
    2 Public             0.257 

``` r
genderassessment |>
  filter(year == 2024) |>
  group_by(region) |>
  summarize(open_enviornment_rights = mean(enabling_environment_union_rights)) |>
  arrange(desc(open_enviornment_rights))
```

    # A tibble: 7 × 2
      region                     open_enviornment_rights
      <chr>                                        <dbl>
    1 Sub-Saharan Africa                         0.0256 
    2 East Asia & Pacific                        0.00590
    3 Europe & Central Asia                      0.00426
    4 Latin America & Caribbean                  0      
    5 Middle East & North Africa                 0      
    6 North America                              0      
    7 South Asia                                 0      

``` r
genderassessment |>
  filter(year == 2024) |>
  group_by(industry) |>
  summarize(mean_percent_score = mean(percent_score)) |>
  arrange(desc(mean_percent_score))
```

    # A tibble: 25 × 2
       industry                         mean_percent_score
       <chr>                                         <dbl>
     1 Personal & Household Products                  27.5
     2 Retail                                         24  
     3 Banks                                          20.6
     4 Motor Vehicles & Parts                         18.8
     5 Insurance                                      18.4
     6 <NA>                                           16  
     7 Oil & Gas                                      15  
     8 Capital Goods                                  14.9
     9 Traditional Asset Managers                     14.4
    10 Development Finance Institutions               14.2
    # ℹ 15 more rows

Write your findings here.

I found that government owned companies have an average score (out of 4)
of 0.05 for paid leave policies for caregivers, while public owned
companies have an average score of 0.25 in the year of 2024. As for the
living wage, I found that per region, the culture of enabling an
environment for freedom of association and collective bargaining is on
average only present in Africa, Asia, and Europe. Finally, the after
exploring the average score (in percent) per industry, the personal &
household products, retail, and banks are doing the best overall (but
all of their averages are below 30% so is that still really good).

#### Data Set 2

``` r
### Explore 3 variables of data set 2 ###
hcmst
```

    # A tibble: 1,328 × 21
       subject_age subject_education subject_sex subject_ethnicity
             <dbl> <chr>             <chr>       <chr>            
     1          53 high_school_grad  female      white            
     2          72 some_college      female      white            
     3          43 associate_degree  male        white            
     4          64 some_college      male        white            
     5          60 high_school_grad  female      black            
     6          78 high_school_grad  female      white            
     7          51 associate_degree  male        white            
     8          47 associate_degree  male        2_plus_eth       
     9          62 some_college      female      white            
    10          59 high_school_grad  female      black            
    # ℹ 1,318 more rows
    # ℹ 17 more variables: subject_income_category <chr>,
    #   subject_employment_status <chr>, same_sex_couple <chr>, married <chr>,
    #   sex_frequency <chr>, flirts_with_partner <chr>, fights_with_partner <chr>,
    #   relationship_duration <dbl>, children <dbl>,
    #   rel_change_during_pandemic <chr>, inc_change_during_pandemic <chr>,
    #   subject_had_covid <chr>, partner_had_covid <chr>, …

``` r
hcmst |>
  mutate(vaccination_match = subject_vaccinated == partner_vaccinated, na.rm = TRUE) |>
  group_by(relationship_quality) |>
  count(vaccination_match, relationship_quality) 
```

    # A tibble: 13 × 3
    # Groups:   relationship_quality [5]
       relationship_quality vaccination_match     n
       <chr>                <lgl>             <int>
     1 excellent            FALSE               142
     2 excellent            TRUE                532
     3 excellent            NA                   12
     4 fair                 FALSE                35
     5 fair                 TRUE                 66
     6 fair                 NA                    4
     7 good                 FALSE               134
     8 good                 TRUE                363
     9 good                 NA                    7
    10 poor                 FALSE                12
    11 poor                 TRUE                 16
    12 very_poor            FALSE                 1
    13 very_poor            TRUE                  4

``` r
hcmst |>
  mutate(fights_numeric = parse_number(fights_with_partner)) |>
  group_by(subject_income_category) |>
  summarize(mean_fights = mean(fights_numeric, na.rm = TRUE)) |>
  arrange(desc(mean_fights))
```

    # A tibble: 21 × 2
       subject_income_category mean_fights
       <chr>                         <dbl>
     1 7k_10k                        1.42 
     2 35k_40k                       1.1  
     3 12k_15k                       1.09 
     4 50k_60k                       1.08 
     5 40k_50k                       1.02 
     6 5k_7k                         1    
     7 over_250k                     0.987
     8 20k_25k                       0.966
     9 10k_12k                       0.909
    10 25k_30k                       0.895
    # ℹ 11 more rows

``` r
#relationship got better during covid if not married v married
hcmst |>
  group_by(rel_change_during_pandemic) |>
  summarize(mean_children = mean(children))
```

    # A tibble: 3 × 2
      rel_change_during_pandemic mean_children
      <chr>                              <dbl>
    1 better_than_before                  2.63
    2 no_change                           2.52
    3 worse_than_before                   2.79

Write your findings here. More relationships were reported a better
quality if their vaccination statuses matched. Additionally, there
didn’t seem to be a correlation between the income category and how
often couples fought per week. Similarly, there didn’t seem to be a
correlation between how many children a couple had and whether their
relationship got better or worse during the pandemic.

<!----------------------------------------------------------------------------->

### 1.3: Choose 1 Data Set **(2 points)**

It’s time to choose only one data set. State the data set that you’ve
chosen, and why you’ve chosen it.

<!-------------------------- Start your work below ---------------------------->

I’m choosing the hcmst because I think it is interesting to predict
relationship dynamics and especially how it was affected by the pandemic
as I think attitudes towards COVID-19 can sometimes be indicators for
factors like political views.
<!----------------------------------------------------------------------------->

### 1.4: Research Question **(4 points)**

Let’s choose a primary and a secondary research question to explore.

Write your research questions **as questions**, and be specific. You can
change it later if needed.

> For example, if I had chosen a `titanic` data set for my project, I
> might ask, “(Primary) Is there a relationship between survival and the
> class of the passengers? (Secondary) Does this relationship differ by
> gender?”

<!-------------------------- Start your work below ---------------------------->

Is there a relationship between relationship quality and if couple’s
vaccination statuses match? Does this relationship differ by income
categories?

<!----------------------------------------------------------------------------->

### 1.5: Commit **(2 points)**

Commit your work and push it to GitHub. Include an informative commit
message, and include “(1.5)” in the message.

# Task 2: Further Exploring Your Chosen Data Set

### 2.1: Missing Data **(6 points)**

Missing data is inevitable, and can complicate analyses. Let’s see what
variables (if any) have missing data in your chosen data set.

Your task is to create a table that calculates the proportion of missing
values per variable. Be sure to output the table.

<!-------------------------- Start your work below ---------------------------->

``` r
### Explore missingness here ###
hcmst |>
  summarize(
    mean_age = mean(is.na(subject_age)),
    mean_education = mean(is.na(subject_education)),
    mean_sex = mean(is.na(subject_sex)),
    mean_ethnicity = mean(is.na(subject_ethnicity)),
    mean_incomecat = mean(is.na(subject_income_category)),
    mean_employment = mean(is.na(subject_employment_status)), 
    mean_same_sex = mean(is.na(same_sex_couple)),
    mean_married = mean(is.na(married)),
    mean_sex_frequency = mean(is.na(sex_frequency)),
    mean_flirt_frequency = mean(is.na(flirts_with_partner)),
    mean_fight_frequency = mean(is.na(fights_with_partner)),
    mean_relation_duration = mean(is.na(relationship_duration)),
    mean_children = mean(is.na(children)),
    mean_pandemic_rel_change = mean(is.na(rel_change_during_pandemic)),
    mean_pandemic_inc_change = mean(is.na(inc_change_during_pandemic)),
    mean_subject_covid = mean(is.na(subject_had_covid)),
    mean_partner_covid = mean(is.na(partner_had_covid)),
    mean_subject_vacc = mean(is.na(subject_vaccinated)),
    mean_partner_vacc = mean(is.na(partner_vaccinated)),
    mean_agree_approach = mean(is.na(agree_covid_approach)),
    mean_relationship_quality = mean(is.na(relationship_quality))
  )
```

    # A tibble: 1 × 21
      mean_age mean_education mean_sex mean_ethnicity mean_incomecat mean_employment
         <dbl>          <dbl>    <dbl>          <dbl>          <dbl>           <dbl>
    1        0              0        0              0              0               0
    # ℹ 15 more variables: mean_same_sex <dbl>, mean_married <dbl>,
    #   mean_sex_frequency <dbl>, mean_flirt_frequency <dbl>,
    #   mean_fight_frequency <dbl>, mean_relation_duration <dbl>,
    #   mean_children <dbl>, mean_pandemic_rel_change <dbl>,
    #   mean_pandemic_inc_change <dbl>, mean_subject_covid <dbl>,
    #   mean_partner_covid <dbl>, mean_subject_vacc <dbl>, mean_partner_vacc <dbl>,
    #   mean_agree_approach <dbl>, mean_relationship_quality <dbl>

<!----------------------------------------------------------------------------->

### 2.2: Missing Data (Again) **(6 points)**

Based on your research question, will this missingness pose an issue?
For the purposes of this class (and this class only!), we will consider
missingness a problem **if there is more than 20% of a single variable
(that is of interest) is missing**.

> For example, let’s assume I wanted to explore the following research
> questions: “Is there a relationship between survival and the class of
> the passengers? Does this relationship vary by gender?”. If the
> variable indicating whether or not a person survived was missing for
> 20% or more of the passengers, then this would be a problem. However,
> if a variable indicating the colour of shirt a passenger was wearing
> was missing, this probably wouldn’t be an issue as that variable is
> quite irrelevant to my analysis!

Based on this definition, is missingness an issue for your analysis? If
so, describe how you will address this (pivoting your research question,
for example). If you will continue with a new research question, write
it here! **Do not go back to Task 1 and redo the analysis.** ).

If missingness is not an issue, describe why.

<!-------------------------- Start your work below ---------------------------->

Missingness will not be an issue as I am using the variables of
relationship quality, subject vaccination, partner vaccination, and for
my secondary question income categories. Each of these have less than
20% of their observations missing (0, 0.8, 1.6, and 0.15 percent
respectively).

<!----------------------------------------------------------------------------->

### 2.3: Tidy your Data **(10 points)**

Produce a tidy data set that could be used to answer your research
questions. **Please ensure you have at least one quantitative (numeric)
and one categorical variable in your data set. It’s okay you need to
include a less relevant variable in your tidied data to ensure this.**

To tidy your data, you should:

- Create new variables (if needed)

- Transform the data into a tidy form (if needed)

- Remove irrelevant columns (if needed)

- Comment your code throughout

Show the first 6 rows of the tidied data.

<!-------------------------- Start your work below ---------------------------->

``` r
hcmst_tidy <- hcmst |>
  mutate(vaccination_match = subject_vaccinated == partner_vaccinated, na.rm = TRUE) |>
  select(vaccination_match, relationship_quality, subject_income_category, children) 
hcmst_tidy
```

    # A tibble: 1,328 × 4
       vaccination_match relationship_quality subject_income_category children
       <lgl>             <chr>                <chr>                      <dbl>
     1 TRUE              excellent            35k_40k                        2
     2 TRUE              good                 75k_85k                        1
     3 TRUE              excellent            75k_85k                        5
     4 TRUE              good                 75k_85k                        2
     5 FALSE             excellent            75k_85k                        3
     6 TRUE              excellent            50k_60k                        2
     7 TRUE              good                 40k_50k                        3
     8 FALSE             poor                 30k_35k                        2
     9 TRUE              excellent            40k_50k                        2
    10 FALSE             good                 40k_50k                        2
    # ℹ 1,318 more rows

<!----------------------------------------------------------------------------->

### 2.4: Create a Table (10 points)

Use any functions from the `tidyverse` to create one table that outputs
the mean, minimum, and maximum of all numeric columns in your data,
dropping the missing values if they exist.

Show the outputted table.

<!-------------------------- Start your work below ---------------------------->

``` r
hcmst_tidy |>
  summarize(
    mean_children = mean(children),
    min_children = min(children),
    max_children = max(children)
  )
```

    # A tibble: 1 × 3
      mean_children min_children max_children
              <dbl>        <dbl>        <dbl>
    1          2.55            1           10

<!----------------------------------------------------------------------------->

### 2.5: Commit **(2 points)**

Commit your work and push it to GitHub. , and include “(2.7)” in the
message.

# Task 3: Tidy Your Submission Overall

Check over your document and GitHub repository for the following:

### 3.1: Coherence **(2 points)**

The document should read sensibly from top to bottom, with no major
continuity errors. An example of a major continuity error is having a
data set listed for Task 3 that is not part of one of the data sets
listed in Task 1.

### 3.2: Error-free code **(2 points)**

For full marks, all code in the document should run without error and be
completely reproducible.

### 3.3 README **(6 points)**

There should be a file named `README.md` at the top level of your
repository. Its contents should automatically appear when you visit the
repository on GitHub.

Minimum contents of the README file:

- In a sentence or two, explains what this repository is, so that
  future-you or someone else stumbling on your repository can be
  oriented to the repository.
- List the files/folders contained in the repository
- In a sentence or two, briefly explains how to engage with the
  repository. You can assume the person reading knows the material from
  STAT 545A. Basically, if a visitor to your repository wants to explore
  your project, what should they know? How can they reproduce your
  report?

### 3.4 Generative AI Disclosure **(3 points)**

In this course, Generative AI can be used in the following ways:

- to clarify concepts discussed in class

- as an “advanced search engine” (i.e., searching error codes)

- debugging code that students wrote and attempted to debug on their own

Generative AI **CANNOT** be used to generate text or code (including
comments) from scratch.

Any use of Generative AI must be disclosed.

**To disclose your use, please copy and paste the following template
into the README of your GitHub Repository and fill out the relevant
details** \[in square brackets\]. BE SPECIFIC. Saying you used it to
debug your code is not enough. Explicitly describe where you got stuck

Here is an example of a specific, explicit debug:

> “I had the error `attempt to apply non-function` after running my
> code. I used Claude to help me identify that this error was due to me
> attempting to multiply two numbers together without the use of a `*`,
> i.e. `(2)(3)` instead of `2*3`.”

``` markdown

## Generative AI Statement

Generative AI (through [LIST MODELS USED, i.e. ChatGPT, CoPilot)] was used to
help me complete  this assignment in the following ways.

1. [Describe here]

2. [Describe here]

...

I affirm that Generative AI was not used to generate text, code, or comments for
my assessments.
```

If you did not use Generative AI, please include the following in your
README:

``` markdown

## Generative AI Statement

Generative AI was not used in any way throughout this assignment.
```

Assessments suspected of having AI-generated text and/or code, or
assignments where the Generative AI use was not disclosed, will be
flagged and temporarily assigned a grade of zero. Students will be
required to meet with the instructor to receive a grade.

### 3.5 Output **(4 points)**

All output on GitHub is readable, recent and relevant:

- All `.qmd` files have been rendered to their output `.md` files.
- All rendered `.md` files are viewable without errors on Github.
  Examples of errors: Missing plots, “Sorry about that, but we can’t
  show files that are this big right now” messages, error messages from
  broken R code
- All of these output files are up-to-date – that is, they haven’t
  fallen behind after the source (`.qmd`) files have been updated.
- There should be no relic output files. For example, if you were
  rendering a `.qmd` to `.html`, but then changed the output to be only
  a markdown file, then the `.html` file is a relic and should be
  deleted.

# Step 4: Submission

\*\* Submit repo link \*\*

To submit this milestone, submit the github link to the repo.

This assignment was authored by the team of instructors at University of
British Colombia’s STA 545 class.
