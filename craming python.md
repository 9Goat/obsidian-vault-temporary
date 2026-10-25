
# reading csv

```python
import pandas as pd

# Loading a CSV file with specific parsing rules
df = pd.read_csv(
    'student_data.csv', 
    sep=',',            # Specifies the delimiter (comma is default)
    header=0,           # Uses the first row (index 0) as column names
    usecols=['ID', 'Name', 'Grade'],  # Loads only these specific columns
    index_col='ID',     # Sets the 'ID' column as the DataFrame index
    nrows=100           # Only reads the first 100 rows of data
)
```

- **Note** the result will be in the format of a DataFrame

# describing the csv

```python
import pandas as pd

# Load our exam data
df = pd.read_csv('exam_results.csv')

# 1. Structural Overview
print(df.info())

# 2. Statistical Summary
print(df.describe())

# 3. Metadata Attributes (No Parentheses!)
print(df.shape)    # e.g., (100, 5) -> 100 rows, 5 columns
print(df.columns)  # e.g., Index(['Name', 'Math', 'Science'], dtype='object')
print(df.dtypes)   # Lists data types for each column
```

# indexing and selecting

- `.loc[]` is **label-based**: You must use the actual names of rows or columns.
- `.iloc[]` is **integer-position-based**: You must use numerical counts (starting at 0), completely ignoring what the labels are called.
- **`isin()`**: Filters rows by checking if column values match any element inside a provided list.
- **`query()`**: Filters rows using a clear, human-readable SQL-like expression string.
- **`filter()`**: Subsets a DataFrame's rows or columns by matching their explicit names (supports substring matching and regular expressions).
- **`select_dtypes()`**: Subsets columns by including or excluding specific data types (like `include='number'` or `exclude='object'`).

## loc

$$\text{df.loc[row\_labels, column\_labels]}$$


```python
import pandas as pd

data = {
    'Continent': ['Europe', 'Asia', 'North America', 'Asia'],
    'Population_M': [67.8, 1412.0, 333.3, 125.7],
    'GDP_B': [2937, 17730, 25440, 4231]
}
# Setting the country names as our Row Index
df = pd.DataFrame(data, index=['France', 'China', 'USA', 'Japan'])

# What is the population of China?
china_pop = df.loc['China', 'Population_M']
print(china_pop)  # Output: 1412.0

# Get data for France and Japan, but only show their Continent and GDP
sub_df = df.loc[['France', 'Japan'], ['Continent', 'GDP_B']]
print(sub_df)

# Output:
#         Continent  GDP_B
# France     Europe   2937
# Japan        Asia   4231

# Slice from China down through USA (Includes China, USA, AND everything in between)
print(df.loc['China':'USA', :])

# Output:
#       Continent  Population_M  GDP_B
# China      Asia        1412.0  17730
# USA   North Amer        333.3  25440

# Get all countries, but only columns from Continent through Population_M
print(df.loc[:, 'Continent':'Population_M'])

# Output:
#        Continent  Population_M
# France    Europe          67.8
# China       Asia        1412.0
# USA   North Amer          333.3
# Japan       Asia          125.7
```

## iloc

exactly like loc except that it works with the index of the columns and rows instead of their name

$$\text{df.iloc[row\_positions, column\_positions]}$$

## isin

isin is used to only accept rows with the values included in the isin function

```python
import pandas as pd

data = {
    'Product': ['Laptop', 'Banana', 'Desk Chair', 'Apple', 'Keyboard'],
    'Department': ['Electronics', 'Grocery', 'Furniture', 'Grocery', 'Electronics'],
    'Price': [1200, 1.5, 150, 0.8, 75]
}
df = pd.DataFrame(data)

# Define our list of acceptable values
target_departments = ['Electronics', 'Furniture']

# Create the mask using .isin()
mask = df['Department'].isin(target_departments)
print("The Boolean Mask:")
print(mask)

print("\nFiltered DataFrame:")
# Apply the mask to get our rows
filtered_df = df[mask]
print(filtered_df)

The Boolean Mask:
0     True  (Electronics)
1    False  (Grocery)
2     True  (Furniture)
3    False  (Grocery)
4     True  (Electronics)
Name: Department, dtype: bool

Filtered DataFrame:
      Product   Department  Price
0      Laptop  Electronics   1200
2  Desk Chair    Furniture    150
4    Keyboard  Electronics     75
```

# coditional slicing

