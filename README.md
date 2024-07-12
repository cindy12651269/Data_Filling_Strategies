# Data Filling Strategies

This section provides examples of filtering rows in a Pandas DataFrame based on various conditions using Python. The script showcases different techniques to manipulate and extract specific subsets of data from a DataFrame.

## Sample Code

```python
import numpy as np
import pandas as pd

raw_data = {'first_name': ['Jason', np.nan, 'Tina', 'Jake', 'Amy'],
            'last_name': ['Miller', np.nan, 'Ali', 'Milner', 'Cooze'],
            'age': [42, np.nan, 36, 24, 73],
            'sex': ['m', np.nan, 'f', 'm', 'f'],
            'preTestScore': [4, np.nan, np.nan, 2, 3],
            'postTestScore': [25, np.nan, np.nan, 62, 70]}

df = pd.DataFrame(raw_data, columns=['first_name', 'last_name', 'age', 'sex', 'preTestScore', 'postTestScore'])

# 1. Drop missing observations
df_drop_na = df.dropna()
print("Drop missing observations:")
print(df_drop_na)

# 2. Drop rows where all cells in that row is NA
df_drop_all_na = df.dropna(how="all") 
print("\nDrop rows where all cells in that row is NA:")
print(df_drop_all_na)

# 3. Create a new column full of missing values
df['new_column'] = np.nan
print("\nCreate a new column full of missing values:")
print(df)

# 4. Fill in missing data with zeros
df_fill_zero = df.fillna(0)
print("\nFill in missing data with zeros:")
print(df_fill_zero)

# 5. Fill in missing in preTestScore with the mean value of preTestScore
preTestScore_Mean = df['preTestScore'].mean()
df['preTestScore'].fillna(preTestScore_Mean, inplace= True)
print("\nFill in missing in preTestScore with the mean value of preTestScore:")
print(df)

# 6. Fill in missing in postTestScore with each sex’s mean value of postTestScore
df['postTestScore']= df.groupby('sex')['postTestScore'].transform(lambda x: x.fillna(x.mean()))
print("\nFill in missing in postTestScore with each sex’s mean value of postTestScore:")
print(df)

# 7. Select some rows but ignore the missing data points
selected_rows = df.loc[0:2, ['first_name', 'last_name', 'age']]
print("\nSelect some rows but ignore the missing data points:")
print(selected_rows)
