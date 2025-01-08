---
layout: post
title:  "[Project] Updated Analysis of Boston housing dataset"
date:   2025-01-01 07:03:36 +0900
categories: [Project, Python]

---

## Description  

+ The purpose
    - From the previous analysis, I noticed some shortcomings and decided to redo it, particularly addressing the lack of outlier analysis. 
    - Given Boston's environmental characteristics, such as the higher proportion of Black residents and the clear disparities in housing prices and income by race, the importance of variable B increases. Therefore, I plan to consider removing outliers of variables that have minimal impact on other factors.
    - Additionally, I will create histograms for the data to assess how each variable influences the dependent variable, aiming to achieve more accurate analysis results.   

```python
ds.isna().sum()

ds['CRIM'].fillna(ds['CRIM'].mean(), inplace=True)
ds['ZN'].fillna(ds['ZN'].mean(), inplace=True)
ds['INDUS'].fillna(ds['INDUS'].mean(), inplace=True)
ds['CHAS'].fillna(ds['CHAS'].mean(), inplace=True)
ds['AGE'].fillna(ds['AGE'].mean(), inplace=True)
ds['LSTAT'].fillna(ds['LSTAT'].mean(), inplace=True)


fig, ax = plt.subplots(nrows=2, ncols=7, figsize=(20, 8))

for i, column in enumerate(ds.columns):
    index = ax[i // 7, i % 7]   
    index.boxplot(ds[column], notch=True, whis=2.5)
    index.set_xlabel(f"{column}")
plt.tight_layout()
plt.show()
```

<img width="719" alt="Screenshot 2025-01-01 at 3 25 22 PM" src="https://github.com/user-attachments/assets/e96ecb9d-1574-41ab-afb1-a5b548421d94" />  

As you can see, the variables that show outliers are CRIM (crime rate), ZN (proportion of residential land), RM(the number of rooms), B(Black people).  

**Standard for Removing Outliers**   
: Which outliers should be removed from the dataset?  
1. Extreme Values: Remove outliers that are unreasonably large or small. For example, an age value of 300 would be considered an outlier and should be removed.  
2. Dataset Size: A sufficiently large dataset may absorb the impact of outliers, making their removal less critical.  
3. Reversibility: Consider keeping outliers for now, especially if you might want to bring them back later.  
4. Threshold of Impact: When outliers make up more than 25% of the data, removal is generally not recommended, as they could represent meaningful variation.  


<img width="527" alt="Screenshot 2025-01-01 at 3 30 43 PM" src="https://github.com/user-attachments/assets/d235b786-2370-48ec-8472-2a4d455abae3" />  

1. The lower the value of LSTAT (the percentage of lower-status population), the higher the house prices tend to be.   
2. The higher the percentage of the lower-status population, the more rooms there are, and the higher the house prices.  

<img width="1144" alt="Screenshot 2025-01-07 at 7 48 05 PM" src="https://github.com/user-attachments/assets/62e9c3d7-1f76-472b-a614-77604410d11d" />  
Here’s the correlation heatmap. As mentioned earlier, there is a positive correlation between RM and MEDV, while LSTAT and MEDV show a negative correlation.  

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler() 
scale_columns = ['CRIM', 'ZN', 'INDUS', 'NOX', 'RM', 'AGE', 'DIS', 'RAD', 'TAX', 'PTRATIO', 'B', 'LSTAT']
ds[scale_columns] = scaler.fit_transform(ds[scale_columns])

ds.head()
```  

<img width="963" alt="Screenshot 2025-01-08 at 2 51 14 PM" src="https://github.com/user-attachments/assets/23470305-537d-4756-8b5f-d5b79462b01b" />  




