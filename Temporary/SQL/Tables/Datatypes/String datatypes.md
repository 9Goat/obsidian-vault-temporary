in strings there are 4 main types of strings which are the following:

- non binary strings
- binary strings
- blob texts
- sets/groups

# Non binary strings

are the most common datatypes in sql  ,These are used for standard text (names, paragraphs, codes). They follow "Character Sets" (like UTF-8) to understand how to display letters and symbols.

| **Data Type**  | **Parameters** | **Max Length (In Characters)** | **Description**                                                       |
| -------------- | -------------- | ------------------------------ | --------------------------------------------------------------------- |
| **CHAR**       | `(M)`          | 255                            | Fixed-length string. Shorter values are padded with spaces.           |
| **VARCHAR**    | `(M)`          | 65,535                         | Variable-length string. Only uses space for actual characters stored. |
| **TINYTEXT**   | None           | 255                            | A very small non-binary string.                                       |
| **TEXT**       | None           | 65,535                         | A small to medium non-binary string.                                  |
| **MEDIUMTEXT** | None           | 16,777,215                     | A medium-sized non-binary string (up to 16 MB).                       |
| **LONGTEXT**   | None           | 4,294,967,295                  | A large non-binary string (up to 4 GB).                               |

- for **`CHAR`** and **`VARCHAR`** the length is specified by the parameter `(M)`, which defines the maximum number of characters that can be stored.
	- For **`CHAR`** if you specify a length of 5 and you store a string of length 3, it will be padded with 2 spaces to meet the defined length of 5. **EXAMPLE**: CHAR(5) -> `  lol`
	- For **`VARCHAR`** the length is also specified by the parameter `(M)`, but it doesn't pad the string with spaces if it's shorter than the defined length. Instead, it stores the string as is, using only the space required for the actual characters.

| **Feature**     | **CHAR** | **VARCHAR** |
| --------------- | -------- | ----------- |
| **Minimum (M)** | **0**    | **0**       |
| **Maximum (M)** | **255**  | **65,535**  |

# Binary strings

These do not use character sets. They store raw bytes (0s and 1s) and are used for data that humans aren't meant to read directly, such as encrypted keys or compressed files. (they are useful for bit for bit comparison which is essential for things like encrypted password)

| **Data Type** | **Parameters** | **Max Length (In Bytes)** | **Description**                  |
| ------------- | -------------- | ------------------------- | -------------------------------- |
| **BINARY**    | `(M)`          | 255                       | A fixed-length binary string.    |
| **VARBINARY** | `(M)`          | 65,535                    | A variable-length binary string. |

# BLOBS

These are specialized versions of binary strings designed to hold large files like images, audio, or PDF documents.

|**Data Type**|**Parameters**|**Max Length (In Bytes)**|**Description**|
|---|---|---|---|
|**TINYBLOB**|None|255|A very small binary large object.|
|**BLOB**|None|65,535|A small binary large object.|
|**MEDIUMBLOB**|None|16,777,215|A medium-sized binary large object.|
|**LONGBLOB**|None|4,294,967,295|A large binary large object.|

blobs dont store values in text but instead in binary format, so when we select them we get the same output as using **`BIT`** from [[Numerical datatypes]]

# Sets/Groups

These types allow you to define a specific list of permitted values.

| **Data Type** | **Parameters**    | **Max Members** | **Description**                                                           |
| ------------- | ----------------- | --------------- | ------------------------------------------------------------------------- |
| **ENUM**      | `('v1','v2',...)` | 65,535          | Each column value may be assigned exactly **one** member from the list.   |
| **SET**       | `('v1','v2',...)` | 64              | Each column value may be assigned **zero or more** members from the list. |

## Example

in set we can store zero of multiple values from the predefined list of values inside that set

```SQL
CREATE TABLE profiles (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50),
    interests SET('Sports', 'Music', 'Tech', 'Travel')
);
```

|**Case**|**SQL Command**|**Result in Column**|
|---|---|---|
|**Zero Values**|`INSERT ... VALUES ('User1', '');`|`''` (Empty String)|
|**One Value**|`INSERT ... VALUES ('User2', 'Tech');`|`'Tech'`|
|**Multiple Values**|`INSERT ... VALUES ('User3', 'Music,Travel');`|`'Music,Travel'`|
|**Out of Order**|`INSERT ... VALUES ('User4', 'Travel,Sports');`|`'Sports,Travel'` (Reordered by MySQL)|

