## Summary statistics

<div style="width: 400px;">

| Statistic | Value |
|:---------:|:-----:|
| Count | 28 |
| Mean | 83.36 |
| Std Dev | 9.43 |
| Min | 55 |
| 10th percentile | 71.40 |
| 25th percentile | 80.00 |
| Median (50th) | 85.00 |
| 75th percentile | 89.00 |
| 90th percentile | 93.60 |
| Max | 96 |

</div>


## Common Mistakes by Question

**Q1: Data Types & Logical Operations**

- Called x "vector" not "numeric"/"double" (15+ students)
- Issues with logical 
    - Reposting of question
      - `x <- c(12.3, 16.5, 9.8)`
      - `Given the R code x < 15, what would be the output?`
      - `What is the output of sum(x < 15)`
    - Gave 22.1 (sum) instead of 2 (count of TRUE) - misunderstood boolean arithmetic (16+ students)
        - Only 1 person got it right even though most people got the previous question `Given the R code x < 15, what would be the output?` right
        - I only took 1 point off here instead of 4 since only 1 person got it right

**Q2: dplyr Verbs**

- Didn't use `group_by` for aggregation
- Used `mutate()` instead of `summarize()` for aggregation (8+ students)
- Invalid syntax: `mutate(summarize())`, used `<-` inside mutate

**Q4: Joins**

- Wrong row count: said 2 not 3 (didn't count S001 twice)
- Misunderstood semi_join: thought it includes both tables' columns (4 students)

**Q9: Outlier Detection**

- **Critical error:** Said use z-score for skewed data (should be IQR) (2 students)
- Missing robustness discussion (median/quartiles)
