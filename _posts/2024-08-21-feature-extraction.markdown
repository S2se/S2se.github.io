---
layout: post
title:  "[Project] Feature Extraction"
date:   2024-08-21 21:03:36 +0900
categories: Python
---

## Description  
### The problem   
1. A consequence of a consistent strive to innovate on a large, multi-national scale, which results in a massive amount of data.​  

2. At this scale, manually finding the key information (features) in an international haystack of data is infeasible. ​ 

3. To maintain their reputation as an innovation leader, Ericsson cannot afford to waste time on these outdated, manual approaches for feature extraction.  

## Approach1 : Understanding the data to be used  

| Email                                                    | whirlpool Forum                                                                    |
|----------------------------------------------------------|------------------------------------------------------------------------------------|
| It is semi-structured, and the content is unpredictable. | Forum where customers discuss customer services. Similarly, there is no structure. |  


## Approach2 : Identifying the tools to be used.  
1. imap_tools
2. Spacy
3. postgresql  

First of all, make the **account.py** file. Should be your email account.  
Password should be app password.

```python
Email_address = "youremail@gmail.com"
Email_password = "password"
```
Save each email into the execl file.

```python
from imap_tools import MailBox
from account import *
import pandas as pd

mailbox =MailBox("imap.gmail.com", 993)
mailbox.login(Email_address, Email_password, initial_folder= "INBOX")
sample_email = pd.DataFrame(columns =['title', 'send', 'get', 'date', 'message'])

for msg in mailbox.fetch(limit=20, reverse=True):
    date =  msg.date
    date2 =date.strftime('%Y-%m-%d')
    title = msg.subject
    send = msg.from_
    get =  msg.to
    message = msg.text
    raw_data = {'title' : title,
                'send' : send,
                'get' :  get,
                'date' :  date2,
                'message' : message
                }

    sample_email= sample_email.append(raw_data, ignore_index =True)
  
sample_email.to_excel('sample.xlsx')
mailbox.logout()

```
<img width="550" alt="Screenshot 2024-09-01 at 4 46 45 PM" src="https://github.com/user-attachments/assets/b88d4003-26dd-40ab-bca9-d9286f4d8c35">  
We got a 20 rows and 5 of each columns. 
