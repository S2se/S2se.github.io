---
layout: post
title:  "[Project] Feature Extraction: 2. Whirlpool"
date:   2024-08-21 21:03:36 +0900
categories: Python
---

## Description  
## Feature Extraction2 

### The problem   
1. A consequence of a consistent strive to innovate on a large, multi-national scale, which results in a massive amount of data.​  

2. At this scale, manually finding the key information (features) in an international haystack of data is infeasible. ​ 

3. To maintain their reputation as an innovation leader, Ericsson cannot afford to waste time on these outdated, manual approaches for feature extraction.  

### Approach 1
1. Web crawling: Get the text from Whirlpool website. 

```python
import requests
import bs4


URL = "https://forums.whirlpool.net.au/thread/3n4wj8v3"
response = requests.get(URL)
soup = bs4.BeautifulSoup(response.text,"html.parser")
```

However, Whirlpool does not allow to access their source code.  
<img width="1440" alt="Sourcecode_whirlpool" src="https://github.com/user-attachments/assets/efb4007d-777b-4319-ae87-8887372dd209">

