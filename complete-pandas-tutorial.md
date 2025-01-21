# Complete Pandas Tutorial: From Beginner to Advanced

## Table of Contents
- [Phase 1: Introduction to Pandas and Basic Operations](#phase1)
- [Phase 2: Data Selection, Filtering, and Advanced Operations](#phase2)
- [Phase 3: Working with Missing Data, Merging DataFrames, and Handling Time Series Data](#phase3)
- [Phase 4: Advanced Data Manipulation and Visualization](#phase4)

## Phase 1: Introduction to Pandas and Basic Operations {#phase1}

### What is Pandas?
Pandas is a powerful open-source Python library used for data manipulation and analysis. It provides data structures and functions that make working with structured data fast, easy, and expressive. The two primary data structures in Pandas are:

- Series: A one-dimensional array-like object
- DataFrame: A two-dimensional table-like structure

### Installing Pandas
```bash
pip install pandas
```

### Importing Pandas
```python
import pandas as pd
```

### 1. Pandas Series
A Series is a one-dimensional array that can hold any data type (integers, strings, floats, etc.).

#### Creating a Series
```python
import pandas as pd

# Create a Series from a list
data = [10, 20, 30, 40, 50]
series = pd.Series(data)
print(series)

# Output:
# 0    10
# 1    20
# 2    30
# 3    40
# 4    50
# dtype: int64
```

#### Custom Index
```python
series = pd.Series(data, index=['a', 'b', 'c', 'd', 'e'])
print(series)

# Output:
# a    10
# b    20
# c    30
# d    40
# e    50
# dtype: int64
```

### 2. Pandas DataFrame

#### Creating a DataFrame
```python
# Create a DataFrame from a dictionary
data = {
    'Name': ['Alice', 'Bob', 'Charlie', 'David'],
    'Age': [25, 30, 35, 40],
    'City': ['New York', 'Los Angeles', 'Chicago', 'Houston']
}

df = pd.DataFrame(data)
print(df)

# Output:
#       Name  Age         City
# 0    Alice   25     New York
# 1      Bob   30  Los Angeles
# 2  Charlie   35      Chicago
# 3    David   40      Houston
```

#### Custom Index
```python
df = pd.DataFrame(data, index=['a', 'b', 'c', 'd'])
```

#### Accessing Data
```python
# Access columns
print(df['Name'])

# Access rows using loc[] or iloc[]
print(df.loc['b'])
print(df.iloc[1])
```

### 3. Basic DataFrame Operations

#### Viewing Data
```python
# View first n rows
print(df.head(2))

# Shape of DataFrame
print(df.shape)  # Output: (4, 3)

# Data types
print(df.dtypes)

# Descriptive statistics
print(df.describe())
```

### 4. Adding and Deleting Columns
```python
# Adding a column
df['Salary'] = [70000, 80000, 90000, 100000]

# Deleting a column
df = df.drop('Salary', axis=1)
```

### 5. Handling Missing Data
```python
import numpy as np

# Create DataFrame with missing values
data = {
    'Name': ['Alice', 'Bob', np.nan, 'David'],
    'Age': [25, np.nan, 35, 40],
    'City': ['New York', 'Los Angeles', np.nan, 'Houston']
}

df = pd.DataFrame(data)

# Check for missing values
print(df.isnull())

# Drop missing values
df_cleaned = df.dropna()

# Fill missing values
df_filled = df.fillna('Unknown')
```

## Phase 2: Data Selection, Filtering, and Advanced Operations {#phase2}

### 1. Data Selection in DataFrames

#### Selecting Columns
```python
# Select a single column
print(df['Name'])

# Select multiple columns
print(df[['Name', 'City']])
```

#### Selecting Rows
```python
# Select row by label
print(df.loc[1])

# Select row by integer position
print(df.iloc[1])
```

### 2. Filtering Data
```python
# Filter rows where Age is greater than 30
filtered_df = df[df['Age'] > 30]

# Multiple conditions
filtered_df = df[(df['Age'] > 30) & (df['City'] == 'Houston')]

# Using query() method
filtered_df = df.query('Age > 30 and City == "Houston"')
```

### 3. Adding and Modifying Data
```python
# Add new column
df['Salary'] = [70000, 80000, 90000, 100000]

# Modify column
df['Salary'] = df['Salary'] * 1.1

# Apply function to column
df['Name'] = df['Name'].apply(lambda x: x.upper())
```

### 4. Sorting Data
```python
# Sort by Age in ascending order
sorted_df = df.sort_values('Age')

# Sort in descending order
sorted_df = df.sort_values('Age', ascending=False)

# Sort by multiple columns
sorted_df = df.sort_values(['City', 'Age'])
```

### 5. Grouping Data
```python
# Group by City and calculate mean
grouped_df = df.groupby('City').agg({'Age': 'mean', 'Salary': 'mean'})

# Multiple aggregations
grouped_df = df.groupby('City').agg({'Age': ['mean', 'max'], 'Salary': 'sum'})
```

### 6. Applying Functions
```python
# Calculate Age squared
df['Age_Squared'] = df['Age'].apply(lambda x: x ** 2)

# Convert strings to lowercase
df_lower = df.applymap(lambda x: x.lower() if isinstance(x, str) else x)
```

## Phase 3: Working with Missing Data, Merging DataFrames, and Time Series Data {#phase3}

### 1. Working with Missing Data
```python
# Detect missing values
print(df.isnull())

# Drop missing values
df_cleaned = df.dropna()

# Fill missing values
df_filled = df.fillna('Unknown')
```

### 2. Merging DataFrames
```python
# Create two DataFrames
df1 = pd.DataFrame({
    'ID': [1, 2, 3],
    'Name': ['Alice', 'Bob', 'Charlie']
})

df2 = pd.DataFrame({
    'ID': [2, 3, 4],
    'City': ['New York', 'Los Angeles', 'Chicago']
})

# Merge DataFrames
merged_df = pd.merge(df1, df2, on='ID')

# Concatenate DataFrames
concatenated_df = pd.concat([df1, df2], axis=0)

# Join DataFrames
joined_df = df1.join(df2, how='inner')
```

### 3. Handling Time Series Data
```python
# Create date range
dates = pd.date_range('2023-10-01', periods=5, freq='D')

# Create DataFrame with dates
df = pd.DataFrame({
    'Value': [10, 20, 30, 40, 50]
}, index=dates)

# Resample time series data
weekly_df = df.resample('W').mean()

# Shift data
df_shifted = df.shift(1)
```

### 4. Handling Duplicates
```python
# Detect duplicates
print(df.duplicated())

# Remove duplicates
df_cleaned = df.drop_duplicates()
```

## Phase 4: Advanced Data Manipulation and Visualization {#phase4}

### 1. Pivoting DataFrames
```python
# Create pivot table
pivot_df = df.pivot_table(
    index='Date',
    columns='City',
    values='Temperature'
)
```

### 2. Melting DataFrames
```python
# Melt DataFrame
melted_df = df.melt(
    id_vars=['Date', 'City'],
    value_vars=['Temperature', 'Humidity'],
    var_name='Metric',
    value_name='Value'
)
```

### 3. Multi-Index DataFrames
```python
# Create multi-index DataFrame
arrays = [
    ['New York', 'New York', 'Los Angeles', 'Los Angeles'],
    ['Day 1', 'Day 2', 'Day 1', 'Day 2']
]

index = pd.MultiIndex.from_arrays(arrays, names=('City', 'Date'))
df = pd.DataFrame({
    'Temperature': [70, 72, 75, 78],
    'Humidity': [50, 52, 55, 58]
}, index=index)
```

### 4. Data Visualization
```python
import matplotlib.pyplot as plt

# Line plot
df.plot(x='Year', y='Sales', kind='line', title='Sales Over Time')

# Bar plot
df.plot(x='Year', y='Sales', kind='bar', title='Sales Over Time')

# Histogram
df['Sales'].plot(kind='hist', title='Sales Distribution')

# Scatter plot
df.plot(x='Year', y='Sales', kind='scatter', title='Sales vs Year')
```

### 5. Advanced Visualization with Seaborn
```python
import seaborn as sns

# Create heatmap
corr = df.corr()
sns.heatmap(corr, annot=True, cmap='coolwarm')

# Create pair plot
sns.pairplot(df)
```

## Best Practices

1. Always create a copy of the DataFrame before modifications
2. Use appropriate data types for memory optimization
3. Chain operations efficiently
4. Set proper indexes for better performance
5. Handle missing data appropriately for your specific use case
6. Document your code and transformations
7. Use descriptive variable names
8. Regularly check data types and shape
9. Back up important data before transformations
10. Use proper error handling when working with data

## Common Pitfalls to Avoid

1. Modifying data without making a copy
2. Ignoring data types
3. Not handling missing values properly
4. Using inefficient operations on large datasets
5. Not checking for duplicates
6. Ignoring index alignment
