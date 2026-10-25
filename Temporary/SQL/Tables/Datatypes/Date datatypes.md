there are 5 main dates datatypes in sql which are the following:

- DATE 
- TIME 
- DATETIME 
- TIMESTAMP 
- YEAR

# DATE

- **Format:** `YYYY-MM-DD`
- **Description:** This type is used when you only need a date without a time component (e.g., a birthday or a national holiday).
- **Range:** It supports a wide range, usually from `'1000-01-01'` to `'9999-12-31'`.


# 2. TIME

- **Format:** `hh:mm:ss`
- **Description:** This stores a time of day or a time interval (duration).
- **Key Detail:** Interestingly, `TIME` can represent more than 24 hours (up to 838 hours) because it can also be used to track the "elapsed time" between two events.

## Syntax

You can use the `D HH:MM:SS` or `HHH:MM:SS` with the extra D and H being **OPTIONAL** format to handle multi-day durations.

| **Input Format**   | **Internal Calculation** | **Resulting Time** |
| ------------------ | ------------------------ | ------------------ |
| **`'12:30'`**      | Assumes `HH:MM:00`       | `12:30:00`         |
| **`'4 12:00:00'`** | $(4 \times 24) + 12$     | `108:00:00`        |
| **`'100:00:00'`**  | Direct hour input        | `100:00:00`        |
| **`'-05:30:00'`**  | Negative duration        | `-05:30:00`        |


# 3. DATETIME

- **Format:** `YYYY-MM-DD hh:mm:ss`
- **Description:** This is a combination of both date and time.
- **NOTE**: unlike time, the maximum and minimum value of `hh:mm:ss` is ` 23:59:59 and 00:00:00` not the 800 hours

# 4. TIMESTAMP

- **Format:** `YYYY-MM-DD hh:mm:ss`
- **Description:** While it looks exactly like `DATETIME`, it behaves differently behind the scenes.
- **Range**: `'1970-01-01'` to `'2038-01-19'`

## How TIMESTAMP Works

When you insert a time into a **TIMESTAMP** column, MySQL doesn't actually store the "date and time" you typed. Instead:

- **Conversion:** MySQL takes your local time, converts it to **UTC** (Coordinated Universal Time), and stores it as a number representing the seconds passed since January 1, 1970 (The "Unix Epoch").
- **Retrieval:** When you select that data later, MySQL looks at your current server or connection time zone and converts that UTC number back into a readable date for you.

## Scenario

A user in **New York (EST)** saves a record at **10:00 AM**. A user in **London (GMT)** then views that same record.

### 1. The Setup

```SQL
CREATE TABLE log_table (
    id INT AUTO_INCREMENT PRIMARY KEY,
    event_name VARCHAR(50),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 2. The Interaction

|Step|User Location|Session Time Zone|Action|Time Seen/Stored|
|---|---|---|---|---|
|**1. Insert**|New York|`America/New_York`|`INSERT ... VALUES ('Login');`|**10:00:00**|
|**2. Storage**|Database|`UTC`|MySQL converts EST to UTC|**15:00:00** (UTC)|
|**3. Select**|London|`Europe/London`|`SELECT created_at ...`|**15:00:00**|


### Comparison: TIMESTAMP vs. DATETIME

If we had used `DATETIME` instead of `TIMESTAMP`, the results would be very different:

| Viewport          | `TIMESTAMP` Result                   | `DATETIME` Result                         |
| ----------------- | ------------------------------------ | ----------------------------------------- |
| **New York User** | 10:00 AM                             | 10:00 AM                                  |
| **London User**   | **03:00 PM**                         | **10:00 AM**                              |
| **Why?**          | It calculated the 5-hour difference. | It just saved the text "10:00" literally. |

# 5. YEAR

- **Format:** `YYYY` or `YY`
- **Description:** A very efficient 1-byte type used to store a year.
- **Parameters:** You can specify `YEAR(4)` for the full year (e.g., 2026) or `YEAR(2)` for the short version (e.g., 26).

# Summary

| **Type**      | **Format**            | **Internal Range**    | **Purpose**             |
| ------------- | --------------------- | --------------------- | ----------------------- |
| **DATE**      | `YYYY-MM-DD`          | 1000 to 9999          | Calendar Dates          |
| **TIME**      | `HH:MM:SS`            | **-838 to 838 Hours** | Durations / Intervals   |
| **DATETIME**  | `YYYY-MM-DD HH:MM:SS` | 1000 to 9999          | Specific fixed events   |
| **TIMESTAMP** | `YYYY-MM-DD HH:MM:SS` | 1970 to 2038          | Global transaction logs |
| **YEAR**      | `YYYY`                | `1901` to `2155`      | for historical events   |

