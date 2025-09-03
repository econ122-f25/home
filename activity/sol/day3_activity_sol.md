Data Wrangling with `dplyr`: In-Class Activity (Solutions)
================
Your Name
2025-08-05

## Welcome to Your `dplyr` Activity! (5 minutes)

This activity is designed to give you hands-on practice with the core
`dplyr` verbs we just discussed. You’ll be working with the `starwars`
dataset, which is already available when you load `dplyr`.

**Goal:** By the end of this activity, you should feel more comfortable
using `filter()`, `select()`, `arrange()`, `mutate()`, `summarize()`,
and `group_by()`, including combining them for more complex tasks.

**Instructions:**

1.  Read each task carefully.
2.  Write your R code in the provided code chunks.
3.  Run the code chunk to see your output.
4.  Compare your output with the expected results or hints.
5.  Don’t be afraid to experiment! If you get stuck, refer back to the
    presentation slides or discuss with a classmate.

Let’s get started!

### Load Libraries and Data

First, make sure you have the necessary packages loaded.

``` r
library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
# The starwars dataset is automatically available after loading dplyr
```

------------------------------------------------------------------------

## Task 1: Filtering Data (`filter()`) (8 minutes)

The `filter()` verb allows you to select rows based on conditions.

**Exercise 1.1:** Find all `starwars` characters whose `species` is
“Droid”.

``` r
starwars %>%
  filter(species == "Droid")
```

    ## # A tibble: 6 × 14
    ##   name   height  mass hair_color skin_color  eye_color birth_year sex   gender  
    ##   <chr>   <int> <dbl> <chr>      <chr>       <chr>          <dbl> <chr> <chr>   
    ## 1 C-3PO     167    75 <NA>       gold        yellow           112 none  masculi…
    ## 2 R2-D2      96    32 <NA>       white, blue red               33 none  masculi…
    ## 3 R5-D4      97    32 <NA>       white, red  red               NA none  masculi…
    ## 4 IG-88     200   140 none       metal       red               15 none  masculi…
    ## 5 R4-P17     96    NA none       silver, red red, blue         NA none  feminine
    ## 6 BB8        NA    NA none       none        black             NA none  masculi…
    ## # ℹ 5 more variables: homeworld <chr>, species <chr>, films <list>,
    ## #   vehicles <list>, starships <list>

**Exercise 1.2:** Find all `starwars` characters who are “Human” AND
have a `height` greater than 180.

``` r
starwars %>%
  filter(species == "Human" & height > 180)
```

    ## # A tibble: 15 × 14
    ##    name     height  mass hair_color skin_color eye_color birth_year sex   gender
    ##    <chr>     <int> <dbl> <chr>      <chr>      <chr>          <dbl> <chr> <chr> 
    ##  1 Darth V…    202 136   none       white      yellow          41.9 male  mascu…
    ##  2 Biggs D…    183  84   black      light      brown           24   male  mascu…
    ##  3 Obi-Wan…    182  77   auburn, w… fair       blue-gray       57   male  mascu…
    ##  4 Anakin …    188  84   blond      fair       blue            41.9 male  mascu…
    ##  5 Boba Fe…    183  78.2 black      fair       brown           31.5 male  mascu…
    ##  6 Qui-Gon…    193  89   brown      fair       blue            92   male  mascu…
    ##  7 Padmé A…    185  45   brown      light      brown           46   fema… femin…
    ##  8 Ric Olié    183  NA   brown      fair       blue            NA   male  mascu…
    ##  9 Quarsh …    183  NA   black      dark       brown           62   male  mascu…
    ## 10 Mace Wi…    188  84   none       dark       brown           72   male  mascu…
    ## 11 Cliegg …    183  NA   brown      fair       blue            82   male  mascu…
    ## 12 Dooku       193  80   white      fair       brown          102   male  mascu…
    ## 13 Bail Pr…    191  NA   black      tan        brown           67   male  mascu…
    ## 14 Jango F…    183  79   black      tan        brown           66   male  mascu…
    ## 15 Raymus …    188  79   brown      light      brown           NA   male  mascu…
    ## # ℹ 5 more variables: homeworld <chr>, species <chr>, films <list>,
    ## #   vehicles <list>, starships <list>

**Exercise 1.3 (Challenging Filter):** Find all `starwars` characters
who have either “brown” or “black” `hair_color` AND have either “blue”
or “brown” `eye_color`.

