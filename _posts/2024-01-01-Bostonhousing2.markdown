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

As you can see, the variables that show outliers are CRIM (crime rate), ZN (proportion of residential land), and CHAS (whether the tract bounds the Charles River). Considering the environment of Boston, it is judged that the presence or absence of the Charles River boundary will not have a significant impact compared to the other variables, so the outlier is removed.  


```python
q1 = ds['CHAS'].quantile(0.25)
q3 = ds['CHAS'].quantile(0.75)
IQR = q3 - q1
lower_bound = q1 - 1.5*IQR
upper_bound = q3 + 1.5*IQR
ds_cleaned = ds[(ds['CHAS']>=lower_bound) & (ds['CHAS']<=upper_bound)]

num_columns = len(ds_cleaned.columns)
rows = (num_columns + 3) // 4  
fig, axs = plt.subplots(rows, 4, figsize=(8, 2 * rows))  
axs = axs.flatten()

for i, column in enumerate(ds_cleaned.columns):
    axs[i].hist(ds_cleaned[column].dropna(), bins=10, color='skyblue', edgecolor='black')
    axs[i].set_title(column, fontsize=10)
    axs[i].set_xlabel(column, fontsize=8)
    axs[i].set_ylabel('Frequency', fontsize=8)
    axs[i].grid(axis='y', linestyle='--', alpha=0.7)

for j in range(i + 1, len(axs)):
    axs[j].axis('off')
    
plt.tight_layout()
plt.show()

```

<img width="527" alt="Screenshot 2025-01-01 at 3 30 43 PM" src="https://github.com/user-attachments/assets/d235b786-2370-48ec-8472-2a4d455abae3" />  

1. The lower the value of LSTAT (the percentage of lower-status population), the higher the house prices tend to be.   
2. The higher the percentage of the lower-status population, the more rooms there are, and the higher the house prices.  