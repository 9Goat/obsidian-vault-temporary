there are 3 constraints that fall into this category which are the following:

- **NOT NULL:** Prevents a column from having a `NULL` value.
- **CHECK:** Ensures that all values in a column satisfy a specific condition (e.g., `age >= 18`). 
- **DEFAULT:** While technically an attribute, it acts as a data integrity check by providing a fallback value if none is supplied, preventing unintentional `NULL` entries.

# NOT NULL

The `NOT NULL` constraint enforces that a column **must** contain a value. By default, MySQL columns can hold `NULL` (which represents "unknown" or "missing" data).

## Example

```SQL
-- Column Level ONLY
username VARCHAR(50) NOT NULL
```


# CHECK

The `CHECK` constraint is the most powerful tool for data validation. It allows you to specify a logical expression that every value in that column must satisfy.

## Example

```SQL
-- Column Level
CREATE TABLE orders (
    price DECIMAL(10,2) CHECK (price > 0)
);

-- Table Level
CREATE TABLE orders (
    price DECIMAL(10,2),
    CONSTRAINT chk_min_price CHECK (price > 0)
);
```

# DEFAULT

`DEFAULT` acts as a data check by providing a "fallback." It ensures that a column has a valid value even if the user forgets to provide one.
## Example

```SQL
-- Column Level ONLY
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
```
