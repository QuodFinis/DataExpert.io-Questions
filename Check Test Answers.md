# Check Test Answers

## Problem Statement
Create a SQL query to evaluate test answers stored in a table named `playground.answers` with columns:
- `id` (unique question ID),
- `correct_answer` (string),
- `given_answer` (which can be `NULL`).

Return a table with columns:
- `id` (integer),
- `checks` (varchar), where:
  - `checks` is "no answer" if `given_answer` is `NULL`.
  - `checks` is "correct" if `given_answer` matches `correct_answer`.
  - `checks` is "incorrect" otherwise.

The results should be ordered by `id`.

### Sample Data
| id | correct_answer | given_answer |
|----|----------------|--------------|
| 1  | a              | a            |
| 2  | b              | null         |
| 3  | c              | b            |

## Solution 
```sql
SELECT id,
  CASE
    WHEN given_answer IS NULL THEN 'no answer'
    WHEN given_answer != correct_answer THEN 'incorrect'
    WHEN given_answer = correct_answer THEN 'correct'
  END AS checks
FROM playground.answers
ORDER BY id;
```

### Explanation
Comparing two columns to create a third can be done using the `CASE ... WHEN ... THEN ... END AS` statement, which evaluates different cases (`no answer`, `incorrect`, or `correct`) within the `SELECT` statement. This approach is equivalent but simpler than writing multiple `SELECT` queries and performing a `UNION` between them. Here, the `given_answer` column is compared with the `correct_answer` column using `IS NULL`, `!=`, and `=`. Finally, the results are ordered by `id` for clarity.
