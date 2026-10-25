there are 3 man types of numerical numbers in sql which are:

- integers
- float numbers
- numbers that hold a sequence of 1 and 0s

| **Name (Syntax)** | **What it's for**                                   | **Specific Maximum Range (Signed)**                                          |
| ----------------- | --------------------------------------------------- | ---------------------------------------------------------------------------- |
| **TINYINT(M)**    | **Flags/Small counts:** Best for "Yes/No" or age.   | **127**                                                                      |
| **SMALLINT(M)**   | **Small IDs:** Good for small inventories.          | **32,767**                                                                   |
| **MEDIUMINT(M)**  | **Mid-sized Data:** Use for city-sized populations. | **8,388,607**                                                                |
| **INT(M)**        | **The Standard:** Use for most IDs and counts.      | **2,147,483,647** (~2.1 Billion)                                             |
| **BIGINT(M)**     | **Massive Data:** Use for global scales.            | **9,223,372,036,854,775,807** (~9.2 Quintillion)                             |
| **DECIMAL(P, D)** | **Exact Money:** No rounding errors.                | **$10^{65} - 1$** (Up to 65 total digits)                                    |
| **FLOAT(P, D)**   | **Fast Decimals:** Approximate scientific data.     | **$3.402823466 \times 10^{38}$** (340 Undecillion)                           |
| **DOUBLE(P, D)**  | **Precise Decimals:** High-stakes scientific data.  | **$1.7976931348623157 \times 10^{308}$** (Nearly infinite for practical use) |
| **BIT(M)**        | **Binary Flags:** Stores multiple bits (0s and 1s). | **$2^{64} - 1$** (If using 64 bits)                                          |

# Integers

are simple whole numbers, either positive, negative, or zero, and they differ in size:

- **`TINYINT`**: **127**
- **`SMALLINT`**: **32,767**
- **`MEDIUMINT`**: **8,388,607**
- **`INT`**: **2,147,483,647** (~2.1 Billion)
- **`BIGINT`**: **9,223,372,036,854,775,807** (~9.2 Quintillion)

For all integers, **M** parameter stands for **Maximum Display Width**.meaning if you have a parameter of 3 and the number if smaller than 100, it will be displayed with leading zeros,otherwise if the number is larger it will be displayed normally (those parameters are **OPTIONAL** and can be omitted)

| **Column Type** | **Without ZEROFILL** | **With ZEROFILL** |
| --------------- | -------------------- | ----------------- |
| **INT(3)**      | `5`                  | `005`             |
| **INT(10)**     | `5`                  | `0000000005`      |
## Example

```SQL
CREATE TABLE display_test (
    small_id INT(3) ZEROFILL,
    large_val INT(3)
);

INSERT INTO display_test (small_id, large_val) 
VALUES (5, 5), (123, 123), (100000, 100000);

SELECT * FROM display_test;
```

**RESULT**

|**small_id (INT(3))**|**large_val (INT(3))**|**Explanation**|
|---|---|---|
|**005**|5|Padded with two zeros because it's smaller than 3.|
|**123**|123|Fits exactly, so no padding needed.|
|**100000**|100000|**Not truncated!** It breaks the "3" limit but displays fully.|

# Float numbers

there are 3 datatypes that concern the float numbers which are :

- **`DECIMAL (P, D)`** :
	- **Parameter P (Precision):** The maximum total number of digits allowed (both before and after the decimal). The maximum value is **65**.
	- **Parameter D (Scale):** The number of digits to the right of the decimal point. The maximum value is **30**.
	- **Example:** `DECIMAL(5, 2)` can store a range from `-999.99` to `999.99`.
- **`FLOAT(P, D)`**:
	- **Parameter P (Precision):** The total number of digits.
	- **Parameter D (Scale):** The number of digits after the decimal point.
	- **Max Range:** Approximately ±3.4×$10^{38}$.
- **`DOUBLE(P, D)`**:
	- **Parameter P (Precision):** The total number of digits.
	- **Parameter D (Scale):** The number of digits after the decimal point.
	- **Max Range:** Approximately ±1.8×$10^{308}$.

## what happens when we omit the parameters

| **Syntax**    | **Becomes...**   | **Result of inserting 10.55**      |
| ------------- | ---------------- | ---------------------------------- |
| **`DECIMAL`** | `DECIMAL(10, 0)` | **`11`** (Rounded to whole number) |
| **`FLOAT`**   | Hardware limit   | **`10.55`** (Stored accurately)    |
| **`DOUBLE`**  | Hardware limit   | **`10.55`** (Stored accurately)    |

# Binary sequences

bit is the only datatype in this  category and it is used to store numbers in a binary counter.

- **The Parameter (M)**: This defines exactly how many bits you want to store in the column.
- **Possible Range**: You can set **M** from **1 to 64**.
- **Default**: If you just write `BIT` without a number, it defaults to **`BIT(1)`**, which holds a single bit.

## Examples

```SQL
CREATE TABLE user_settings (
    id INT AUTO_INCREMENT PRIMARY KEY,
    -- 4 bits representing: [Email, SMS, DarkMode, IsAdmin]
    flags BIT(4)
);
```

```SQL
INSERT INTO table_name (bit_column) VALUES (5);       -- Decimal
INSERT INTO table_name (bit_column) VALUES (b'0101'); -- Binary Literal
INSERT INTO table_name (bit_column) VALUES (0x5);     -- Hexadecimal
```

