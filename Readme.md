# Helper Code For AI Ethics Search Project 

## Importing the packages

If you dont have this package install run the installer


```python
pip install selenium

```

Import the packages


```python
from selenium import webdriver
from webdriver_manager.chrome import ChromeDriverManager 
from selenium.webdriver.chrome.service import Service
import pandas as pd

```

## Company list and KeyPrhase to search

#### When we have the company data we can read it like this and convert to list


```python
df = pd.read_csv('data.csv')  
company_list = df["name"].tolist()
```

#### This is a random list for testing purpose


```python
testList = ["google","facebook","netflix","amazon","alibaba"]
keyprhase = "AI+ethics"
```

#### Split the list into as many chunks as you want for a session


```python
import numpy as np
chunk_num = 3
chunks = np.array_split(testList, chunk_num)

```

## The code

<div class="alert alert-block alert-info">
<b>Warning:</b> You dont need to worry about the code. You can inspect the code, but dont change anything if you arent sure.
</div>


```python
def Auto_search (company_list, keyword, is_bing = True):
    options = webdriver.ChromeOptions()
    options.add_experimental_option("detach", True)
    driver = webdriver.Chrome(options=options,service=Service(ChromeDriverManager().install()))
    current_page=1
    for i,x in enumerate (company_list):
        
        
        driver.get("https://www.google.com/search?as_q=&as_epq="+x+"&as_oq="+keyword+"&as_eq=&as_nlo=&as_nhi=&lr=&cr=&as_qdr=all&as_sitesearch=&as_occt=any&safe=images&as_filetype=&tbs= ")
#         time.sleep(1)
        if is_bing:
            driver.execute_script("window.open('');")
            driver.switch_to.window(driver.window_handles[2*current_page-1])
            driver.get("https://www.bing.com/search?q=google+AI+ethics&form=QBLH&sp=-1&pq="+x+keyword+"&sc=9-16&qs=n&sk=&cvid=F1B69B9DC82042769364838123B11EA8&ghsh=0&ghacc=0&ghpl=")
            driver.execute_script("window.open('');")
            driver.switch_to.window(driver.window_handles[2*current_page])
        else:
            driver.execute_script("window.open('');")
            driver.switch_to.window(driver.window_handles[i+1])
        current_page = current_page+1
    
```

## Call the function

### Run the function. The parameters in serial follows: 

 - Chunks index; Remember index start with 0
 - KeyWords/Phrases; Remeber to add a + in between words and keep it in string
 - Search in Bing; either True or False



```python

Auto_search(chunks[0],keyprhase,True)
```

    
    

    [WDM] - ====== WebDriver manager ======
    [WDM] - Current google-chrome version is 107.0.5304
    [WDM] - Get LATEST chromedriver version for 107.0.5304 google-chrome
    [WDM] - Driver [C:\Users\u\.wdm\drivers\chromedriver\win32\107.0.5304.62\chromedriver.exe] found in cache
   
A separate browser would open like this:

Inline-style: 
![alt text]([https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 1"](https://github.com/sakhawat13/AutoSearch-BCS2Lab-/blob/main/auto_google.jpg))   

Give it some time to load all the tabs. 
There you have it!! 
Next time just change to the next index number when calling the function. 
Best of luck! 
