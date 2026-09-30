# Python-EDA-and-Correlation-Analysis
## Overview
This project analyzes a hypothetical B2B and B2G company that sells various goods—including Amarilla, Carretera, Montana, Paseo, Velo, and VTT—to government agencies, small businesses, and enterprise clients. Using Python, I cleaned and preprocessed the raw dataset before conducting an exploratory data analysis (EDA) and correlation analysis to uncover key business insights and relationships.

### Data Cleaning
I used python to clean my data before conducting EDA and Correlation Analysis

```
import pandas as pd
import seaborn as sns
import numpy as np

import matplotlib
import matplotlib.pyplot as plt
plt.style.use('ggplot')
from matplotlib.pyplot import figure

%matplotlib inline
matplotlib.rcParams['figure.figsize'] = (6,2)
```
Importing the excel file into Jupyter Notebook

```df = pd.read_excel(r'/Users/dc/Downloads/Sample datasets copy1.xlsx') 
df.head() # to check the first five rows of the dataset after importing it
df.shape # this tells you the number of rows and columns in our data. So we have 700 rows and 16 columns
```
Dropping columns that are not necessary for our analysis
```
df = df.drop(columns =['Unnamed: 16', 'Unnamed: 17', 'Unnamed: 18'])
df.info() # to check what your data is made up of
```
Checking for nulls and missing values
```
# count the amount of nulls in each column and return the column n their numbers of missing values
for values in df.columns:
    count = df[values].isnull().sum() # for every value in the df count the null value and the sum them to get the total number of null values
    print(values, count)
```
Treating missing and null values
```
# so we have missing values in discount band, sales, and month number, how do we fill them without droping it
# df[values]
df['Discount Band'] = df['Discount Band'].fillna(0)
df[' Sales'] = df[' Sales'].fillna(0)
df['Month Name'] = df['Month Name'].fillna(0)

df.isnull().sum()  # checking to see if we still have any null value and there are none     
```
First converting the date column to 'datetime' then splitting it up to show individual columns for the month, day and year
```
# first drop the error dates splits

#df = df.drop(columns =['Unnamed: 16', 'Unnamed: 17', 'Unnamed: 18'])

#convert the date column to a date time and split it up
df['Date_Time'] = pd.to_datetime(df['Date'])

df['Day'] = df['Date_Time'].dt.day # extracts the day into the column day
df['Month_Text'] = df['Date_Time'].dt.strftime('%b') # extracts the month in short form
df['Month_Num'] = df['Date_Time'].dt.month # extracts the month as 1, 2, 3
df['Years'] = df['Date_Time'].dt.year # extracts the year from the date
df
```
### Exploratory Data Analysis (EDA)
Sales by revenue
```
# segment with the most number of sales

segment_revenue = df.groupby('Segment')[' Sales'].sum()

print(segment_revenue)
segment_revenue = segment_revenue.sort_values(ascending=True)
segment_revenue.plot(kind='barh')

plt.title('Revenue by Segment')
plt.xlabel('Segment')
plt.ylabel('Total Revenue')
plt.show()
```
Units sold by Products
```
units_sold_by_products = df.groupby('Product')['Units Sold'].sum()

print(units_sold_by_products)
units_sold_by_products = units_sold_by_products.sort_values(ascending=True)
units_sold_by_products.plot(kind='barh')

plt.title('Units Sold by Products')
plt.xlabel('Total Units Sold')
plt.ylabel('Products')
plt.show()
```















