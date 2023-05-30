# Ex-08-Data-Visualization-

## AIM
To Perform Data Visualization on a complex dataset and save the data to a file. 

# Explanation
Data visualization is the graphical representation of information and data. By using visual elements like charts, graphs, and maps, data visualization tools provide an accessible way to see and understand trends, outliers, and patterns in data.

# ALGORITHM
### STEP 1
Read the given Data
### STEP 2
Clean the Data Set using Data Cleaning Process
### STEP 3
Apply Feature generation and selection techniques to all the features of the data set
### STEP 4
Apply data visualization techniques to identify the patterns of the data.


# CODE
# DATA PREPROCESSING
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from google.colab import files
uploaded = files.upload()
df = pd.read_csv("tips.csv")
df
```
```
df.isnull().sum()
```
![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/adf3f7bc-67e7-43c6-8f6d-782971784da1)
# FINDING OUTLIERS
```
plt.figure(figsize=(8,8))
plt.title("Data with outliers")
df.boxplot()
plt.show()
```
![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/f352f2c7-3948-43d8-9175-ba067a7c24c3)
# REMOVING OUTLIERS
```
plt.figure(figsize=(8,8))
cols = ['size','tip','total_bill']
Q1 = df[cols].quantile(0.25)
Q3 = df[cols].quantile(0.75)
IQR = Q3 - Q1
df = df[~((df[cols] < (Q1 - 1.5 * IQR)) |(df[cols] > (Q3 + 1.5 * IQR))).any(axis=1)]
plt.title("Dataset after removing outliers")
df.boxplot()
plt.show()
```
![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/5094d898-93e5-40c1-8219-b2c6c30ffad3)
# 1.Which day of the week has the highest total bill amount?
```
sns.barplot(x="day", y="total_bill", data=df)
plt.title("Total Bill Amount by Day of Week")
plt.show()
```
![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/45d7e74f-f82e-4dff-a4ef-a7e328ead13f)
# 2.What is the average tip amount given by smokers and non-smokers?
```
sns.boxplot(x="smoker", y="tip", data=df)
plt.title("Tip Amount by Smoking Status")
plt.show()
```
![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/19bc3748-812e-4308-b765-e9bfcaaf4807)

# 3.How does the tip percentage vary based on the size of the dining party?
```
df["tip_pct"] = df["tip"] / df["total_bill"]
sns.scatterplot(x="size", y="tip_pct", data=df)
plt.title("Tip Percentage by Dining Party Size")
plt.show()
```
![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/08da4ddf-0a69-4d0d-9492-cb6cbbfad189)
# 4.Which gender tends to leave higher tips?
![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/22bbf54e-84b0-4d6e-9132-d5ac2498ff8a)

# 5.Is there any relationship between the total bill amount and the day of the week?
```
sns.scatterplot(x="day", y="total_bill", data=df)
plt.title("Total Bill Amount by Day of Week")
plt.show()
```
![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/608fd3af-1f31-4ffe-a623-f715fe5c6906)
# 6.How does the distribution of total bill amounts vary across different time periods (lunch vs. dinner)?
```
sns.histplot(data=df, x="total_bill", hue="time", element="step", stat="density")
plt.title("Distribution of Total Bill Amounts by Time of Day")
plt.show()
```
![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/dfd435e1-f328-4a1c-b9e9-bdc123362f07)
# 7.Which dining party size group tends to have the highest average total bill amount?
```
sns.barplot(x="size", y="total_bill", data=df)
plt.title("Average Total Bill Amount by Dining Party Size")
plt.show()
```
![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/1c46c7bf-34c6-49fa-8a61-c65643d83698)
# 8.What is the distribution of tip amounts for each day of the week?
```
sns.boxplot(x="day", y="tip", data=df)
plt.title("Tip Amount by Day of Week")
plt.show()
```
![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/7ba83caf-f3ac-4a23-9ab5-b0e4e1f512d9)
# 9.How does the tip amount vary based on the type of service (lunch vs. dinner)?
```
sns.violinplot(x="time", y="tip", data=df)
plt.title("Tip Amount by Time of Day")
plt.show()
```
![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/fc6ba855-d71d-4663-8a45-8fbe65659f71)
# 10.Is there any correlation between the total bill amount and the tip amount?
```
sns.scatterplot(x="total_bill", y="tip", data=df)
plt.title("Correlation between Tip Amount and Total Bill Amount")
plt.show()
```
![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/a2d27635-07ec-4736-86f2-79f5897f9245)
# Result:
Thus, Data Visualization is performed on the given dataset and save the data to a fil



