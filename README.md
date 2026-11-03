# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output
# Data_set.csv:
```
import pandas as pd
import numpy as np
df = pd.read_csv("Data_set.csv")
print("\nOriginal Data:\n", df.head(10))
print("\nMissing values:\n", df.isnull().sum())
clean = df.copy()
for col in clean.select_dtypes(include="number").columns:
    clean[col] = clean[col].fillna(clean[col].median())
for col in clean.select_dtypes(include="object").columns:
    if not clean[col].mode().empty:
        clean[col] = clean[col].fillna(clean[col].mode()[0])
print("\nMissing values after cleaning:\n", clean.isnull().sum())
print("\nCleaned Data:\n", clean.head(10))
clean.to_csv("Data_set_cleaned.csv", index=False)
print("\nSaved Data_set_cleaned.csv")
```
<img width="461" height="722" alt="image" src="https://github.com/user-attachments/assets/09e59866-b7a0-4ad3-90e6-3e7db876087e" />

# SAMPLEIDS.csv:
```
import pandas as pd
import numpy as np

df = pd.read_csv("SAMPLEIDS.csv")

print("\nOriginal Data:\n", df.head(10))
print("\nDuplicate rows:", df.duplicated().sum())

clean = df.drop_duplicates().copy()
for col in clean.select_dtypes(include="object").columns:
    clean[col] = clean[col].str.strip()
    print("\nUnique values in", col)
    print(clean[col].unique())

print("\nDuplicate rows after removal:", clean.duplicated().sum())
print("\nCleaned Data:\n", clean.head(10))

clean.to_csv("SAMPLEIDS_cleaned.csv", index=False)
print("\nSaved SAMPLEIDS_cleaned.csv")
```
<img width="433" height="703" alt="image" src="https://github.com/user-attachments/assets/90660acd-f3d9-4f5e-ad1f-fd4cc7999a6e" />

# heights.csv:
```
import pandas as pd
import numpy as np
from scipy import stats
import matplotlib.pyplot as plt

df = pd.read_csv("heights.csv")

print("\nOriginal Data:\n", df.head(10))

for col in df.select_dtypes(include="number").columns:

    values = df[col].dropna()

    if values.empty:
        continue

    q1 = values.quantile(0.25)
    q3 = values.quantile(0.75)
    iqr = q3 - q1

    lower = q1 - 1.5 * iqr
    upper = q3 + 1.5 * iqr

    outliers = values[(values < lower) | (values > upper)]

    print("\nIQR results for", col)
    print("Lower limit:", lower)
    print("Upper limit:", upper)
    print("Unusual measurements:\n", outliers)

for col in df.select_dtypes(include="number").columns:
    plt.figure()
    plt.boxplot(df[col].dropna())
    plt.title("Unusual measurements in " + col)
    plt.ylabel(col)
    plt.show()
```
   <img width="937" height="760" alt="image" src="https://github.com/user-attachments/assets/894ff67f-7a88-4256-bdfd-5b16ee6d2dcc" />

# iris.csv:
```
import pandas as pd
import numpy as np
from scipy import stats
df = pd.read_csv("iris.csv")

print("\nOriginal Data:\n", df.head(10))


for col in df.select_dtypes(include="number").columns:

    values = df[col].dropna()

    if values.empty:
        continue

    q1 = values.quantile(0.25)
    q3 = values.quantile(0.75)
    iqr = q3 - q1

    lower = q1 - 1.5 * iqr
    upper = q3 + 1.5 * iqr

    outliers = values[(values < lower) | (values > upper)]

    print("\nIQR outliers in", col)
    print(outliers if not outliers.empty else "None")

# STEP 3: Z-SCORE OUTLIER DETECTION
for col in df.select_dtypes(include="number").columns:

    values = df[col].dropna()

    if len(values) < 2:
        continue

    z = np.abs(stats.zscore(values))
    outliers = values[z > 3]

    print("\nZ-score outliers in", col)
    print(outliers if not outliers.empty else "None")
```
   <img width="735" height="688" alt="image" src="https://github.com/user-attachments/assets/02c89519-e171-4830-b4a9-16af143a36f8" />

# loan_data.csv:
```
import pandas as pd
import numpy as np
from scipy import stats
df = pd.read_csv("loan_data.csv")

print("\nOriginal Data:\n", df.head(10))


for col in df.select_dtypes(include="number").columns:

    values = df[col].dropna()

    if values.empty:
        continue

    q1 = values.quantile(0.25)
    q3 = values.quantile(0.75)
    iqr = q3 - q1

    lower = q1 - 1.5 * iqr
    upper = q3 + 1.5 * iqr

    outliers = values[(values < lower) | (values > upper)]

    print("\nIQR outliers in", col)
    print(outliers if not outliers.empty else "None")

# STEP 3: Z-SCORE OUTLIER DETECTION
for col in df.select_dtypes(include="number").columns:

    values = df[col].dropna()

    if len(values) < 2:
        continue

    z = np.abs(stats.zscore(values))
    outliers = values[z > 3]

    print("\nZ-score outliers in", col)
    print(outliers if not outliers.empty else "None")
```
  <img width="366" height="862" alt="image" src="https://github.com/user-attachments/assets/4318ede6-3e46-4deb-a3c1-88ecf53632c1" />

# interpretation:

      Thus, the data cleaning process was successfully performed by reading the datasets, 
      analyzing their information, handling missing values, removing duplicate records,
      and identifying outliers using the IQR and Z-score methods. The cleaned datasets were 
      saved into separate CSV files, making the data more accurate, consistent, and suitable 
      for further analysis.
      
# Result
          Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score
