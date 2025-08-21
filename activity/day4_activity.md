Day 4: In-Class Activity - Student Data Wrangling
================
Your Name
2025-08-20

## Welcome to Your In-Class Activity!

This activity will give you hands-on practice with the data reshaping
and joining techniques we discussed today. You’ll work with simulated
student and course data from the Claremont Colleges.

**Estimated Time:** 40 minutes

**Goal:** By the end of this activity, you should be comfortable
applying `tidyr` functions for reshaping and `dplyr` functions for
joining datasets.

## Part 1: Data Setup (5 minutes)

First, let’s create the datasets you’ll be working with. Run the
following R code chunk to create three tibbles: `students_raw`,
`colleges_info`, and `course_enrollment`.

``` r
# Raw student data (untidy for reshaping)
students_raw <- tibble(
  student_id = c(101, 102, 103, 104, 105, 106),
  name = c("Alice", "Bob", "Charlie", "David", "Eve", "Frank"),
  Pomona = c("Yes", "No", "Yes", "No", "No", "No"),
  Scripps = c("No", "Yes", "No", "No", "Yes", "No"),
  CMC = c("No", "No", "No", "Yes", "No", "No")
)

# Information about the colleges
colleges_info <- tibble(
  college_name = c("Pomona", "Scripps", "Claremont McKenna", "Harvey Mudd", "Pitzer", "Keck Graduate Institute"),
  college_id = c(1, 2, 3, 4, 5, 6),
  type = c("Liberal Arts", "Liberal Arts", "Liberal Arts", "STEM", "Liberal Arts", "Graduate")
)

# Course enrollment data
course_enrollment <- tibble(
  student_id = c(101, 101, 102, 103, 104, 105, 107),
  course_code = c("DS101", "MATH200", "BIO101", "DS101", "ECON300", "CHEM101", "CS100"),
  semester = c("Fall23", "Fall23", "Spring24", "Fall23", "Spring24", "Fall23", "Fall23")
)

# Display the raw dataframes
print(students_raw)
```

    ## # A tibble: 6 × 5
    ##   student_id name    Pomona Scripps CMC  
    ##        <dbl> <chr>   <chr>  <chr>   <chr>
    ## 1        101 Alice   Yes    No      No   
    ## 2        102 Bob     No     Yes     No   
    ## 3        103 Charlie Yes    No      No   
    ## 4        104 David   No     No      Yes  
    ## 5        105 Eve     No     Yes     No   
    ## 6        106 Frank   No     No      No

``` r
print(colleges_info)
```

    ## # A tibble: 6 × 3
    ##   college_name            college_id type        
    ##   <chr>                        <dbl> <chr>       
    ## 1 Pomona                           1 Liberal Arts
    ## 2 Scripps                          2 Liberal Arts
    ## 3 Claremont McKenna                3 Liberal Arts
    ## 4 Harvey Mudd                      4 STEM        
    ## 5 Pitzer                           5 Liberal Arts
    ## 6 Keck Graduate Institute          6 Graduate

``` r
print(course_enrollment)
```

    ## # A tibble: 7 × 3
    ##   student_id course_code semester
    ##        <dbl> <chr>       <chr>   
    ## 1        101 DS101       Fall23  
    ## 2        101 MATH200     Fall23  
    ## 3        102 BIO101      Spring24
    ## 4        103 DS101       Fall23  
    ## 5        104 ECON300     Spring24
    ## 6        105 CHEM101     Fall23  
    ## 7        107 CS100       Fall23

## Part 2: Reshaping Data (10 minutes)

The `students_raw` data is in a **wide** format, where each college is
its own column. Your task is to transform it into a **tidy (long)**
format, where you have one column for `college_name` and another for
`is_enrolled` (indicating “Yes” or “No”).

**Task:** Use `pivot_longer()` to reshape `students_raw` into a new
tibble called `students_tidy`.

``` r
# Your code here: Reshape students_raw into students_tidy


# Display the tidy student data
```

**Hint:** Remember to specify which columns to pivot, what to name the
new “names” column, and what to name the new “values” column. You might
also want to filter out the “No” entries after pivoting to only show the
colleges a student *is* enrolled in.

## Part 3: Mutating Joins (15 minutes)

Now that you have `students_tidy` and `colleges_info`, let’s combine
them to get more details about the colleges.

**Task 3.1: Add College Type** Use a mutating join to add the `type` of
college (e.g., “Liberal Arts”, “STEM”) from `colleges_info` to your
`students_tidy` data. Store the result in `students_with_college_type`.

``` r
# Your code here: Join students_tidy with colleges_info


# Display the result
```

**Task 3.2: Combine with Course Enrollment** Now, let’s combine
`students_with_college_type` with `course_enrollment` to see which
courses each student is taking. Store the result in `full_student_data`.

``` r
# Your code here: Join students_with_college_type with course_enrollment


# Display the result
```

**Hint:** Pay attention to the common columns between the dataframes for
the `by` argument in your join functions. Consider which type of
mutating join (`inner`, `left`, `full`) makes the most sense for each
task to ensure you keep the desired rows.

## Part 4: Filtering Joins (10 minutes)

Filtering joins are great for identifying subsets of your data.

**Task 4.1: Find Enrolled Students with Courses** Use a filtering join
to identify which students from `students_raw` (before tidying) are
actually enrolled in a course listed in `course_enrollment`. This should
*only* return columns from `students_raw`.

``` r
# Your code here:


# Display the result
```

**Task 4.2: Find Students Without Courses** Now, use another filtering
join to identify which students from `students_raw` are *not* currently
enrolled in any course listed in `course_enrollment`.

``` r
# Your code here:


# Display the result
```

## Reflection & Discussion (Optional)

- What was the most challenging part of this activity for you?
- Can you think of other real-world scenarios where reshaping data would
  be necessary?
- When might an `inner_join()` be more appropriate than a `left_join()`?
- How could `anti_join()` be useful for data cleaning or identifying
  anomalies in a larger dataset?
