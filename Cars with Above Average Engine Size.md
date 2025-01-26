# Cars with Above Average Engine Size

## Problem Statement
Using the table `playground.automobile`, write a SQL query to identify cars that have an engine size above the average across all cars in the dataset. The table includes the following columns:
- `brand_name` (string)
- `fuel_type` (string)
- `aspiration` (string)
- `door_panel` (string)
- `design` (string)
- `wheel_drive` (string)
- `engine_location` (string)
- `engine_type` (string)
- `cylinder_count` (string)
- `engine_size` (integer)
- `fuel_system` (string)
- `bore` (double)
- `stroke` (double)
- `compression_ratio` (double)
- `horse_power` (integer)
- `top_RPM` (integer)
- `city_mileage` (integer)
- `highway_mileage` (integer)
- `price_in_dollars` (integer)

The result should include:
- `brand_name` (varchar)
- `fuel_type` (varchar)
- `engine_size` (integer)

The results should be ordered by `engine_size` in descending order and then by `brand_name` in ascending order.

### Sample Data
| brand_name   | fuel_type | aspiration | door_panel | design      | wheel_drive | engine_location | engine_type | cylinder_count | engine_size | fuel_system | bore | stroke | compression_ratio | horse_power | top_RPM | city_mileage | highway_mileage | price_in_dollars |
|--------------|-----------|------------|------------|-------------|-------------|-----------------|-------------|----------------|-------------|-------------|------|--------|-------------------|-------------|---------|--------------|-----------------|------------------|
| alfa-romero  | gas       | std        | two        | convertible | rwd         | front           | dohc        | four           | 130         | mpfi        | 3.47 | 2.68   | 9                 | 111         | 5000    | 21           | 27              | 13495            |
| volvo        | gas       | turbo      | four       | sedan       | rwd         | front           | ohc         | four           | 141         | mpfi        | 3.78 | 3.15   | 9.5               | 114         | 5400    | 19           | 25              | 22625            |
| volvo        | diesel    | turbo      | four       | sedan       | rwd         | front           | ohc         | six            | 145         | idi         | 3.01 | 3.4    | 23                | 106         | 4800    | 26           | 27              | 22470            |
| volvo        | gas       | std        | four       | sedan       | rwd         | front           | ohcv        | six            | 173         | mpfi        | 3.58 | 2.87   | 8.8               | 134         | 5500    | 18           | 23              | 21485            |
| volvo        | gas       | turbo      | four       | sedan       | rwd         | front           | ohc         | four           | 141         | mpfi        | 3.78 | 3.15   | 8.7               | 160         | 5300    | 19           | 25              | 19045            |
| volvo        | gas       | std        | four       | sedan       | rwd         | front           | ohc         | four           | 141         | mpfi        | 3.78 | 3.15   | 9.5               | 114         | 5400    | 23           | 28              | 16845            |
| volvo        | gas       | turbo      | four       | wagon       | rwd         | front           | ohc         | four           | 130         | mpfi        | 3.62 | 3.15   | 7.5               | 162         | 5100    | 17           | 22              | 18950            |
| volvo        | gas       | turbo      | four       | sedan       | rwd         | front           | ohc         | four           | 130         | mpfi        | 3.62 | 3.15   | 7.5               | 162         | 5100    | 17           | 22              | 18420            |
| volvo        | gas       | std        | four       | wagon       | rwd         | front           | ohc         | four           | 141         | mpfi        | 3.78 | 3.15   | 9.5               | 114         | 5400    | 24           | 28              | 16515            |
| volvo        | gas       | std        | four       | sedan       | rwd         | front           | ohc         | four           | 141         | mpfi        | 3.78 | 3.15   | 9.5               | 114         | 5400    | 24           | 28              | 15985            |

## Solution
```sql
SELECT automobile.brand_name, automobile.fuel_type, automobile.engine_size
FROM playground.automobile
WHERE automobile.engine_size > (SELECT AVG(automobile.engine_size) FROM playground.automobile)
ORDER BY automobile.engine_size DESC, automobile.brand_name ASC;
```

### Explanation
A common mistake would be to include the aggregation `AVG()` directly in the `WHERE` clause, but this is incorrect because the `WHERE` clause is applied before any aggregation. Instead, the average engine size is calculated using a subquery, ensuring it can be used in the `WHERE` clause.

1. **Filtering with Subquery**: The `WHERE` clause uses the subquery `(SELECT AVG(automobile.engine_size) FROM playground.automobile)` to calculate the average engine size, ensuring only cars with an engine size greater than the average are included.
2. **Selecting Columns**: The main query selects the `brand_name`, `fuel_type`, and `engine_size` columns for the filtered results.
3. **Ordering Results**: The `ORDER BY automobile.engine_size DESC, automobile.brand_name ASC` arranges the results first by engine size in descending order and then alphabetically by brand name.
