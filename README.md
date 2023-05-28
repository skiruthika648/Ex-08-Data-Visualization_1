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
```
#loading the dataset
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
df=pd.read_csv("Superstore.csv")
df
#removing unnecessary data variables
df.drop('Row ID',axis=1,inplace=True)
df.drop('Order ID',axis=1,inplace=True)
df.drop('Customer ID',axis=1,inplace=True)
df.drop('Customer Name',axis=1,inplace=True)
df.drop('Country',axis=1,inplace=True)
df.drop('Postal Code',axis=1,inplace=True)
df.drop('Product ID',axis=1,inplace=True)
df.drop('Product Name',axis=1,inplace=True)
df.drop('Order Date',axis=1,inplace=True)
df.drop('Ship Date',axis=1,inplace=True)
print("Updated dataset")
df

df.isnull().sum()
#detecting and removing outliers in current numeric data
plt.figure(figsize=(12,10))
plt.title("Data with outliers")
df.boxplot()
plt.show()

plt.figure(figsize=(12,10))
cols = ['Sales','Quantity','Discount','Profit']
Q1 = df[cols].quantile(0.25)
Q3 = df[cols].quantile(0.75)
IQR = Q3 - Q1
df = df[~((df[cols] < (Q1 - 1.5 * IQR)) |(df[cols] > (Q3 + 1.5 * IQR))).any(axis=1)]
plt.title("Dataset after removing outliers")
df.boxplot()
plt.show()
#data visualization
#line plots
import seaborn as sns
sns.lineplot(x="Sub-Category",y="Sales",data=df,marker='o')
plt.title("Sub Categories vs Sales")
plt.xticks(rotation = 90)
plt.show()

sns.lineplot(x="Category",y="Profit",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Categories vs Profit")
plt.show()

sns.lineplot(x="Region",y="Sales",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Region area vs Sales")
plt.show()

sns.lineplot(x="Category",y="Discount",data=df,marker='o')
plt.title("Categories vs Discount")
plt.show()

sns.lineplot(x="Sub-Category",y="Quantity",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Sub Categories vs Quantity")
plt.show()
#bar plots
sns.barplot(x="Sub-Category",y="Sales",data=df)
plt.title("Sub Categories vs Sales")
plt.xticks(rotation = 90)
plt.show()

sns.barplot(x="Category",y="Profit",data=df)
plt.title("Categories vs Profit")
plt.show()

sns.barplot(x="Sub-Category",y="Quantity",data=df)
plt.title("Sub Categories vs Quantity")
plt.xticks(rotation = 90)
plt.show()

sns.barplot(x="Category",y="Discount",data=df)
plt.title("Categories vs Discount")
plt.show()

plt.figure(figsize=(12,7))
sns.barplot(x="State",y="Sales",data=df)
plt.title("States vs Sales")
plt.xticks(rotation = 90)
plt.show()

plt.figure(figsize=(25,8))
sns.barplot(x="State",y="Sales",hue="Region",data=df)
plt.title("State vs Sales based on Region")
plt.xticks(rotation = 90)
plt.show()
#Histogram
sns.histplot(data = df,x = 'Region',hue='Ship Mode')
sns.histplot(data = df,x = 'Category',hue='Quantity')
sns.histplot(data = df,x = 'Sub-Category',hue='Category')
plt.xticks(rotation = 90)
plt.show()
sns.histplot(data = df,x = 'Quantity',hue='Segment')
plt.hist(data = df,x = 'Profit')
plt.show()
#count plot
plt.figure(figsize=(10,7))
sns.countplot(x ='Segment', data = df,hue = 'Sub-Category')
sns.countplot(x ='Region', data = df,hue = 'Segment')
sns.countplot(x ='Category', data = df,hue='Discount')
sns.countplot(x ='Ship Mode', data = df,hue = 'Quantity')
#Barplot 
sns.boxplot(x="Sub-Category",y="Discount",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot( x="Profit", y="Category",data=df)
plt.xticks(rotation = 90)
plt.show()
plt.figure(figsize=(10,7))
sns.boxplot(x="Sub-Category",y="Sales",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot(x="Category",y="Profit",data=df)
sns.boxplot(x="Region",y="Sales",data=df)
plt.figure(figsize=(10,7))
sns.boxplot(x="Sub-Category",y="Quantity",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot(x="Category",y="Discount",data=df)
plt.figure(figsize=(15,7))
sns.boxplot(x="State",y="Sales",data=df)
plt.xticks(rotation = 90)
plt.show()
#KDE plot
sns.kdeplot(x="Profit", data = df,hue='Category')
sns.kdeplot(x="Sales", data = df,hue='Region')
sns.kdeplot(x="Quantity", data = df,hue='Segment')
sns.kdeplot(x="Discount", data = df,hue='Segment')
#violin plot
sns.violinplot(x="Profit",data=df)
sns.violinplot(x="Discount",y="Ship Mode",data=df)
sns.violinplot(x="Quantity",y="Ship Mode",data=df)
#point plot
sns.pointplot(x=df["Quantity"],y=df["Discount"])
sns.pointplot(x=df["Quantity"],y=df["Category"])
sns.pointplot(x=df["Sales"],y=df["Sub-Category"])
#Pie Chart
df.groupby(['Category']).sum().plot(kind='pie', y='Discount',figsize=(6,10),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Sub-Category']).sum().plot(kind='pie', y='Sales',figsize=(10,10),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Region']).sum().plot(kind='pie', y='Profit',figsize=(6,9),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Ship Mode']).sum().plot(kind='pie', y='Quantity',figsize=(8,11),pctdistance=1.7,labeldistance=1.2)

df1=df.groupby(by=["Category"]).sum()
labels=[]
for i in df1.index:
    labels.append(i)  
plt.figure(figsize=(8,8))
colors = sns.color_palette('pastel')
plt.pie(df1["Profit"],colors = colors,labels=labels, autopct = '%0.0f%%')
plt.show()

df1=df.groupby(by=["Ship Mode"]).sum()
labels=[]
for i in df1.index:
    labels.append(i)
colors=sns.color_palette("bright")
plt.pie(df1["Sales"],labels=labels,autopct="%0.0f%%")
plt.show()
#HeatMap
df4=df.copy()

#encoding
from sklearn.preprocessing import LabelEncoder,OrdinalEncoder,OneHotEncoder
le=LabelEncoder()
ohe=OneHotEncoder
oe=OrdinalEncoder()

df4["Ship Mode"]=oe.fit_transform(df[["Ship Mode"]])
df4["Segment"]=oe.fit_transform(df[["Segment"]])
df4["City"]=le.fit_transform(df[["City"]])
df4["State"]=le.fit_transform(df[["State"]])
df4['Region'] = oe.fit_transform(df[['Region']])
df4["Category"]=oe.fit_transform(df[["Category"]])
df4["Sub-Category"]=le.fit_transform(df[["Sub-Category"]])

#scaling
from sklearn.preprocessing import RobustScaler
sc=RobustScaler()
df5=pd.DataFrame(sc.fit_transform(df4),columns=['Ship Mode', 'Segment', 'City', 'State','Region',
                                               'Category','Sub-Category','Sales','Quantity','Discount','Profit'])

#Heatmap
plt.subplots(figsize=(12,7))
sns.heatmap(df5.corr(),cmap="PuBu",annot=True)
plt.show()
```
# OUPUT
# Initial Dataset:
![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/0e4920a3-fa1f-4d21-8ceb-dcddda2598e6)