``` r
starwars %>%
  filter((hair_color == "brown" | hair_color == "black") & (eye_color == "blue" | eye_color == "brown"))
```

    ## # A tibble: 27 × 14
    ##    name     height  mass hair_color skin_color eye_color birth_year sex   gender
    ##    <chr>     <int> <dbl> <chr>      <chr>      <chr>          <dbl> <chr> <chr> 
    ##  1 Leia Or…    150  49   brown      light      brown           19   fema… femin…
    ##  2 Beru Wh…    165  75   brown      light      blue            47   fema… femin…
    ##  3 Biggs D…    183  84   black      light      brown           24   male  mascu…
    ##  4 Chewbac…    228 112   brown      unknown    blue           200   male  mascu…
    ##  5 Han Solo    180  80   brown      fair       brown           29   male  mascu…
    ##  6 Jek Ton…    180 110   brown      fair       blue            NA   <NA>  <NA>  
    ##  7 Boba Fe…    183  78.2 black      fair       brown           31.5 male  mascu…
    ##  8 Lando C…    177  79   black      dark       brown           31   male  mascu…
    ##  9 Arvel C…     NA  NA   brown      fair       brown           NA   male  mascu…
    ## 10 Wicket …     88  20   brown      brown      brown            8   male  mascu…
    ## # ℹ 17 more rows
    ## # ℹ 5 more variables: homeworld <chr>, species <chr>, films <list>,
    ## #   vehicles <list>, starships <list>

------------------------------------------------------------------------

## Task 2: Selecting Columns (`select()`) (7 minutes)

The `select()` verb allows you to choose specific columns.

**Exercise 2.1:** Select only the `name`, `species`, and `homeworld`
columns from the `starwars` dataset.

``` r
starwars %>%
  select(name, species, homeworld)
```

    ## # A tibble: 87 × 3
    ##    name               species homeworld
    ##    <chr>              <chr>   <chr>    
    ##  1 Luke Skywalker     Human   Tatooine 
    ##  2 C-3PO              Droid   Tatooine 
    ##  3 R2-D2              Droid   Naboo    
    ##  4 Darth Vader        Human   Tatooine 
    ##  5 Leia Organa        Human   Alderaan 
    ##  6 Owen Lars          Human   Tatooine 
    ##  7 Beru Whitesun Lars Human   Tatooine 
    ##  8 R5-D4              Droid   Tatooine 
    ##  9 Biggs Darklighter  Human   Tatooine 
    ## 10 Obi-Wan Kenobi     Human   Stewjon  
    ## # ℹ 77 more rows

**Exercise 2.2:** Select all columns EXCEPT `films` and `vehicles`.

``` r
starwars %>%
  select(-films, -vehicles)
```

    ## # A tibble: 87 × 12
    ##    name     height  mass hair_color skin_color eye_color birth_year sex   gender
    ##    <chr>     <int> <dbl> <chr>      <chr>      <chr>          <dbl> <chr> <chr> 
    ##  1 Luke Sk…    172    77 blond      fair       blue            19   male  mascu…
    ##  2 C-3PO       167    75 <NA>       gold       yellow         112   none  mascu…
    ##  3 R2-D2        96    32 <NA>       white, bl… red             33   none  mascu…
    ##  4 Darth V…    202   136 none       white      yellow          41.9 male  mascu…
    ##  5 Leia Or…    150    49 brown      light      brown           19   fema… femin…
    ##  6 Owen La…    178   120 brown, gr… light      blue            52   male  mascu…
    ##  7 Beru Wh…    165    75 brown      light      blue            47   fema… femin…
    ##  8 R5-D4        97    32 <NA>       white, red red             NA   none  mascu…
    ##  9 Biggs D…    183    84 black      light      brown           24   male  mascu…
    ## 10 Obi-Wan…    182    77 auburn, w… fair       blue-gray       57   male  mascu…
    ## # ℹ 77 more rows
    ## # ℹ 3 more variables: homeworld <chr>, species <chr>, starships <list>

**Exercise 2.3 (Challenging Select):** Select all columns that contain
the word “color” (e.g., `hair_color`, `skin_color`, `eye_color`).

``` r
starwars %>%
  select(contains("color"))
```

    ## # A tibble: 87 × 3
    ##    hair_color    skin_color  eye_color
    ##    <chr>         <chr>       <chr>    
    ##  1 blond         fair        blue     
    ##  2 <NA>          gold        yellow   
    ##  3 <NA>          white, blue red      
    ##  4 none          white       yellow   
    ##  5 brown         light       brown    
    ##  6 brown, grey   light       blue     
    ##  7 brown         light       blue     
    ##  8 <NA>          white, red  red      
    ##  9 black         light       brown    
    ## 10 auburn, white fair        blue-gray
    ## # ℹ 77 more rows

------------------------------------------------------------------------

## Task 3: Arranging Rows (`arrange()`) (5 minutes)

The `arrange()` verb sorts your data.

**Exercise 3.1:** Arrange the `starwars` data by `mass` in ascending
order. (Note: `arrange()` handles `NA` values by default, placing them
at the end for ascending sort).