```python
import pandas as pd

df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie', 'David'],
    'Age': [20, 23, 21, 24]
})

# Let's look at the raw condition by itself:
mask = df['Age'] > 21
print(mask)

# Output:
# 0    False  (Alice is 20)
# 1     True  (Bob is 23)
# 2    False  (Charlie is 21)
# 3     True  (David is 24)
# Name: Age, dtype: bool

# Pass the True/False mask into the DataFrame
filtered_df = df[df['Age'] > 21]
print(filtered_df)

# Output: Only rows where the mask was True!
#    Name  Age
# 1   Bob   23
# 3 David   24
# Note how the index labels (1 and 3) stay exactly as they were originally.

# Filter rows where Age > 21, but only output the 'Name' column
names_only = df.loc[df['Age'] > 21, 'Name']
print(names_only)

# Output:
# 1      Bob
# 3    David
# Name: Name, dtype: object
```

- **Note** we use the following operators to combine conditions:
	- Use **`&`** instead of `and`
	- Use **`|`** instead of `or`
	- Use **`~`** instead of `not`


# SQL methods

## Where

```python
import pandas as pd

df = pd.DataFrame({
    'Student': ['Alex', 'Blake', 'Charlie'],
    'Score': [85, 55, 92]
})

# Condition: Keep scores that are >= 60. Replace failing scores with 'Fail'.
df['Exam_Status'] = df['Score'].where(df['Score'] >= 60, other='Fail')

print(df)

Student  Score Exam_Status
0     Alex     85          85
1    Blake     55        Fail
2  Charlie     92          92
```


##  group by

```python
import pandas as pd

df = pd.DataFrame({
    'City': ['NYC', 'LA', 'NYC', 'LA', 'NYC'],
    'Sales': [100, 150, 200, 50, 300]
})

# Group the rows by 'City' and calculate the total (sum) sales for each city
city_totals = df.groupby('City')['Sales'].sum().reset_index()

print(city_totals)

City  Sales
0   LA    200
1  NYC    600
```

## sort values

```python
import pandas as pd

df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie', 'David'],
    'Grade': ['B', 'A', 'A', 'C'],
    'Score': [85, 95, 92, 70]
})

# Sort primarily by Grade (A to Z), then break ties by Score (highest to lowest)
sorted_multi_df = df.sort_values(
    by=['Grade', 'Score'], 
    ascending=[True, False]
)
print(sorted_multi_df)

# Output:
#       Name Grade  Score
# 1      Bob     A     95   <-- Bob comes first because 95 > 92
# 2  Charlie     A     92
# 0    Alice     B     85
# 3    David     C     70
```

##  sort index

```python
import pandas as pd

# Let's create a DataFrame where the index and scores are completely scrambled
df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Score': [95, 70, 88]
}, index=[2, 0, 1])

by_val = df.sort_values(by='Score')
print(by_val)

Name  Score
0     Bob     70
1 Charlie     88
2   Alice     95
```

## aggregate functions

```python
import numpy as np
import pandas as pd

df = pd.DataFrame({
    'Product': ['Item_A', 'Item_B', 'Item_C', 'Item_A'],
    'Price': [10.0, 25.0, np.nan, 15.0]  # Item_C has a missing price!
})

total_revenue = df['Price'].sum()
print(total_revenue)  # Output: 50.0  (10.0 + 25.0 + 15.0)

price_count = df['Price'].count()
total_rows = len(df)

print(f"Count function: {price_count}")  # Output: 3 (Item_C is skipped!)
print(f"Total row count: {total_rows}")  # Output: 4

cheapest = df['Price'].min()
priciest = df['Price'].max()

print(f"Min: {cheapest}, Max: {priciest}")  # Output: Min: 10.0, Max: 25.0

average_price = df['Price'].mean()
print(average_price)  # Output: 16.666... (Calculated as 50.0 divided by 3, NOT 4!)
```

## drop

```python
import pandas as pd

df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [20, 22, 21],
    'Unnecessary_Col': [100, 200, 300]
}, index=['Row_0', 'Row_1', 'Row_2'])

# A. Dropping a Column (axis=1)
# Let's clean up our dataset by removing 'Unnecessary_Col'
cleaned_df = df.drop('Unnecessary_Col', axis=1)
print("After dropping column:")
print(cleaned_df)

print("\n" + "="*30 + "\n")

# B. Dropping a Row by Index Label (axis=0)
# Let's remove 'Row_1' (Bob's row)
fewer_rows_df = df.drop('Row_1', axis=0)
print("After dropping row:")
print(fewer_rows_df)
```