# Cleaned Dataset:
![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/04be4192-e746-475b-b68c-4d24f8722ffb)

# Removing Outliers:
![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/2e65c35d-27d2-4b82-91ad-f45f91990ef8)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/d94e2961-d350-4980-a929-118578f6bb14)

# Line PLot:
![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/c8b0a64d-0b65-4225-a3d8-4033ce08f72d)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/5297d76e-eae3-4409-86a0-73dcef9dfa67)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/e7fcdd21-06ff-46e9-9a8f-264761bdb9f1)

# Bar Plots:
![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/aa043d7a-6861-495d-8923-03fde2be677d)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/e1c001e8-1112-4c2d-90c9-6b9eafe2f5f6)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/6f6c4738-bf43-4e7c-b968-3f962cf23317)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/f25d9f0c-3226-40d7-b152-4d1d67b1ab5a)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/a2b7dbc3-2e1c-417e-ba65-86f05edbf39e)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/da4aa329-2321-421d-8f4a-2301be8aa61b)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/da882b40-f1f0-4175-b878-8c45ff9af004)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/9cdee55e-d2f2-49b3-8b83-4ac7c117acb6)
# Histograms:
![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/7d491bf7-eb0d-40b9-96d5-c6a04b41cca2)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/7577f3d7-83ae-4b76-a686-aa9c9218e91f)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/3275a914-7099-4758-91d4-0f977282fb44)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/bdc66d36-6979-4ac9-8aa5-8df9b0834de8)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/d1f4cff8-48f9-48a8-a188-a96967cfb34d)
# Count plots:
![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/b383f987-ffef-4ea2-825c-efe42bda93d5)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/82426910-817e-41a4-bd19-6a804131d291)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/b6e9d863-c0ab-4bff-8788-06435a60026b)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/7297cf7c-421d-480c-bf16-0dc1097dd34d)
# Bar Charts:
![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/947794dd-ca0d-4032-847a-91e1d6ae6c79)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/4f09c861-af35-4304-8a58-408f89373239)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/77fe661a-501d-4c0c-bf4f-a9c06526c914)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/dd54ddf8-6058-490f-8b1d-b03709729b68)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/d3e6547b-6449-42ee-9806-ec55fa22ac7e)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/e7293943-9a30-43f4-9edb-2907b49c8fc4)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/d3314ec5-a349-438d-b6b0-546e4577bc14)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/05f9494f-0433-404f-8b4a-1dca18ac5489)
# KDE Plots:
![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/f4c14219-7b6a-4d55-99c2-d6b1b345410a)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/83b1931f-32d2-4aea-bdb9-1f84b4cd9eb3)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/f2fdec6a-a81e-4720-a120-4a1a902de601)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/850e5180-69fb-461f-a534-44395855ec77)
# Violin Plot:
![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/ddc39bf5-e3a7-4acf-bc4e-2f932a67c5b7)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/cb485f19-124d-43e5-9f68-a2f435e4c5e6)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/17c1f59f-34c0-4bd1-8376-db612d65fc82)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/4f934849-f13b-41fa-a443-e66a6a16a39d)

# Point Plots:
![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/327096fd-449c-4f21-a23f-d79e04ca3ae8)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/342dc6f1-0638-4aba-8c68-6fd11ef68cc5)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/67723beb-6419-4cfd-99cc-c2461ae0b87d)
# Pie Charts:
![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/22df7a31-51d3-49eb-8a88-1df25956d716)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/ec8ecc5d-b702-4bca-b362-7daaf4222fbd)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/1e526e52-26dd-4d7d-a7f8-95b1d2e81eed)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/99374c09-00dd-42d7-b9ef-e5d59d0c1b3b)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/260fc40a-6738-49bb-8eb9-4d3ae544176e)

![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/e3d0d39f-5e11-4873-b72a-db02b62596d5)

# HeatMap:
![image](https://github.com/skiruthika648/Ex-08-Data-Visualization_1/assets/128348968/70449266-4421-4640-9570-17f092659a7d)

# Result:
Hence,Data Visualization is applied on the complex dataset using libraries like Seaborn and Matplotlib successfully and the data is saved to file.