``` r
starwars %>%
  arrange(mass)
```

    ## # A tibble: 87 × 14
    ##    name     height  mass hair_color skin_color eye_color birth_year sex   gender
    ##    <chr>     <int> <dbl> <chr>      <chr>      <chr>          <dbl> <chr> <chr> 
    ##  1 Ratts T…     79    15 none       grey, blue unknown           NA male  mascu…
    ##  2 Yoda         66    17 white      green      brown            896 male  mascu…
    ##  3 Wicket …     88    20 brown      brown      brown              8 male  mascu…
    ##  4 R2-D2        96    32 <NA>       white, bl… red               33 none  mascu…
    ##  5 R5-D4        97    32 <NA>       white, red red               NA none  mascu…
    ##  6 Sebulba     112    40 none       grey, red  orange            NA male  mascu…
    ##  7 Padmé A…    185    45 brown      light      brown             46 fema… femin…
    ##  8 Dud Bolt     94    45 none       blue, grey yellow            NA male  mascu…
    ##  9 Wat Tam…    193    48 none       green, gr… unknown           NA male  mascu…
    ## 10 Sly Moo…    178    48 none       pale       white             NA <NA>  <NA>  
    ## # ℹ 77 more rows
    ## # ℹ 5 more variables: homeworld <chr>, species <chr>, films <list>,
    ## #   vehicles <list>, starships <list>

**Exercise 3.2 (Challenging Arrange):** Arrange the `starwars` data
first by `species` in ascending order, then by `height` in descending
order, and finally by `name` in ascending order for characters with the
same species and height.

``` r
starwars %>%
  arrange(species, desc(height), name)
```

    ## # A tibble: 87 × 14
    ##    name     height  mass hair_color skin_color eye_color birth_year sex   gender
    ##    <chr>     <int> <dbl> <chr>      <chr>      <chr>          <dbl> <chr> <chr> 
    ##  1 Ratts T…     79    15 none       grey, blue unknown           NA male  mascu…
    ##  2 Dexter …    198   102 none       brown      yellow            NA male  mascu…
    ##  3 Ki-Adi-…    198    82 white      pale       yellow            92 male  mascu…
    ##  4 Mas Ame…    196    NA none       blue       blue              NA male  mascu…
    ##  5 Zam Wes…    168    55 blonde     fair, gre… yellow            NA fema… femin…
    ##  6 IG-88       200   140 none       metal      red               15 none  mascu…
    ##  7 C-3PO       167    75 <NA>       gold       yellow           112 none  mascu…
    ##  8 R5-D4        97    32 <NA>       white, red red               NA none  mascu…
    ##  9 R2-D2        96    32 <NA>       white, bl… red               33 none  mascu…
    ## 10 R4-P17       96    NA none       silver, r… red, blue         NA none  femin…
    ## # ℹ 77 more rows
    ## # ℹ 5 more variables: homeworld <chr>, species <chr>, films <list>,
    ## #   vehicles <list>, starships <list>

------------------------------------------------------------------------

## Task 4: Adding/Modifying Columns (`mutate()`) (8 minutes)

The `mutate()` verb creates new columns or modifies existing ones.

**Exercise 4.1:** Create a new column called `height_meters` that
converts `height` from centimeters to meters (divide by 100). Then,
select `name`, `height`, and your new `height_meters` column.

``` r
starwars %>%
  mutate(height_meters = height / 100) %>%
  select(name, height, height_meters)
```

    ## # A tibble: 87 × 3
    ##    name               height height_meters
    ##    <chr>               <int>         <dbl>
    ##  1 Luke Skywalker        172          1.72
    ##  2 C-3PO                 167          1.67
    ##  3 R2-D2                  96          0.96
    ##  4 Darth Vader           202          2.02
    ##  5 Leia Organa           150          1.5 
    ##  6 Owen Lars             178          1.78
    ##  7 Beru Whitesun Lars    165          1.65
    ##  8 R5-D4                  97          0.97
    ##  9 Biggs Darklighter     183          1.83
    ## 10 Obi-Wan Kenobi        182          1.82
    ## # ℹ 77 more rows

**Exercise 4.2:** Create a new column called `bmi` (Body Mass Index).
The formula for BMI is `mass / (height_meters^2)`. Remember to use the
`height_meters` column you just created. Select `name`, `height`,
`mass`, and your new `bmi` column.

``` r
starwars %>%
  mutate(height_meters = height / 100,
         bmi = mass / (height_meters^2)) %>%
  select(name, height, mass, bmi)
```

    ## # A tibble: 87 × 4
    ##    name               height  mass   bmi
    ##    <chr>               <int> <dbl> <dbl>
    ##  1 Luke Skywalker        172    77  26.0
    ##  2 C-3PO                 167    75  26.9
    ##  3 R2-D2                  96    32  34.7
    ##  4 Darth Vader           202   136  33.3
    ##  5 Leia Organa           150    49  21.8
    ##  6 Owen Lars             178   120  37.9
    ##  7 Beru Whitesun Lars    165    75  27.5
    ##  8 R5-D4                  97    32  34.0
    ##  9 Biggs Darklighter     183    84  25.1
    ## 10 Obi-Wan Kenobi        182    77  23.2
    ## # ℹ 77 more rows

