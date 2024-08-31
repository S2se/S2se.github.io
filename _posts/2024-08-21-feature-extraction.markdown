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
Get the mail

```python
from imap_tools import MailBox
from account import *

mailbox =MailBox("imap.gmail.com", 993)
mailbox.login(Email_address, Email_password, initial_folder= "INBOX")
```