##  insert

```python
import pandas as pd

df = pd.DataFrame({
    'Name': ['Alice', 'Bob'],
    'GPA': [3.9, 3.2]
})

# Let's insert an 'ID' column at position 0 (the absolute far left column)
student_ids = [101, 102]

# DO NOT write: df = df.insert(...) -> it modifies 'df' directly!
df.insert(loc=0, column='ID', value=student_ids)

print("After inserting 'ID' column at position 0:")
print(df)
```
# unique methods

 - unique works on a single column
 - By default, `nunique()` completely ignores missing (`NaN`) values. If you want to count `NaN` as a unique category, pass `dropna=False`.

```python
import pandas as pd

df = pd.DataFrame({
    'Product': ['Laptop', 'Mouse', 'Laptop', 'Keyboard', 'Mouse', 'Laptop'],
    'Quantity': [1, 2, 1, 1, 5, 2]
})

# Get a list of the unique products sold
unique_products = df['Product'].unique()
print(unique_products)

# Output:
# ['Laptop' 'Mouse' 'Keyboard']

# How many different types of products did we sell?
product_count = df['Product'].nunique()
print(product_count)

# Output: 
# 3

# How many transactions did each product have?
frequency = df['Product'].value_counts()
print(frequency)

# Output:
# Laptop      3
# Mouse       2
# Keyboard    1
# Name: Product, dtype: int64
```

#  null methods

```python
import numpy as np
import pandas as pd

# Creating a messy dataset for our examples
data = {
    'Name': ['Alex', 'Blake', 'Charlie', 'Taylor'],
    'Section': ['Section_A', None, 'Section_B', 'Section_A'],
    'Midterm': [85.0, np.nan, 92.0, np.nan],
    'Final': [90.0, np.nan, np.nan, np.nan]
}
df = pd.DataFrame(data)

# Scan and count the missing numbers per column
print(df.isna().sum())

Name       0
Section    1
Midterm    2
Final      3
dtype: int64

# Keep only rows where the 'Midterm' score is valid and filled in
valid_midterms = df[df['Midterm'].notna()]
print(valid_midterms)

Name    Section  Midterm  Final
0     Alex  Section_A     85.0   90.0
2  Charlie  Section_B     92.0    NaN

# Example A: Drop rows ONLY if they are missing a 'Section'
clean_sections = df.dropna(subset=['Section'])
print("Dropped rows missing a section:")
print(clean_sections)

print("\n" + "="*45 + "\n")

# Example B: Drop entire columns if they contain ANY null values
clean_columns = df.dropna(axis=1)
print("Dropped columns containing any nulls:")
print(clean_columns)

Dropped rows missing a section:
      Name    Section  Midterm  Final
0     Alex  Section_A     85.0   90.0
2  Charlie  Section_B     92.0    NaN
3   Taylor  Section_A      NaN    NaN

=============================================

Dropped columns containing any nulls:
     Name
0    Alex
1   Blake
2 Charlie
3  Taylor

# Calculate the average score for the Midterm exam (ignoring the NaNs)
midterm_avg = df['Midterm'].mean()  # (85 + 92) / 2 = 88.5

# Fill the missing midterm slots with that average number
df['Midterm'] = df['Midterm'].fillna(midterm_avg)

# Fill any categorical missing text slots with a placeholder string
df['Section'] = df['Section'].fillna('Unknown')

print(df)

Name    Section  Midterm  Final
0     Alex  Section_A     85.0   90.0
1   Blake    Unknown     88.5    NaN   <-- Filled with Mean and 'Unknown'
2  Charlie  Section_B     92.0    NaN
3   Taylor  Section_A     88.5    NaN   <-- Filled with Mean
```


# customisations

- `plt.title('Text')` — The Heading
- `plt.xlabel('Text')` & `plt.ylabel('Text')` — Axis Labels 
- `plt.legend()` — The Key Map
- `plt.figure(figsize=(w, h))` creates a new figure
- `plt.show()` shows the figure 

# plot

