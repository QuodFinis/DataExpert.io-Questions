# Average Number of Births by Day of the Week

## Problem Statement
Create a SQL query to calculate the average number of births for each day of the week across all years in the `playground.us_birth_stats` table. The average should be cast as an integer. The results should include:
- `day_of_week` (integer)
- `average_births` (integer)

Order the results by `day_of_week`.

### Sample Data
| year  | month | date_of_month | day_of_week | births |
|-------|-------|---------------|-------------|--------|
| 2000  | 1     | 1             | 6           | 9083   |
| 2014  | 12    | 31            | 3           | 11990  |
| 2014  | 12    | 30            | 2           | 13634  |
| 2014  | 12    | 29            | 1           | 12811  |
| 2014  | 12    | 28            | 7           | 7724   |
| 2014  | 12    | 27            | 6           | 8656   |
| 2014  | 12    | 26            | 5           | 10386  |
| 2014  | 12    | 25            | 4           | 6749   |
| 2014  | 12    | 24            | 3           | 9308   |
| 2014  | 12    | 23            | 2           | 12604  |

## Solution Query
```sql
SELECT us_birth_stats.day_of_week, ROUND(AVG(us_birth_stats.births)) AS average_births
FROM playground.us_birth_stats
GROUP BY us_birth_stats.day_of_week
ORDER BY us_birth_stats.day_of_week;
```

### Explanation
A common mistake is assuming that `AVG()` alone can automatically produce integer results or that it can be applied without `GROUP BY`. However, averages are computed per group, and casting the result as an integer requires explicit use of functions like `ROUND()`.

1. **Calculating Averages**: The `AVG(us_birth_stats.births)` function calculates the average number of births for each `day_of_week`. 
2. **Rounding the Result**: The `ROUND()` function is applied to cast the average to an integer value.
3. **Grouping by Day of the Week**: The `GROUP BY us_birth_stats.day_of_week` groups the data by each day of the week so the averages are computed for each unique day.
4. **Ordering Results**: The `ORDER BY us_birth_stats.day_of_week` arranges the output in ascending order of the days of the week.
