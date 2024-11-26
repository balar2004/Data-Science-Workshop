# Data-Science-Workshop
# Data-Cleaning-and-Data-Analysis
# Aim:
To read the given perform data cleaning and data analysis.
# Algorithm:
1.Perform Data cleaning process wherever necessary
2.Implement Boxplot method to detect outliers
3.Implement IQR method to Remove Outliers
4.Implement Count plot method for univariate analysis
5.Implement DistPlot method for multivariate analysis

# Coding and Output:
Data cleaning process
```
import pandas as pd
data = pd.read_csv('supermarket.csv')

print("Missing values in each column:")
print(data.isnull().sum())

duplicate_rows = data.duplicated().sum()
print(f"\nNumber of duplicate rows: {duplicate_rows}")

if duplicate_rows > 0:
    data = data.drop_duplicates()
if data['Date'].dtype == 'object':
    data['Date'] = pd.to_datetime(data['Date'], format='%m/%d/%Y')

data = data.drop(columns=['Invoice ID'], axis=1)
print("\nData types after cleaning:")
print(data.dtypes)

print("\nCleaned data preview:")
print(data.head())
```
![383105611-f92a982c-12b0-4953-ae2a-48aada423ecb](https://github.com/user-attachments/assets/b3d3b768-5f00-41a3-bfc7-120ebd606bbe)

Boxplot:
```
import seaborn as sns
import matplotlib.pyplot as plt

# Plotting boxplots
plt.figure(figsize=(14, 6))

plt.subplot(1, 3, 1)
sns.boxplot(y=data['Unit price'])
plt.title('Boxplot of Unit Price')

plt.subplot(1, 3, 2)
sns.boxplot(y=data['Total'])
plt.title('Boxplot of Total')

plt.subplot(1, 3, 3)
sns.boxplot(y=data['Rating'])
plt.title('Boxplot of Rating')

plt.tight_layout()
plt.show()
```
![383105995-5a795da6-1a9f-40db-9a3c-5bcc972e51e3](https://github.com/user-attachments/assets/7e393998-2e32-4514-9e70-729e073833ab)

IQR method:
```
import pandas as pd

# Load your dataset
data = pd.read_csv('supermarket.csv')

# Function to remove outliers using IQR
def remove_outliers_iqr(df, column):
    Q1 = df[column].quantile(0.25)
    Q3 = df[column].quantile(0.75)
    IQR = Q3 - Q1
    lower_bound = Q1 - 1.5 * IQR
    upper_bound = Q3 + 1.5 * IQR
    return df[(df[column] >= lower_bound) & (df[column] <= upper_bound)]

# Removing outliers for 'Unit price', 'Total', and 'Rating'
for col in ['Unit price', 'Total', 'Rating']:
    data = remove_outliers_iqr(data, col)

# Display cleaned data shape
print(data.shape)
```
![383106558-8aea8342-9cf2-4da3-aafb-2702f6552f61](https://github.com/user-attachments/assets/a6326b00-b3a7-4201-9545-882ca1ab60d5)

Countolot Method
```
plt.figure(figsize=(8, 6))
sns.countplot(data=data, x='Product line')
plt.title('Count of Product Line')
plt.xticks(rotation=45)
plt.show()
```
![383106743-17f6d784-085b-4901-8a12-32631d220057](https://github.com/user-attachments/assets/85358c45-000c-49f1-a15b-e5886a45bc63)

Distplot Method
```
sns.jointplot(x=data['Total'], y=data['Rating'], kind='scatter')
plt.title('Total vs Rating')
plt.show()
```
![383106925-e2294d12-a720-4a7a-a933-0ac018bbe136](https://github.com/user-attachments/assets/ccb1bbbc-be77-42fb-acfd-29f26dcfae2b)

# Result:
Thus we have cleaned the data and removed the outliers by Data cleaning process.
