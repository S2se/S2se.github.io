---
layout: post
title:  "[Project] Feature Extraction: 2. Whirlpool"
date:   2024-08-21 21:03:36 +0900
categories: [Project, Python]
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

Therefore, instead of Whirlpool, I will use Wikipedia. I've decided to use the page for Sydney Observatory, which is my favorite place in Sydney.

```python
import wikipediaapi

wiki = wikipediaapi.Wikipedia(language='en', user_agent='Example/1.0')
page_sydob = wiki.page('Sydney Observatory')
print("Page - Exists: %s" % page_sydob.exists())


extract = wikipediaapi.ExtractFormat.WIKI
print("Page - Full Text: %s" % page_sydob.text)
```
**After run this code, if it is successfully work, you can get this result.**  
:Page - Exists: True  
Page - Full Text: The Sydney Observatory is a heritage-listed meteorological station, astronomical observatory, function venue, science museum, and education facility located on Observatory Hill at Upper Fort Street, in the inner city Sydney suburb of Millers Point in the City of Sydney local government area of New South Wales, Australia. It was designed by William Weaver (plans) and Alexander Dawson (supervision) and built from 1857 to 1859 by Charles Bingemann & Ebenezer Dewar. It is also known as The Sydney Observatory; Observatory; Fort Phillip; Windmill Hill; and Flagstaff Hill. It was added to the New South Wales State Heritage Register on 22 December 2000.
The site was formerly a defence fort, semaphore station, time ball station, meteorological station, observatory and windmills. The site evolved from a fort built on 'Windmill Hill' in the early 19th century to an observatory within the following 100 years. It is now a working museum where evening visitors can observe the stars and planets through a modern 40-centimetre (16 in) Schmidt-Cassegrain telescope and an historic 29-centimetre (11 in) refractor telescope built in 1874, the oldest telescope in Australia in regular use. ...

```python
import wikipediaapi

wiki = wikipediaapi.Wikipedia(user_agent='Example/1.0',language='en')
page_sydob = wiki.page('Sydney Observatory')

with open("sydney_observatory.txt", "w") as f:
    f.write(page_sydob.text)
```

**After run this code, you can find the "sydney_observatory.txt" file inside of your folder.**  
<img width="648" alt="Screenshot 2024-10-02 at 2 37 47 PM" src="https://github.com/user-attachments/assets/20915c3e-d87d-4102-8a80-cd2f87684b26">  