**Exercise 4.3 (Challenging Mutate):** Create a new column called
`mass_class`. Use `case_when()` to assign the following categories based
on `mass`: \* `mass < 50`: “Light” \* `mass >= 50 & mass < 100`:
“Medium” \* `mass >= 100`: “Heavy” \* For `NA` values in `mass`, assign
“Unknown”. Select `name`, `mass`, and your new `mass_class` column.

``` r
starwars %>%
  mutate(mass_class = case_when(
    is.na(mass) ~ "Unknown",
    mass < 50 ~ "Light",
    mass >= 50 & mass < 100 ~ "Medium",
    mass >= 100 ~ "Heavy",
    TRUE ~ "Other" # Catch-all for any other cases, though not strictly needed here
  )) %>%
  select(name, mass, mass_class)
```

    ## # A tibble: 87 × 3
    ##    name                mass mass_class
    ##    <chr>              <dbl> <chr>     
    ##  1 Luke Skywalker        77 Medium    
    ##  2 C-3PO                 75 Medium    
    ##  3 R2-D2                 32 Light     
    ##  4 Darth Vader          136 Heavy     
    ##  5 Leia Organa           49 Light     
    ##  6 Owen Lars            120 Heavy     
    ##  7 Beru Whitesun Lars    75 Medium    
    ##  8 R5-D4                 32 Light     
    ##  9 Biggs Darklighter     84 Medium    
    ## 10 Obi-Wan Kenobi        77 Medium    
    ## # ℹ 77 more rows

------------------------------------------------------------------------

## Task 5: Summarizing and Grouping (`summarize()`, `group_by()`, `n()`, `n_distinct()`) (7 minutes)

These verbs are often used together to get insights from your data.

**Exercise 5.1:** Calculate the average `mass` for each `species`.
Exclude `NA` values from the mass calculation.

``` r
starwars %>%
  group_by(species) %>%
  summarize(average_mass = mean(mass, na.rm = TRUE))
```

    ## # A tibble: 38 × 2
    ##    species   average_mass
    ##    <chr>            <dbl>
    ##  1 Aleena            15  
    ##  2 Besalisk         102  
    ##  3 Cerean            82  
    ##  4 Chagrian         NaN  
    ##  5 Clawdite          55  
    ##  6 Droid             69.8
    ##  7 Dug               40  
    ##  8 Ewok              20  
    ##  9 Geonosian         80  
    ## 10 Gungan            74  
    ## # ℹ 28 more rows

**Exercise 5.2:** Count how many characters there are for each
`eye_color`. Order the results by the count in descending order.

``` r
starwars %>%
  group_by(eye_color) %>%
  summarize(count = n()) %>%
  arrange(desc(count))
```

    ## # A tibble: 15 × 2
    ##    eye_color     count
    ##    <chr>         <int>
    ##  1 brown            21
    ##  2 blue             19
    ##  3 yellow           11
    ##  4 black            10
    ##  5 orange            8
    ##  6 red               5
    ##  7 hazel             3
    ##  8 unknown           3
    ##  9 blue-gray         1
    ## 10 dark              1
    ## 11 gold              1
    ## 12 green, yellow     1
    ## 13 pink              1
    ## 14 red, blue         1
    ## 15 white             1

**Exercise 5.3 (Challenging Summary):** For each `species`, calculate
the **average `height`**, the **average `mass`**, and the **number of
distinct `homeworld`s**. Only include species that have **more than 10
characters**. Order the final result by the number of characters in
descending order.

``` r
starwars %>%
  group_by(species) %>%
  summarize(
    average_height = mean(height, na.rm = TRUE),
    average_mass = mean(mass, na.rm = TRUE),
    num_characters = n(),
    distinct_homeworlds = n_distinct(homeworld)
  ) %>%
  filter(num_characters > 10) %>%
  arrange(desc(num_characters))
```

    ## # A tibble: 1 × 5
    ##   species average_height average_mass num_characters distinct_homeworlds
    ##   <chr>            <dbl>        <dbl>          <int>               <int>
    ## 1 Human              178         81.3             35                  15

------------------------------------------------------------------------

## Wrap-up (Optional: 5 minutes for discussion)

Take a moment to review your answers.

- Did you find any challenges?
- Which `dplyr` verb do you think will be most useful for your own data?
- Discuss with a neighbor any parts you found particularly tricky or
  elegant.

Feel free to ask questions if anything is unclear!
