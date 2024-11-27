---
layout: post
title:  "[Project] Analysis Banana Quality"
date:   2024-11-19 14:03:36 +0900
categories: [Project, Python]
---

## Description  
### A model for finding a high-quality bananas  
The dataset : [Dataset_from_Kaggle](https://www.kaggle.com/datasets/mrmars1010/banana-quality-dataset/data)  

1. Bring the dataset  
```python
import pandas as pd
import sklearn
import matplotlib.pyplot as plt
import numpy as np

bs = pd.read_csv("/Users/leesangeun/Downloads/banana_quality_dataset.csv")
bs.head()
```

<img width="987" alt="Screenshot 2024-11-20 at 10 27 59 PM" src="https://github.com/user-attachments/assets/8b90d448-55c6-4a40-9d84-3d379572afcb">  

2. Deal with null values  
```python
bs.isna().sum()
bs.info()
```

<img width="216" alt="Screenshot 2024-11-20 at 10 29 01 PM" src="https://github.com/user-attachments/assets/4438997e-6404-45e9-bb7c-599fc388d7f5">  
<img width="423" alt="Screenshot 2024-11-20 at 10 29 45 PM" src="https://github.com/user-attachments/assets/23bd75c8-10aa-45c8-8c86-6ebc04cc1920">  

3. Replacing category values to numeric values  
```python
from sklearn.preprocessing import LabelEncoder
le = LabelEncoder()

bs['variety'] = le.fit_transform(bs['variety'])
bs['region'] = le.fit_transform(bs['region'])
bs['quality_category'] = le.fit_transform(bs['quality_category'])

bs = bs.drop(['ripeness_category'], axis = 1)
bs = bs.drop(['tree_age_years'], axis = 1)
bs = bs.drop(['altitude_m'], axis = 1)
bs = bs.drop(['rainfall_mm'], axis = 1)
bs = bs.drop(['harvest_date'], axis = 1)

bs.head()
```

<img width="947" alt="Screenshot 2024-11-20 at 10 30 54 PM" src="https://github.com/user-attachments/assets/287eb0e7-93f2-4bcc-80bb-c6ae09e73e25">  

4. Check the outliers with boxplot  

```python
import seaborn as sns

col_bs = [
    "quality_score", "ripeness_index", "sugar_content_brix",
    "firmness_kgf", "length_cm", "weight_g", "soil_nitrogen_ppm"
]

plt.figure(figsize=(14, 10))
for i, col in enumerate( col_bs, 1):
    plt.subplot(3, 3, i)
    sns.boxplot(y=bs[col], color="darkgreen")  
    plt.title(f"Boxplot of {col}")

plt.tight_layout()
plt.show()
```  

<img width="779" alt="Screenshot 2024-11-27 at 10 48 27 PM" src="https://github.com/user-attachments/assets/7552d277-9c76-433a-b550-46f79c0ad872">  

