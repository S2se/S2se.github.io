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

5. Get rid of variables
- Identify Unused Variables
- Check for Redundancy


```python
bs_cleaned = bs_cleaned.drop(columns = ['sample_id' ,'quality_score' ])
bs_cleaned.info()
```   

<img width="344" alt="Screenshot 2024-12-08 at 11 17 18 PM" src="https://github.com/user-attachments/assets/b04671e3-7e9d-4ba4-b4d1-4a6c2002f980">  

6. Adapt Random Forest classification  

RandomForestClassifier : [sckit learn explanation](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html)  

```python
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestRegressor

x = bs_cleaned.drop(columns=[ 'quality_category']) 
y = bs_cleaned["quality_category"]

x_train, x_test , y_train, y_test = train_test_split(x, y, test_size=0.2, random_state=42)
print(x_train.shape, x_test.shape, y_train.shape, y_test.shape)
```  

(799, 8) (200, 8) (799,) (200,)

```python
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score 

clf = RandomForestClassifier(n_estimators=100, max_depth=20,random_state=0)
clf.fit(x_train,y_train)

predict1 = clf.predict(x_test)
print(accuracy_score(y_test,predict1))
```
Accuracy score is 0.86.  

```python
from sklearn.model_selection import cross_validate

scores = cross_validate(
    clf, x, y, cv=5, scoring=['accuracy', 'f1_weighted']
)

print("Accuracy score:", scores['test_accuracy'])
print("F1-score :", scores['test_f1_weighted'])
print("Average Accuracy score:", scores['test_accuracy'].mean())
print("Average F1-score:", scores['test_f1_weighted'].mean())
```

7. Result 
Accuracy score: [0.92       0.855      0.895      0.935      0.91959799]  
F1-score : [0.90774265 0.84391891 0.88608024 0.92155348 0.91306533]  
Average Accuracy score: 0.9049195979899498  
Average F1-score: 0.8944721218848048  