```python
import matplotlib.pyplot as plt
import numpy as np

# Apply a professional visual style theme from Page 10
plt.style.use('ggplot')  # 

# Define data arrays tracking a moving trend line
days = np.array([1, 2, 3, 4, 5])
temperatures = np.array([22, 24, 21, 28, 25])

# Draw the line with custom nodes, custom hotpink color, and thin line width
plt.plot(days, temperatures, marker='o', color='hotpink', linewidth=1.5, label='Daily Temp')

# Add context annotations using the custom tools we just covered
plt.title('Weekly Temperature Tracking')
plt.xlabel('Days of the Week')
plt.ylabel('Degrees Celsius')
plt.grid(True)
plt.legend()

# Render output
plt.show()
```

#  scatter

```python
import matplotlib.pyplot as plt
import numpy as np

# Apply a built-in clean visual style from page 11
plt.style.use('seaborn-v0_8-whitegrid') [cite: 452]

# Define mock test datasets
study_hours = np.array([2, 4, 5, 7, 8, 10, 11, 12, 3, 6])
exam_scores = np.array([55, 62, 65, 78, 82, 95, 91, 99, 58, 70])

# Plot the scatter graph using customized size, color, shape, and transparency
plt.scatter(study_hours, exam_scores, 
            s=120,             # Make dots bigger
            color='darkviolet',# Custom color theme
            marker='o',        # Filled circle points
            alpha=0.85)        # Soft transparency to trace overlapping grid locations

# Add structural context labels from the textbook guide
plt.title('Analysis of Study Time vs. Exam Success') [cite: 397]
plt.xlabel('Hours Studied') [cite: 397]
plt.ylabel('Exam Percentage Score (%)') [cite: 398]

# Turn on background helper grid guides
plt.grid(True)

# Render layout canvas
plt.show() [cite: 401]
```


# bar and barh

h is for horizontal the more you know

```python
import matplotlib.pyplot as plt
import numpy as np

# Apply the global clean whitegrid style from page 11
plt.style.use('seaborn-v0_8-whitegrid') [cite: 215]

# Define product tracking dataset
categories = np.array(['Tech', 'Clothing', 'Home', 'Toys'])
revenue = np.array([45, 30, 15, 60])

# Plot customized bars with structural arguments
plt.bar(categories, revenue, 
        color='salmon',      # Set explicit background color 
        edgecolor='black',   # Highlight borders cleanly 
        width=0.6)           # Make bars slightly narrower for readability

# Attach context annotations [cite: 160, 161]
plt.title('Department Quarterly Revenue Breakdowns') [cite: 160]
plt.xlabel('Store Departments') [cite: 160]
plt.ylabel('Sales Volume (in thousands)') [cite: 161]

# Turn on background helper grid lines
plt.grid(True)

# Render canvas layout
plt.show()
```

# pie chart

```python
import matplotlib.pyplot as plt
import numpy as np

# 1. Define proportional dataset 
market_shares = np.array([40, 30, 20, 10])
brand_names = ["Brand Alpha", "Brand Beta", "Brand Gamma", "Brand Delta"]


# 3. Define a clean color theme
custom_colors = ["deepskyblue", "lightgrey", "darkgrey", "whitesmoke"]

# 4. Generate the fully customized pie chart
plt.pie(market_shares, 
        labels=brand_names,          # Track slice identities
        autopct='%1.1f%%',           # Inject percentage tags inside slices
        colors=custom_colors)       # Apply our custom palette)         

# 5. Add a structural title heading
plt.title("Smartphone Market Share Breakdown")

# 6. Render canvas layout
plt.show()
```

# hist

```python
import matplotlib.pyplot as plt
import numpy as np

# 1. Define a targeted raw continuous numeric sequence
scores = [5, 10, 10, 20, 25, 30, 35, 30, 45, 50] [cite: 390]

# 2. Plot the histogram using custom bins, colors, and sharp edge separation
plt.hist(scores, 
         bins=9,              # Divide data range into 9 equal blocks [cite: 395, 392]
         color='salmon',      # Fill bins with salmon color theme 
         edgecolor='black')   # Highlight individual boundaries clearly [cite: 395, 394]

# 3. Add context annotations using structural labels [cite: 396]
plt.title("Distribution of Student Exam Scores") [cite: 397]
plt.xlabel("Score Intervals (Valeurs)") [cite: 397]
plt.ylabel("Student Count (Fréquence)") [cite: 398]

# 4. Control background grid visibility
plt.grid(True) # Set to False if you want to turn it off completely [cite: 400]

# 5. Render canvas layout
plt.show() [cite: 401]
```

