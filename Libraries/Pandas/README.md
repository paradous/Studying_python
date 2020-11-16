# Pandas basics

### Basic methods:

```Python
df.head(n) # Show the first n-rows of a DataFrame.
df.tail(n) # Show the last n-rows of a DataFrame.


df.shape # Get the dimention (x, y) of a Dataframe (like Numpy).
df.columns.tolist() # Get a list of the Dataframe's columns.


# Summary statistics of the Series/Dataframe provided.
df.describe()
# count: Count number of non-NA/null observations.
# max: Maximum of the values in the object.
# min: Minimum of the values in the object.
# mean: Mean of the values.
# std: Standard deviation of the observations.

# The following return the same as df.describe, and can be applied on all dataframe, or on a column:
df.max()
df['column'].max()
df['value'].idxmax() # Return the index of the max value in a column.

df.min()
df['column'].min()
df['column'].idxmin() # Return the index of the min value in a column.

df.mean()
df['column'].mean()

# Useful: Shows how many times each item appears in the column.
df['column'].value_counts()

# Return the amount of non-null observations
df.count()

# To know how a dataframe is indexed:
df.index

# To know the datatype of each columns:
df.dtype
df.info()

# To know if a Series ( a row or column) have unique values:
df['column'].is_unique # Boolean
```

### Retrieving the data:

```Python
# From local storage:
df = pd.read_csv('/content/drive/My Drive/datas/en.openfoodfacts.org.products.tsv', sep='\t')

# From web:
df = pd.read_csv(url, sep = '\t')
```

![https://shanelynnwebsite-mid9n9g1q9y8tt.netdna-ssl.com/wp-content/uploads/2016/10/Pandas-selections-and-indexing-768x549.png](https://shanelynnwebsite-mid9n9g1q9y8tt.netdna-ssl.com/wp-content/uploads/2016/10/Pandas-selections-and-indexing-768x549.png)

### Accessing values, on a int-indexed array - iloc:

**iloc** is definitely one of the most important functions. Generally, you want to use it whenever you have the integer index of a certain row (or a list of integer indexes) that you want to access.

```Python
df.iloc[144] # Return the row @ index 144.

# Using basic method to access specific values:

# We retrieve the row index of 'column1's maximum value, to access its corresponding 'column2'.
df.iloc[ [df['column1'].idxmax()] ]['column2'] 
# Note: the type of returned value is: "pandas.core.series.Series".

# But the following return type is "pandas.core.frame.DataFrame".
df.iloc[[df['column'].idxmax()]]
```

### Accessong values, on a string/boolean-indexed array - loc

**loc** is a "Purely label-location based indexer for selection by label". See this [useful documentation with examples](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.loc.html).

But **loc** can also manage integers !

```Python
# Same as iloc, but shorter.
df.loc[df['column1'].idxmax(), 'column2'] 

# Even shorter, with "at".
df.at[df['column1'].idxmax(), 'column2']

# Or simply:
df.loc['row', 'column'] 
```

### Manipulating data

#### Sorting
With **df.sort_values()**: [See doc here](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.sort_values.html).

```Python
# By default, sort_value sort ascending:
df.sort_values('value')
```

#### Filtering the rows conditionally:
An easy and powerfull tool of pandas: filtering your dataframe, with pythonic assesments:

```Python
df[df['value'] > 150] # Get a copy of the df with all rows, where 'value' column is greater than 150
df[(df['value'] > 150) & (df['value'] < 200)] # More complex filter
```

#### Groupby:
Full explanation: https://medium.com/analytics-vidhya/pandas-groupby-take-the-most-from-your-data-1303a4d41389

In a table, let's imagine we have a column "Name" and a column "score".
 - Some names appear more than one time.
 - groupby('name')['score'].sum() will "merge" the row with same name together, and apply a sum() bewteen all score of a same name.

![https://i.imgur.com/Jw6Ghy3.png](https://i.imgur.com/Jw6Ghy3.png)

### Accessing slice of Dataframe

#### By iteration

```Python
for index, row in df.iterrows()
```

#### With bracket indexing:

```Python

# Extracting two columns:
df[['col1', 'col2']].head()

# Same with loc:
df.loc[:, ['Wscore', 'Lscore']].head()

# Extracing row with slicing:
df[0:3]
df.iloc[0:3,:]
```
