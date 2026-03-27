# -*- coding: utf-8 -*-
"""
Created on Sat Apr 13 12:50:20 2024

@author: hanee
"""

import numpy as np # linear algebra
import pandas as pd # data processing, CSV file I/O (e.g. pd.read_csv)
import matplotlib.pyplot as plt
import seaborn as sns

# Input data files are available in the read-only "../input/" directory
# For example, running this (by clicking run or pressing Shift+Enter) will list all files under the input directory


df = pd.read_csv("C:\\Users\\hanee\\Downloads\\unemployement\\Unemployment_Rate_-_Trailing_30_days_D_Rural.txt",sep=", ")
print(df)

a_file = open("C:\\Users\\hanee\\Downloads\\unemployement\\Unemployment_Rate_-_Trailing_30_days_D_Rural.txt", "r")

lines = a_file.readlines()[1:]
with open("sample.txt","w") as f1:
    for i in lines:
        f1.write(i+'\n')
a_file.close()

d = pd.read_table("sample.txt",sep=", ")
print(d)
print(d.columns)

print(d.info())
print(d.head(6))
print(d['Value'].describe())
print(np.unique(d['Region']))
print(d['Date'].unique())
print(np.unique(d['Frequency']))
print(np.unique(d['Value']))
print(d.isna().sum())
d.insert(4,'Day',0)
d.insert(5,'Month',0)
d.insert(6,'Year',0)
print(d.info())
for i in range(2053):
    d['Day'][i]=int(d['Date'][i][0:2])
    d['Month'][i]=int(d['Date'][i][3:5])
    d['Year'][i]=int(d['Date'][i][6:])
    
print(d.head(6))
print(max(d['Year']))
print(min(d['Year']))

plt.scatter(d['Date'],d['Value'],c='#FF6B6B')
plt.title('Scatter plot of Date vs Value of Unemployment')
plt.xlabel('Date(From 29 Jan 2016 to 14 Sep 2021)')
plt.ylabel('Value')
plt.xticks(rotation=0)
plt.show()

ValMean=d['Value'].mean()

plt.scatter(d['Date'],d['Value'],c='#FF6B6B')
plt.title('Scatter plot of Date vs Value of Unemployment')
plt.xlabel('Date (From 29 Jan 2016 to 14 Sep 2021)')
plt.ylabel('Value')
plt.xticks(rotation=0)
plt.plot(['29-01-2016','14-09-2021'], [ValMean, ValMean])

plt.show()

plt.scatter(d['Year'],d['Value'],c='#FF6B6B')
plt.title('Scatter plot of Year vs Value of Unemployment')
plt.xlabel('Year')
plt.ylabel('Value')
plt.xticks(rotation=0)
plt.plot([2016,2021], [ValMean, ValMean])
plt.show()

plt.scatter(d['Month'],d['Value'],c='#FF6B6B')
plt.title('Scatter plot of Month vs Value of Unemployment')
plt.xlabel('Month')
plt.ylabel('Value')
plt.xticks(rotation=90)
plt.show()

arr1=[]
arr2=[]
for i in range (2053):
    if d['Year'][i]==2020:
        arr1.append(d['Value'][i])
        arr2.append(d['Month'][i])
        
plt.scatter(arr2, arr1,c='#FF6B6B')
plt.title('Scatter plot of Month vs Value of Unemployment for the year 2020')
plt.xlabel('Month')
plt.ylabel('Value')
plt.show()

sns.set_theme(style="darkgrid")
sns.pairplot(d,kind="scatter",hue="Value")
plt.show()

sns.pairplot(d,kind="scatter")
plt.show()

sns.pairplot(d, kind="kde")
plt.show()
sns.pairplot(d, kind="hist")

sns.histplot(x="Value",data=d,kde=True,bins=30)

