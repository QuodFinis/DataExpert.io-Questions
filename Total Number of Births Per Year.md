# Total Number of Births Per Year

## Problem Statement
Write a SQL query to calculate the total number of births recorded for each year in the `playground.us_birth_stats` table. The table includes the following columns:
- `year` (integer)
- `month` (integer)
- `date_of_month` (integer)
- `day_of_week` (integer)
- `births` (integer)

The result should include:
- `year` (integer)
- `total_births` (integer)

The results should be ordered by `year`.

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
SELECT us_birth_stats.year, SUM(us_birth_stats.births) AS total_births
FROM playground.us_birth_stats
GROUP BY us_birth_stats.year
ORDER BY us_birth_stats.year;
```
Note: It is standard practice to use the table_name.column_name convention, and this is especially the case for column ```year``` where it might be confused with the function ```YEAR()```.

### Explanation
The key to creating this query is understanding that `SUM` aggregation in the `SELECT` expression calculates the total for the column specified (in this case, `births`) within each group defined by the `GROUP BY` clause. Here’s a step-by-step breakdown:
1. **Select and Aggregate**: Use `SUM(us_birth_stats.births)` to calculate the total number of births for each year.
2. **Group by Year**: The `GROUP BY us_birth_stats.year` ensures that the `SUM` function operates on the births column for each year separately.
3. **Order Results**: The `ORDER BY us_birth_stats.year` arranges the output in ascending order of years for better readability and analysis.
