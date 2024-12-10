---
layout: post
title:  "[Project] Analysis Banana Quality"
date:   2024-11-19 14:03:36 +0900
categories: [Project, Python]
---

## Description  
### A model for finding a high-quality bananas  
- The dataset : [Dataset_from_Kaggle](https://www.kaggle.com/datasets/mrmars1010/banana-quality-dataset/data)  
- Build a RandomForest Classifier  

```python
import seaborn as sns
sns.pairplot(bs_cleaned)
```  

<img width="782" alt="Screenshot 2024-12-10 at 3 26 38 PM" src="https://github.com/user-attachments/assets/9855bc5f-6735-485a-93de-18dcac802945">  

This is evident that there is no discernible linear relationship between any variables.  
The data exhibit non-linear relations between them.  

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
```  

4. Get rid of variables
- Identify Unused Variables
- Check for Redundancy  

```python
bs_cleaned = bs.drop(columns = ['sample_id' ,'quality_score','ripeness_category', 'tree_age_years', 'altitude_m', 'rainfall_mm', 'harvest_date' ])
bs_cleaned.info()
```  

<img width="338" alt="Screenshot 2024-12-10 at 3 08 27 PM" src="https://github.com/user-attachments/assets/65a91a53-fe0a-4286-ac8e-44e0d8656fd7">  

5. Check the outliers with boxplot  

```python
import seaborn as sns

col_bs = [
     "ripeness_index", "sugar_content_brix",
    "firmness_kgf", "length_cm", "weight_g", "soil_nitrogen_ppm"
]

plt.figure(figsize=(14, 10))
for i, col in enumerate( col_bs, 1):
    plt.subplot(3, 3, i)
    sns.boxplot(y=bs_cleaned[col], color="darkgreen")  
    plt.title(f"Boxplot of {col}")

plt.tight_layout()
plt.show()
```  


<img width="778" alt="Screenshot 2024-12-10 at 3 10 44 PM" src="https://github.com/user-attachments/assets/448f24b4-d477-4664-89df-f9293d081a26">   


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

(800, 8) (200, 8) (800,) (200,)

```python
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score 

clf = RandomForestClassifier(n_estimators=100, max_depth=20,random_state=0)
clf.fit(x_train,y_train)

predict1 = clf.predict(x_test)
print(accuracy_score(y_test,predict1))
```
Accuracy score is 0.895.  

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
Accuracy score: [0.925 0.89  0.875 0.935 0.895]  
F1-score : [0.91546266 0.88079787 0.86371544 0.92769708 0.88211976]  
Average Accuracy score: 0.9039999999999999  
Average F1-score: 0.8939585619159265  