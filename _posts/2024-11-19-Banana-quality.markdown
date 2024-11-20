---
layout: post
title:  "[Project] Analysis Banana Quality"
date:   2024-11-19 14:03:36 +0900
categories: [Project, Python]
---

## Description  
[Dataset_from_Kaggle](https://www.kaggle.com/datasets/mrmars1010/banana-quality-dataset/data)  

```python
import pandas as pd
import sklearn
import matplotlib.pyplot as plt
import numpy as np

bs = pd.read_csv("/Users/leesangeun/Downloads/banana_quality_dataset.csv")
bs.head()
```

<img width="987" alt="Screenshot 2024-11-20 at 10 27 59 PM" src="https://github.com/user-attachments/assets/8b90d448-55c6-4a40-9d84-3d379572afcb">  

```python
bs.isna().sum()
bs.info()
```

<img width="216" alt="Screenshot 2024-11-20 at 10 29 01 PM" src="https://github.com/user-attachments/assets/4438997e-6404-45e9-bb7c-599fc388d7f5">  
<img width="423" alt="Screenshot 2024-11-20 at 10 29 45 PM" src="https://github.com/user-attachments/assets/23bd75c8-10aa-45c8-8c86-6ebc04cc1920">  

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



```python
import seaborn as sns


```
