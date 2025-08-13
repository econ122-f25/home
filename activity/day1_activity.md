Week 1, Day 1: In-Class Activity
================
Your Name
2025-08-04

### Introduction

This activity is designed for you to work through at your own pace. It
should take about 40 minutes to complete. The goal is to apply the
fundamental R concepts we covered today in a hands-on way using RStudio.

Please answer the questions and write your code directly in the code
chunks provided below.

### A Note on R Markdown: Running vs. Knitting

It is important to understand the difference between running code chunks
and knitting the document.

- **Running a Code Chunk:** When you click the green ‘play’ button or
  press `Ctrl + Enter` inside a chunk, the code is executed directly in
  the R console. This is useful for testing your code and seeing the
  results immediately.

- **Knitting the Document:** When you click the ‘Knit’ button, RStudio
  runs all of the code chunks in the document from top to bottom in a
  clean, isolated session. This process creates a final, reproducible
  output file (like this HTML file). It ensures that your entire
  analysis runs from start to finish without errors.

### Part 1: R Basics and Variable Assignment (10 minutes)

**Task 1.1: Hello, R!** Use R as a calculator to find the result of
$$(150 + 75) / 3$$ in the code chunk below.

``` r
# Write your code here to calculate the result
```

**Task 1.2: Creating Variables** Create three new variables in the code
chunk below. - `my_age`: Your age as a numeric value. - `my_name`: Your
name as a character string. - `is_student`: A logical value (`TRUE` or
`FALSE`) to indicate if you are a student.

``` r
# Write your code to create the variables here
my_age <- 10
my_name <- 'hell'
is_student <- 1
```

**Task 1.3: Combining Variables** Use the `paste()` function to create a
new variable called `greeting` that combines your name and a welcome
message. For example: “Hello, `Your Name`! Welcome to Data Science.”

``` r
# Write your code to create the greeting variable here
```

### Part 2: Exploring Data Types & Logical Operations (15 minutes)

**Task 2.1: Checking the Class** Use the `class()` function to check the
data type of the three variables you created in Part 1. Explain what
each output means in the space below.

``` r
# Write your code to check the class of each variable here
```

**Task 2.2: Integer vs. Numeric** Create two variables, one storing the
number 10 as a numeric and another storing 10 as an integer. Use the
`class()` function to show the difference.

*Hint: Remember to use the `L` suffix for integers.*

``` r
# Write your code here to demonstrate the difference
```

**Task 2.3: Logical Operations** Use logical operators (`>`, `<`, `==`,
`!=`) to answer the following questions. Write the R code and the output
you expect.

1.  Is $10$ greater than $5$?
2.  Is “R” the same as “r”?
3.  Is the variable `is_student` true?

``` r
# Write your code to check the logical conditions here
```

### Part 3: Introduction to Vectors (15 minutes)

**Task 3.1: Creating a Vector** Vectors are the most basic data
structure in R. Use the `c()` function to create a vector named
`my_numbers` with the values $5, 10, 15, 20$. Then, print the vector.

``` r
# Create and print the vector here
```

**Task 3.2: Vector Operations** Add a new number, $25$, to your
`my_numbers` vector. You can do this by re-assigning the variable. Then,
calculate the sum and the mean of the new vector.

``` r
# Write your code here to update the vector and perform calculations
```

**Task 3.3: Logical Vectors** Create a new vector called `is_even` that
contains logical values (`TRUE` or `FALSE`) for each element in your
`my_numbers` vector, indicating whether the number is even.

*Hint: The modulo operator `%%` is useful for this.*

``` r
# Write your code here to create the logical vector
```

### Challenge Question (For early finishers)

Imagine you have a vector of temperatures in Celsius:
`c(10, 15, 20, 25)`. How would you convert this entire vector to
Fahrenheit using a single line of R code? The formula for Celsius to
Fahrenheit is

$$
(C \times 9/5) + 32
$$

.

``` r
# Write the challenge question solution here
```
