# Find Viewers with Multiple Article Views in a Day

## Problem Statement
Using the table `playground.views`, write a SQL query to identify all viewers who viewed more than one article on the same day. The table includes columns:
- `viewer_id` (the ID of the viewer),
- `article_id` (the ID of the article viewed),
- `view_date` (the date of the view).

The result should contain a single column named `viewer_id`, listing each viewer who meets the criteria without duplicates, and should be sorted in ascending order of `viewer_id`.

### Sample Data
| article_id | author_id | viewer_id | view_date  |
|------------|-----------|-----------|------------|
| 1          | 3         | 5         | 2023-08-14 |
| 3          | 4         | 5         | 2023-08-14 |
| 1          | 3         | 6         | 2023-08-15 |
| 2          | 7         | 7         | 2023-08-14 |
| 2          | 7         | 6         | 2023-08-15 |
| 4          | 7         | 1         | 2023-08-18 |
| 3          | 4         | 4         | 2023-08-17 |
| 3          | 4         | 4         | 2023-08-17 |

## Solution
```sql
SELECT DISTINCT viewer_id
FROM (SELECT DISTINCT * FROM playground.views)
GROUP BY viewer_id, view_date
HAVING COUNT(*) > 1
ORDER BY viewer_id ASC
```

### Explaination
Examining the sample table, notice that a viewer can view the same article more than once and it will be included each time. However, only views of different articles are to be included so we will exclude any duplicates using ```SELECT DISTINCT * FROM playground.views```. With duplicates removed, all remaining rows will be unique visits for articles. To see how many articles a viewer has seen in a day, a ```GROUP BY viewer_id, view_date``` must be performed. With the addition of ```HAVING COUNT(*) > 1``` we can count the rows for each group and filter groups without multiple views per day. While the sample table does not have this example, consider that a user may view multiple articles on different days, so there would a group for each of those different days, required the ```SELECT DISTINCT viewer_id``` to show any user that has ever viewed more than one article on the any day. Finally, ```ORDER BY viewer_id ASC``` will sort the results in ascednding order. 
