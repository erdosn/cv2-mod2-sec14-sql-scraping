
### Questions
- Setting up VSCode
- Webscraping???
    - Selenium

### Objectives
YWBAT 
* Explain 'having' in sql
* Explain when to use 'having' vs other sql keywords
* Apply Selenium to scrape some data

### Outline


```python
import requests

import pandas as pd
import numpy as np

from bs4 import BeautifulSoup

import matplotlib.pyplot as plt
```

### What is Selenium
- It's a scraping tool that opens a browser and acts like a human
- Pros:
    - get past bot detection
    - interact with javascript
- Cons:
    - Because it opens a browser, you need to make sure it's running on a system with a monitor
    - A steep learning curve

### Setting Up Selenium
- install ChromeDriver make sure the versions are compatible
- find a tutorial



```python
from selenium import webdriver 
from selenium.webdriver.common.by import By 
from selenium.webdriver.support.ui import WebDriverWait 
from selenium.webdriver.support import expected_conditions as EC 
from selenium.common.exceptions import TimeoutException
import time
```


```python
option = webdriver.ChromeOptions()
option.add_argument("--incognito")
browser = webdriver.Chrome(executable_path="/Users/rafael/Downloads/chromedriver")
```


```python
browser.get("https://www.amazon.com/s?k=oneplus+7t&ref=nb_sb_noss_1")
```

### Clicking Prime Box


```python
checkbox_container = browser.find_element_by_id("primeRefinements")
```


```python
checkbox_container.find_element_by_class_name("a-checkbox").click()
```

### Selecting Review Filter


```python
review_filter_container = browser.find_element_by_id("reviewsRefinements")
```


```python
review_filter_container.find_element_by_class_name("a-unordered-list")
```


    -----------------------------------------------

    StaleElementReferenceExceptionTraceback (most recent call last)

    <ipython-input-72-d7b94fdc565e> in <module>
    ----> 1 review_filter_container.find_element_by_class_name("a-unordered-list")
    

    ~/anaconda3/envs/flatiron-env/lib/python3.6/site-packages/selenium/webdriver/remote/webelement.py in find_element_by_class_name(self, name)
        396             element = element.find_element_by_class_name('foo')
        397         """
    --> 398         return self.find_element(by=By.CLASS_NAME, value=name)
        399 
        400     def find_elements_by_class_name(self, name):


    ~/anaconda3/envs/flatiron-env/lib/python3.6/site-packages/selenium/webdriver/remote/webelement.py in find_element(self, by, value)
        657 
        658         return self._execute(Command.FIND_CHILD_ELEMENT,
    --> 659                              {"using": by, "value": value})['value']
        660 
        661     def find_elements(self, by=By.ID, value=None):


    ~/anaconda3/envs/flatiron-env/lib/python3.6/site-packages/selenium/webdriver/remote/webelement.py in _execute(self, command, params)
        631             params = {}
        632         params['id'] = self._id
    --> 633         return self._parent.execute(command, params)
        634 
        635     def find_element(self, by=By.ID, value=None):


    ~/anaconda3/envs/flatiron-env/lib/python3.6/site-packages/selenium/webdriver/remote/webdriver.py in execute(self, driver_command, params)
        319         response = self.command_executor.execute(driver_command, params)
        320         if response:
    --> 321             self.error_handler.check_response(response)
        322             response['value'] = self._unwrap_value(
        323                 response.get('value', None))


    ~/anaconda3/envs/flatiron-env/lib/python3.6/site-packages/selenium/webdriver/remote/errorhandler.py in check_response(self, response)
        240                 alert_text = value['alert'].get('text')
        241             raise exception_class(message, screen, stacktrace, alert_text)
    --> 242         raise exception_class(message, screen, stacktrace)
        243 
        244     def _value_or_default(self, obj, key, default):


    StaleElementReferenceException: Message: stale element reference: element is not attached to the page document
      (Session info: chrome=77.0.3865.90)




```python

```


```python

```


```python

```


```python
for element in browser.find_elements_by_class_name("a-link-normal"):
    print(element.get_attribute('href'))
```

    https://www.amazon.com/s?k=oneplus+7t&ref=nb_sb_noss_1#s-skipLinkTargetForMainSearchResults
    https://www.amazon.com/s?k=oneplus+7t&rh=p_85%3A2470955011&dc&qid=1570646486&rnid=2470954011&ref=sr_nr_p_85_1
    https://www.amazon.com/s?k=oneplus+7t&rh=p_90%3A8308921011&dc&qid=1570646486&rnid=8308919011&ref=sr_nr_p_90_1
    https://www.amazon.com/s?k=oneplus+7t&rh=p_76%3A2661625011&dc&qid=1570646486&rnid=2661623011&ref=sr_nr_p_76_1
    https://www.amazon.com/s?k=oneplus+7t&rh=n%3A2335752011&dc&qid=1570646486&rnid=2941120011&ref=sr_nr_n_1
    https://www.amazon.com/s?k=oneplus+7t&rh=n%3A2335752011%2Cn%3A2407774011&dc&qid=1570646486&rnid=2941120011&ref=sr_nr_n_2
    https://www.amazon.com/s?k=oneplus+7t&rh=n%3A2335752011%2Cn%3A2407781011&dc&qid=1570646486&rnid=2941120011&ref=sr_nr_n_3
    https://www.amazon.com/s?k=oneplus+7t&rh=n%3A2335752011%2Cn%3A2407765011&dc&qid=1570646486&rnid=2941120011&ref=sr_nr_n_4
    https://www.amazon.com/s?k=oneplus+7t&rh=n%3A2335752011%2Cn%3A9931389011&dc&qid=1570646486&rnid=2941120011&ref=sr_nr_n_5
    https://www.amazon.com/s?k=oneplus+7t&rh=n%3A2335752011%2Cn%3A2407756011&dc&qid=1570646486&rnid=2941120011&ref=sr_nr_n_6
    https://www.amazon.com/s?k=oneplus+7t&rh=n%3A2335752011%2Cn%3A17875443011&dc&qid=1570646486&rnid=2941120011&ref=sr_nr_n_7
    https://www.amazon.com/s?k=oneplus+7t&rh=n%3A2335752011%2Cn%3A12557637011&dc&qid=1570646486&rnid=2941120011&ref=sr_nr_n_8
    https://www.amazon.com/s?k=oneplus+7t&rh=n%3A172282&dc&qid=1570646486&rnid=2941120011&ref=sr_nr_n_9
    https://www.amazon.com/s?k=oneplus+7t&rh=n%3A172282%2Cn%3A12097478011&dc&qid=1570646486&rnid=2941120011&ref=sr_nr_n_10
    https://www.amazon.com/s?k=oneplus+7t&rh=n%3A172282%2Cn%3A2267280011&dc&qid=1570646486&rnid=2941120011&ref=sr_nr_n_11
    https://www.amazon.com/s?k=oneplus+7t&rh=n%3A541966&dc&qid=1570646486&rnid=2941120011&ref=sr_nr_n_12
    https://www.amazon.com/s?k=oneplus+7t&rh=n%3A541966%2Cn%3A2348629011&dc&qid=1570646486&rnid=2941120011&ref=sr_nr_n_13
    https://www.amazon.com/s?k=oneplus+7t&i=automotive&dc&qid=1570646486&ref=sr_nr_i_14
    https://www.amazon.com/s?k=oneplus+7t&i=industrial&dc&qid=1570646486&ref=sr_nr_i_15
    https://www.amazon.com/s?k=oneplus+7t&rh=p_72%3A2661618011&dc&qid=1570646486&rnid=2661617011&ref=sr_nr_p_72_1
    https://www.amazon.com/s?k=oneplus+7t&rh=p_72%3A2661619011&dc&qid=1570646486&rnid=2661617011&ref=sr_nr_p_72_2
    https://www.amazon.com/s?k=oneplus+7t&rh=p_72%3A2661620011&dc&qid=1570646486&rnid=2661617011&ref=sr_nr_p_72_3
    https://www.amazon.com/s?k=oneplus+7t&rh=p_72%3A2661621011&dc&qid=1570646486&rnid=2661617011&ref=sr_nr_p_72_4
    https://www.amazon.com/s?k=oneplus+7t&rh=p_89%3AAGOZ&dc&qid=1570646486&rnid=2528832011&ref=sr_nr_p_89_1
    https://www.amazon.com/s?k=oneplus+7t&rh=p_89%3ATITACUTE&dc&qid=1570646486&rnid=2528832011&ref=sr_nr_p_89_2
    https://www.amazon.com/s?k=oneplus+7t&rh=p_89%3AJiunai&dc&qid=1570646486&rnid=2528832011&ref=sr_nr_p_89_3
    https://www.amazon.com/s?k=oneplus+7t&rh=p_89%3AJelanry&dc&qid=1570646486&rnid=2528832011&ref=sr_nr_p_89_4
    https://www.amazon.com/s?k=oneplus+7t&rh=p_89%3AIVSO&dc&qid=1570646486&rnid=2528832011&ref=sr_nr_p_89_5
    https://www.amazon.com/s?k=oneplus+7t&rh=p_89%3ASupershieldz&dc&qid=1570646486&rnid=2528832011&ref=sr_nr_p_89_6
    https://www.amazon.com/s?k=oneplus+7t&rh=p_89%3ASLEO&dc&qid=1570646486&rnid=2528832011&ref=sr_nr_p_89_7
    https://www.amazon.com/s?k=oneplus+7t&rh=p_89%3ALankXin&dc&qid=1570646486&rnid=2528832011&ref=sr_nr_p_89_8
    https://www.amazon.com/s?k=oneplus+7t&rh=p_89%3ATamoria&dc&qid=1570646486&rnid=2528832011&ref=sr_nr_p_89_9
    https://www.amazon.com/s?k=oneplus+7t&rh=p_89%3ACOOYA&dc&qid=1570646486&rnid=2528832011&ref=sr_nr_p_89_10
    https://www.amazon.com/s?k=oneplus+7t&rh=p_89%3AIFCASE&dc&qid=1570646486&rnid=2528832011&ref=sr_nr_p_89_11
    https://www.amazon.com/s?k=oneplus+7t&rh=p_89%3AiMangoo&dc&qid=1570646486&rnid=2528832011&ref=sr_nr_p_89_12
    https://www.amazon.com/s?k=oneplus+7t&rh=p_n_feature_nine_browse-bin%3A15284134011&dc&qid=1570646486&rnid=2488708011&ref=sr_nr_p_n_feature_nine_browse-bin_4
    https://www.amazon.com/s?k=oneplus+7t&rh=p_n_feature_nine_browse-bin%3A10030581011&dc&qid=1570646486&rnid=2488708011&ref=sr_nr_p_n_feature_nine_browse-bin_6
    https://www.amazon.com/s?k=oneplus+7t&rh=p_n_feature_nine_browse-bin%3A7079349011&dc&qid=1570646486&rnid=2488708011&ref=sr_nr_p_n_feature_nine_browse-bin_8
    https://www.amazon.com/s?k=oneplus+7t&rh=n%3A2407760011%2Cp_n_feature_four_browse-bin%3A17875444011&dc&qid=1570646486&rnid=11269698011&ref=sr_nr_p_n_feature_four_browse-bin_1
    https://www.amazon.com/s?k=oneplus+7t&rh=n%3A2407760011%2Cp_n_feature_four_browse-bin%3A11269700011&dc&qid=1570646486&rnid=11269698011&ref=sr_nr_p_n_feature_four_browse-bin_2
    https://www.amazon.com/s?k=oneplus+7t&rh=n%3A2407760011%2Cp_n_feature_four_browse-bin%3A17875446011&dc&qid=1570646486&rnid=11269698011&ref=sr_nr_p_n_feature_four_browse-bin_3
    https://www.amazon.com/s?k=oneplus+7t&rh=n%3A2407760011%2Cp_n_feature_ten_browse-bin%3A17731926011&dc&qid=1570646486&rnid=11043306011&ref=sr_nr_p_n_feature_ten_browse-bin_1
    https://www.amazon.com/s?k=oneplus+7t&rh=n%3A2407760011%2Cp_n_feature_ten_browse-bin%3A17731933011&dc&qid=1570646486&rnid=11043306011&ref=sr_nr_p_n_feature_ten_browse-bin_2
    https://www.amazon.com/s?k=oneplus+7t&rh=n%3A2407760011%2Cp_n_feature_ten_browse-bin%3A17731930011&dc&qid=1570646486&rnid=11043306011&ref=sr_nr_p_n_feature_ten_browse-bin_3
    https://www.amazon.com/s?k=oneplus+7t&rh=n%3A2407760011%2Cp_n_feature_ten_browse-bin%3A11043312011&dc&qid=1570646486&rnid=11043306011&ref=sr_nr_p_n_feature_ten_browse-bin_4
    https://www.amazon.com/s?k=oneplus+7t&rh=n%3A172541%2Cp_n_feature_two_browse-bin%3A2266981011&dc&qid=1570646486&rnid=2266979011&ref=sr_nr_p_n_feature_two_browse-bin_1
    https://www.amazon.com/s?k=oneplus+7t&rh=n%3A172541%2Cp_n_feature_two_browse-bin%3A12097494011&dc&qid=1570646486&rnid=2266979011&ref=sr_nr_p_n_feature_two_browse-bin_2
    https://www.amazon.com/s?k=oneplus+7t&rh=n%3A172541%2Cp_n_feature_two_browse-bin%3A509318&dc&qid=1570646486&rnid=2266979011&ref=sr_nr_p_n_feature_two_browse-bin_3
    https://www.amazon.com/s?k=oneplus+7t&rh=n%3A172541%2Cp_n_feature_two_browse-bin%3A509316&dc&qid=1570646486&rnid=2266979011&ref=sr_nr_p_n_feature_two_browse-bin_4
    https://www.amazon.com/s?k=oneplus+7t&rh=n%3A172541%2Cp_n_feature_four_browse-bin%3A12097501011&dc&qid=1570646486&rnid=12097500011&ref=sr_nr_p_n_feature_four_browse-bin_1
    https://www.amazon.com/s?k=oneplus+7t&rh=n%3A541966%2Cp_n_size_browse-bin%3A7817238011&dc&qid=1570646486&rnid=1254615011&ref=sr_nr_p_n_size_browse-bin_4
    https://www.amazon.com/s?k=oneplus+7t&rh=p_n_shipping_option-bin%3A3242350011&dc&qid=1570646486&rnid=2944662011&ref=sr_nr_p_n_shipping_option-bin_1
    https://www.amazon.com/s?k=oneplus+7t&rh=p_n_condition-type%3A6461716011&dc&qid=1570646486&rnid=6461714011&ref=sr_nr_p_n_condition-type_1
    https://www.amazon.com/s?k=oneplus+7t&rh=p_n_condition-type%3A6461718011&dc&qid=1570646486&rnid=6461714011&ref=sr_nr_p_n_condition-type_2
    https://www.amazon.com/OnePlus-GM1900-Unlocked-International-Warranty/dp/B07RFWG93C/ref=sr_1_1?keywords=oneplus+7t&qid=1570646486&sr=8-1
    https://www.amazon.com/OnePlus-GM1900-Unlocked-International-Warranty/dp/B07RFWG93C/ref=sr_1_1?keywords=oneplus+7t&qid=1570646486&sr=8-1
    https://www.amazon.com/OnePlus-GM1900-Unlocked-International-Warranty/dp/B07RFWG93C/ref=sr_1_1?keywords=oneplus+7t&qid=1570646486&sr=8-1#customerReviews
    https://www.amazon.com/OnePlus-GM1900-Unlocked-International-Warranty/dp/B07RFWG93C/ref=sr_1_1?keywords=oneplus+7t&qid=1570646486&sr=8-1
    https://www.amazon.com/gp/offer-listing/B07RFWG93C
    https://www.amazon.com/Oneplus-GM1910-Unlocked-International-Warranty/dp/B07SD7Z3J7/ref=sr_1_2?keywords=oneplus+7t&qid=1570646486&sr=8-2
    https://www.amazon.com/Oneplus-GM1910-Unlocked-International-Warranty/dp/B07SD7Z3J7/ref=sr_1_2?keywords=oneplus+7t&qid=1570646486&sr=8-2
    https://www.amazon.com/Oneplus-GM1910-Unlocked-International-Warranty/dp/B07SD7Z3J7/ref=sr_1_2?keywords=oneplus+7t&qid=1570646486&sr=8-2#customerReviews
    https://www.amazon.com/Oneplus-GM1910-Unlocked-International-Warranty/dp/B07SD7Z3J7/ref=sr_1_2?keywords=oneplus+7t&qid=1570646486&sr=8-2
    https://www.amazon.com/gp/offer-listing/B07SD7Z3J7
    https://www.amazon.com/Google-Pixel-Memory-Unlocked-Clearly/dp/B07R9PTDTZ/ref=sr_1_3?keywords=oneplus+7t&qid=1570646486&sr=8-3
    https://www.amazon.com/Google-Pixel-Memory-Unlocked-Clearly/dp/B07R9PTDTZ/ref=sr_1_3?keywords=oneplus+7t&qid=1570646486&sr=8-3
    https://www.amazon.com/Google-Pixel-Memory-Unlocked-Clearly/dp/B07R9PTDTZ/ref=sr_1_3?keywords=oneplus+7t&qid=1570646486&sr=8-3#customerReviews
    https://www.amazon.com/Google-Pixel-Memory-Unlocked-Clearly/dp/B07R9PTDTZ/ref=sr_1_3?keywords=oneplus+7t&qid=1570646486&sr=8-3
    https://www.amazon.com/gp/offer-listing/B07R9PTDTZ
    https://www.amazon.com/OnePlus-A6013-128GB-Mirror-Black/dp/B07V3TL48P/ref=sr_1_4?keywords=oneplus+7t&qid=1570646486&sr=8-4
    https://www.amazon.com/OnePlus-A6013-128GB-Mirror-Black/dp/B07V3TL48P/ref=sr_1_4?keywords=oneplus+7t&qid=1570646486&sr=8-4
    https://www.amazon.com/OnePlus-A6013-128GB-Mirror-Black/dp/B07V3TL48P/ref=sr_1_4?keywords=oneplus+7t&qid=1570646486&sr=8-4#customerReviews
    https://www.amazon.com/OnePlus-A6013-128GB-Mirror-Black/dp/B07V3TL48P/ref=sr_1_4?keywords=oneplus+7t&qid=1570646486&sr=8-4
    https://www.amazon.com/OnePlus-Unlocked-International-Warranty-Mirror/dp/B07L395DB4/ref=sr_1_5?keywords=oneplus+7t&qid=1570646486&sr=8-5
    https://www.amazon.com/OnePlus-Unlocked-International-Warranty-Mirror/dp/B07L395DB4/ref=sr_1_5?keywords=oneplus+7t&qid=1570646486&sr=8-5
    https://www.amazon.com/OnePlus-Unlocked-International-Warranty-Mirror/dp/B07L395DB4/ref=sr_1_5?keywords=oneplus+7t&qid=1570646486&sr=8-5#customerReviews
    https://www.amazon.com/OnePlus-Unlocked-International-Warranty-Mirror/dp/B07L395DB4/ref=sr_1_5?keywords=oneplus+7t&qid=1570646486&sr=8-5
    https://www.amazon.com/gp/offer-listing/B07L395DB4
    https://www.amazon.com/OnePlus-Factory-Unlocked-Verizon-Tmobile/dp/B07RCXCPV5/ref=sr_1_6?keywords=oneplus+7t&qid=1570646486&sr=8-6
    https://www.amazon.com/OnePlus-Factory-Unlocked-Verizon-Tmobile/dp/B07RCXCPV5/ref=sr_1_6?keywords=oneplus+7t&qid=1570646486&sr=8-6
    https://www.amazon.com/OnePlus-Factory-Unlocked-Verizon-Tmobile/dp/B07RCXCPV5/ref=sr_1_6?keywords=oneplus+7t&qid=1570646486&sr=8-6#customerReviews
    https://www.amazon.com/OnePlus-Factory-Unlocked-Verizon-Tmobile/dp/B07RCXCPV5/ref=sr_1_6?keywords=oneplus+7t&qid=1570646486&sr=8-6
    https://www.amazon.com/OnePlus-Storage-Memory-Display-Android/dp/B07RYBGNDQ/ref=sr_1_7?keywords=oneplus+7t&qid=1570646486&sr=8-7
    https://www.amazon.com/OnePlus-Storage-Memory-Display-Android/dp/B07RYBGNDQ/ref=sr_1_7?keywords=oneplus+7t&qid=1570646486&sr=8-7
    https://www.amazon.com/OnePlus-Storage-Memory-Display-Android/dp/B07RYBGNDQ/ref=sr_1_7?keywords=oneplus+7t&qid=1570646486&sr=8-7#customerReviews
    https://www.amazon.com/OnePlus-Storage-Memory-Display-Android/dp/B07RYBGNDQ/ref=sr_1_7?keywords=oneplus+7t&qid=1570646486&sr=8-7
    https://www.amazon.com/OnePlus-A6013-128GB-Mirror-Black/dp/B07PQSYGKB/ref=sr_1_8?keywords=oneplus+7t&qid=1570646486&sr=8-8
    https://www.amazon.com/OnePlus-A6013-128GB-Mirror-Black/dp/B07PQSYGKB/ref=sr_1_8?keywords=oneplus+7t&qid=1570646486&sr=8-8
    https://www.amazon.com/OnePlus-A6013-128GB-Mirror-Black/dp/B07PQSYGKB/ref=sr_1_8?keywords=oneplus+7t&qid=1570646486&sr=8-8#customerReviews
    https://www.amazon.com/OnePlus-A6013-128GB-Mirror-Black/dp/B07PQSYGKB/ref=sr_1_8?keywords=oneplus+7t&qid=1570646486&sr=8-8
    https://www.amazon.com/gp/slredirect/picassoRedirect.html/ref=pa_sp_mtf_aps_sr_pg1_1?ie=UTF8&adId=A080421727U4LF9HH4QHU&url=%2FColorful-OnePlus-Ultra-Thin-Premium-Material%2Fdp%2FB07XXRZFL8%2Fref%3Dsr_1_9_sspa%3Fkeywords%3Doneplus%2B7t%26qid%3D1570646486%26sr%3D8-9-spons%26psc%3D1&qualifier=1570646485&id=8566210519729588&widgetName=sp_mtf
    https://advertising.amazon.com/products-self-serve?ref_=ext_amzn_wtsp
    https://www.amazon.com/s?k=oneplus+7t&ref=nb_sb_noss_1#
    https://www.amazon.com/gp/slredirect/picassoRedirect.html/ref=pa_sp_mtf_aps_sr_pg1_1?ie=UTF8&adId=A080421727U4LF9HH4QHU&url=%2FColorful-OnePlus-Ultra-Thin-Premium-Material%2Fdp%2FB07XXRZFL8%2Fref%3Dsr_1_9_sspa%3Fkeywords%3Doneplus%2B7t%26qid%3D1570646486%26sr%3D8-9-spons%26psc%3D1&qualifier=1570646485&id=8566210519729588&widgetName=sp_mtf
    https://www.amazon.com/gp/slredirect/picassoRedirect.html/ref=pa_sp_mtf_aps_sr_pg1_1?ie=UTF8&adId=A080421727U4LF9HH4QHU&url=%2FColorful-OnePlus-Ultra-Thin-Premium-Material%2Fdp%2FB07XXRZFL8%2Fref%3Dsr_1_9_sspa%3Fkeywords%3Doneplus%2B7t%26qid%3D1570646486%26sr%3D8-9-spons%26psc%3D1&qualifier=1570646485&id=8566210519729588&widgetName=sp_mtf
    https://www.amazon.com/gp/slredirect/picassoRedirect.html/ref=pa_sp_mtf_aps_sr_pg1_2?ie=UTF8&adId=A06733252BLH3NDLAGVS5&url=%2FPack-OnePlus-Screen-Protector-Definition%2Fdp%2FB07XCT1KKK%2Fref%3Dsr_1_10_sspa%3Fkeywords%3Doneplus%2B7t%26qid%3D1570646486%26sr%3D8-10-spons%26psc%3D1&qualifier=1570646485&id=8566210519729588&widgetName=sp_mtf
    https://advertising.amazon.com/products-self-serve?ref_=ext_amzn_wtsp
    https://www.amazon.com/s?k=oneplus+7t&ref=nb_sb_noss_1#
    https://www.amazon.com/gp/slredirect/picassoRedirect.html/ref=pa_sp_mtf_aps_sr_pg1_2?ie=UTF8&adId=A06733252BLH3NDLAGVS5&url=%2FPack-OnePlus-Screen-Protector-Definition%2Fdp%2FB07XCT1KKK%2Fref%3Dsr_1_10_sspa%3Fkeywords%3Doneplus%2B7t%26qid%3D1570646486%26sr%3D8-10-spons%26psc%3D1&qualifier=1570646485&id=8566210519729588&widgetName=sp_mtf
    https://www.amazon.com/gp/slredirect/picassoRedirect.html/ref=pa_sp_mtf_aps_sr_pg1_2?ie=UTF8&adId=A06733252BLH3NDLAGVS5&url=%2FPack-OnePlus-Screen-Protector-Definition%2Fdp%2FB07XCT1KKK%2Fref%3Dsr_1_10_sspa%3Fkeywords%3Doneplus%2B7t%26qid%3D1570646486%26sr%3D8-10-spons%26psc%3D1&qualifier=1570646485&id=8566210519729588&widgetName=sp_mtf#customerReviews
    https://www.amazon.com/gp/slredirect/picassoRedirect.html/ref=pa_sp_mtf_aps_sr_pg1_2?ie=UTF8&adId=A06733252BLH3NDLAGVS5&url=%2FPack-OnePlus-Screen-Protector-Definition%2Fdp%2FB07XCT1KKK%2Fref%3Dsr_1_10_sspa%3Fkeywords%3Doneplus%2B7t%26qid%3D1570646486%26sr%3D8-10-spons%26psc%3D1&qualifier=1570646485&id=8566210519729588&widgetName=sp_mtf
    https://www.amazon.com/Moto-Alexa-Hands-Free-camera-included/dp/B07N9255CG/ref=sr_1_11?keywords=oneplus+7t&qid=1570646486&sr=8-11
    https://www.amazon.com/Moto-Alexa-Hands-Free-camera-included/dp/B07N9255CG/ref=sr_1_11?keywords=oneplus+7t&qid=1570646486&sr=8-11
    https://www.amazon.com/Moto-Alexa-Hands-Free-camera-included/dp/B07N9255CG/ref=sr_1_11?keywords=oneplus+7t&qid=1570646486&sr=8-11#customerReviews
    https://www.amazon.com/Moto-Alexa-Hands-Free-camera-included/dp/B07N9255CG/ref=sr_1_11?keywords=oneplus+7t&qid=1570646486&sr=8-11
    https://www.amazon.com/gp/offer-listing/B07N9255CG
    https://www.amazon.com/ASUS-ZenFone-5Z-ZS620KL-S845-6G64G-2160x1080/dp/B07CLWGC3T/ref=sr_1_12?keywords=oneplus+7t&qid=1570646486&sr=8-12
    https://www.amazon.com/ASUS-ZenFone-5Z-ZS620KL-S845-6G64G-2160x1080/dp/B07CLWGC3T/ref=sr_1_12?keywords=oneplus+7t&qid=1570646486&sr=8-12
    https://www.amazon.com/ASUS-ZenFone-5Z-ZS620KL-S845-6G64G-2160x1080/dp/B07CLWGC3T/ref=sr_1_12?keywords=oneplus+7t&qid=1570646486&sr=8-12#customerReviews
    https://www.amazon.com/ASUS-ZenFone-5Z-ZS620KL-S845-6G64G-2160x1080/dp/B07CLWGC3T/ref=sr_1_12?keywords=oneplus+7t&qid=1570646486&sr=8-12
    https://www.amazon.com/OnePlus-Unlocked-International-Warranty-Midnight/dp/B07Q1K5VHS/ref=sr_1_13?keywords=oneplus+7t&qid=1570646486&sr=8-13
    https://www.amazon.com/OnePlus-Unlocked-International-Warranty-Midnight/dp/B07Q1K5VHS/ref=sr_1_13?keywords=oneplus+7t&qid=1570646486&sr=8-13
    https://www.amazon.com/OnePlus-Unlocked-International-Warranty-Midnight/dp/B07Q1K5VHS/ref=sr_1_13?keywords=oneplus+7t&qid=1570646486&sr=8-13#customerReviews
    https://www.amazon.com/OnePlus-Unlocked-International-Warranty-Midnight/dp/B07Q1K5VHS/ref=sr_1_13?keywords=oneplus+7t&qid=1570646486&sr=8-13
    https://www.amazon.com/OnePlus-Unlocked-International-Model-GSM-Networks/dp/B07SNFSS4L/ref=sr_1_14?keywords=oneplus+7t&qid=1570646486&sr=8-14
    https://www.amazon.com/OnePlus-Unlocked-International-Model-GSM-Networks/dp/B07SNFSS4L/ref=sr_1_14?keywords=oneplus+7t&qid=1570646486&sr=8-14
    https://www.amazon.com/OnePlus-Unlocked-International-Model-GSM-Networks/dp/B07SNFSS4L/ref=sr_1_14?keywords=oneplus+7t&qid=1570646486&sr=8-14#customerReviews
    https://www.amazon.com/OnePlus-Unlocked-International-Model-GSM-Networks/dp/B07SNFSS4L/ref=sr_1_14?keywords=oneplus+7t&qid=1570646486&sr=8-14
    https://www.amazon.com/Colorful-OnePlus-Ultra-Thin-Premium-Material/dp/B07XXS81MN/ref=sr_1_15?keywords=oneplus+7t&qid=1570646486&sr=8-15
    https://www.amazon.com/Colorful-OnePlus-Ultra-Thin-Premium-Material/dp/B07XXS81MN/ref=sr_1_15?keywords=oneplus+7t&qid=1570646486&sr=8-15
    https://www.amazon.com/Colorful-OnePlus-Ultra-Thin-Premium-Material/dp/B07XXS81MN/ref=sr_1_15?keywords=oneplus+7t&qid=1570646486&sr=8-15
    https://www.amazon.com/Pack-OnePlus-Screen-Protector-Definition/dp/B07XCT1KKK/ref=sr_1_16?keywords=oneplus+7t&qid=1570646486&sr=8-16
    https://www.amazon.com/Pack-OnePlus-Screen-Protector-Definition/dp/B07XCT1KKK/ref=sr_1_16?keywords=oneplus+7t&qid=1570646486&sr=8-16
    https://www.amazon.com/Pack-OnePlus-Screen-Protector-Definition/dp/B07XCT1KKK/ref=sr_1_16?keywords=oneplus+7t&qid=1570646486&sr=8-16#customerReviews
    https://www.amazon.com/Pack-OnePlus-Screen-Protector-Definition/dp/B07XCT1KKK/ref=sr_1_16?keywords=oneplus+7t&qid=1570646486&sr=8-16
    https://www.amazon.com/Protector-SPARIN-Tempered-Definition-Resistance/dp/B07XBQC3LK/ref=sr_1_17?keywords=oneplus+7t&qid=1570646486&sr=8-17
    https://www.amazon.com/Protector-SPARIN-Tempered-Definition-Resistance/dp/B07XBQC3LK/ref=sr_1_17?keywords=oneplus+7t&qid=1570646486&sr=8-17
    https://www.amazon.com/Protector-SPARIN-Tempered-Definition-Resistance/dp/B07XBQC3LK/ref=sr_1_17?keywords=oneplus+7t&qid=1570646486&sr=8-17
    https://www.amazon.com/PULEN-Protector-Anti-Scratch-Hardness-Replacement/dp/B07R1Q3LTY/ref=sr_1_18?keywords=oneplus+7t&qid=1570646486&sr=8-18
    https://www.amazon.com/PULEN-Protector-Anti-Scratch-Hardness-Replacement/dp/B07R1Q3LTY/ref=sr_1_18?keywords=oneplus+7t&qid=1570646486&sr=8-18
    https://www.amazon.com/PULEN-Protector-Anti-Scratch-Hardness-Replacement/dp/B07R1Q3LTY/ref=sr_1_18?keywords=oneplus+7t&qid=1570646486&sr=8-18#customerReviews
    https://www.amazon.com/PULEN-Protector-Anti-Scratch-Hardness-Replacement/dp/B07R1Q3LTY/ref=sr_1_18?keywords=oneplus+7t&qid=1570646486&sr=8-18
    https://www.amazon.com/gp/slredirect/picassoRedirect.html/ref=pa_sp_btf_aps_sr_pg1_1?ie=UTF8&adId=A09865291U08NQKMHKZ7V&url=%2FOnePlus-Almiao-Ultra-Thin-Minimalist-Protective%2Fdp%2FB07Y4DXV3W%2Fref%3Dsr_1_19_sspa%3Fkeywords%3Doneplus%2B7t%26qid%3D1570646486%26sr%3D8-19-spons%26psc%3D1&qualifier=1570646485&id=8566210519729588&widgetName=sp_btf
    https://advertising.amazon.com/products-self-serve?ref_=ext_amzn_wtsp
    https://www.amazon.com/s?k=oneplus+7t&ref=nb_sb_noss_1#
    https://www.amazon.com/gp/slredirect/picassoRedirect.html/ref=pa_sp_btf_aps_sr_pg1_1?ie=UTF8&adId=A09865291U08NQKMHKZ7V&url=%2FOnePlus-Almiao-Ultra-Thin-Minimalist-Protective%2Fdp%2FB07Y4DXV3W%2Fref%3Dsr_1_19_sspa%3Fkeywords%3Doneplus%2B7t%26qid%3D1570646486%26sr%3D8-19-spons%26psc%3D1&qualifier=1570646485&id=8566210519729588&widgetName=sp_btf
    https://www.amazon.com/gp/slredirect/picassoRedirect.html/ref=pa_sp_btf_aps_sr_pg1_1?ie=UTF8&adId=A09865291U08NQKMHKZ7V&url=%2FOnePlus-Almiao-Ultra-Thin-Minimalist-Protective%2Fdp%2FB07Y4DXV3W%2Fref%3Dsr_1_19_sspa%3Fkeywords%3Doneplus%2B7t%26qid%3D1570646486%26sr%3D8-19-spons%26psc%3D1&qualifier=1570646485&id=8566210519729588&widgetName=sp_btf
    https://www.amazon.com/gp/slredirect/picassoRedirect.html/ref=pa_sp_btf_aps_sr_pg1_2?ie=UTF8&adId=A08082841CTBTBXVOLSRF&url=%2FRhinoShield-SolidSuit-Absorbent-Protective-Protection%2Fdp%2FB07S6NG5PM%2Fref%3Dsr_1_20_sspa%3Fkeywords%3Doneplus%2B7t%26qid%3D1570646486%26sr%3D8-20-spons%26psc%3D1&qualifier=1570646485&id=8566210519729588&widgetName=sp_btf
    https://advertising.amazon.com/products-self-serve?ref_=ext_amzn_wtsp
    https://www.amazon.com/s?k=oneplus+7t&ref=nb_sb_noss_1#
    https://www.amazon.com/gp/slredirect/picassoRedirect.html/ref=pa_sp_btf_aps_sr_pg1_2?ie=UTF8&adId=A08082841CTBTBXVOLSRF&url=%2FRhinoShield-SolidSuit-Absorbent-Protective-Protection%2Fdp%2FB07S6NG5PM%2Fref%3Dsr_1_20_sspa%3Fkeywords%3Doneplus%2B7t%26qid%3D1570646486%26sr%3D8-20-spons%26psc%3D1&qualifier=1570646485&id=8566210519729588&widgetName=sp_btf
    https://www.amazon.com/gp/slredirect/picassoRedirect.html/ref=pa_sp_btf_aps_sr_pg1_2?ie=UTF8&adId=A08082841CTBTBXVOLSRF&url=%2FRhinoShield-SolidSuit-Absorbent-Protective-Protection%2Fdp%2FB07S6NG5PM%2Fref%3Dsr_1_20_sspa%3Fkeywords%3Doneplus%2B7t%26qid%3D1570646486%26sr%3D8-20-spons%26psc%3D1&qualifier=1570646485&id=8566210519729588&widgetName=sp_btf#customerReviews
    https://www.amazon.com/gp/slredirect/picassoRedirect.html/ref=pa_sp_btf_aps_sr_pg1_2?ie=UTF8&adId=A08082841CTBTBXVOLSRF&url=%2FRhinoShield-SolidSuit-Absorbent-Protective-Protection%2Fdp%2FB07S6NG5PM%2Fref%3Dsr_1_20_sspa%3Fkeywords%3Doneplus%2B7t%26qid%3D1570646486%26sr%3D8-20-spons%26psc%3D1&qualifier=1570646485&id=8566210519729588&widgetName=sp_btf
    https://www.amazon.com/gp/slredirect/picassoRedirect.html/ref=pa_sp_btf_aps_sr_pg1_3?ie=UTF8&adId=A023913333ES3MWQ7A1ZL&url=%2FRhinoShield-CrashGuard-Absorbent-Protective-Protection%2Fdp%2FB07S9RVTWF%2Fref%3Dsr_1_21_sspa%3Fkeywords%3Doneplus%2B7t%26qid%3D1570646486%26sr%3D8-21-spons%26psc%3D1&qualifier=1570646485&id=8566210519729588&widgetName=sp_btf
    https://advertising.amazon.com/products-self-serve?ref_=ext_amzn_wtsp
    https://www.amazon.com/s?k=oneplus+7t&ref=nb_sb_noss_1#
    https://www.amazon.com/gp/slredirect/picassoRedirect.html/ref=pa_sp_btf_aps_sr_pg1_3?ie=UTF8&adId=A023913333ES3MWQ7A1ZL&url=%2FRhinoShield-CrashGuard-Absorbent-Protective-Protection%2Fdp%2FB07S9RVTWF%2Fref%3Dsr_1_21_sspa%3Fkeywords%3Doneplus%2B7t%26qid%3D1570646486%26sr%3D8-21-spons%26psc%3D1&qualifier=1570646485&id=8566210519729588&widgetName=sp_btf
    https://www.amazon.com/gp/slredirect/picassoRedirect.html/ref=pa_sp_btf_aps_sr_pg1_3?ie=UTF8&adId=A023913333ES3MWQ7A1ZL&url=%2FRhinoShield-CrashGuard-Absorbent-Protective-Protection%2Fdp%2FB07S9RVTWF%2Fref%3Dsr_1_21_sspa%3Fkeywords%3Doneplus%2B7t%26qid%3D1570646486%26sr%3D8-21-spons%26psc%3D1&qualifier=1570646485&id=8566210519729588&widgetName=sp_btf#customerReviews
    https://www.amazon.com/gp/slredirect/picassoRedirect.html/ref=pa_sp_btf_aps_sr_pg1_3?ie=UTF8&adId=A023913333ES3MWQ7A1ZL&url=%2FRhinoShield-CrashGuard-Absorbent-Protective-Protection%2Fdp%2FB07S9RVTWF%2Fref%3Dsr_1_21_sspa%3Fkeywords%3Doneplus%2B7t%26qid%3D1570646486%26sr%3D8-21-spons%26psc%3D1&qualifier=1570646485&id=8566210519729588&widgetName=sp_btf
    https://www.amazon.com/gp/slredirect/picassoRedirect.html/ref=pa_sp_btf_aps_sr_pg1_4?ie=UTF8&adId=A07537452AE02Q8A9DQKY&url=%2FOnePlus-Almiao-Ultra-Thin-Minimalist-Protective%2Fdp%2FB07Y4VHSFF%2Fref%3Dsr_1_22_sspa%3Fkeywords%3Doneplus%2B7t%26qid%3D1570646486%26sr%3D8-22-spons%26psc%3D1&qualifier=1570646485&id=8566210519729588&widgetName=sp_btf
    https://advertising.amazon.com/products-self-serve?ref_=ext_amzn_wtsp
    https://www.amazon.com/s?k=oneplus+7t&ref=nb_sb_noss_1#
    https://www.amazon.com/gp/slredirect/picassoRedirect.html/ref=pa_sp_btf_aps_sr_pg1_4?ie=UTF8&adId=A07537452AE02Q8A9DQKY&url=%2FOnePlus-Almiao-Ultra-Thin-Minimalist-Protective%2Fdp%2FB07Y4VHSFF%2Fref%3Dsr_1_22_sspa%3Fkeywords%3Doneplus%2B7t%26qid%3D1570646486%26sr%3D8-22-spons%26psc%3D1&qualifier=1570646485&id=8566210519729588&widgetName=sp_btf
    https://www.amazon.com/gp/slredirect/picassoRedirect.html/ref=pa_sp_btf_aps_sr_pg1_4?ie=UTF8&adId=A07537452AE02Q8A9DQKY&url=%2FOnePlus-Almiao-Ultra-Thin-Minimalist-Protective%2Fdp%2FB07Y4VHSFF%2Fref%3Dsr_1_22_sspa%3Fkeywords%3Doneplus%2B7t%26qid%3D1570646486%26sr%3D8-22-spons%26psc%3D1&qualifier=1570646485&id=8566210519729588&widgetName=sp_btf
    https://www.amazon.com/s/?k=oneplus+7t+pro&ref=sugsr_0&pd_rd_w=CSMhL&pf_rd_p=7be70e42-b5c0-4077-873a-35a472a6fbd4&pf_rd_r=GDWNZNBEYPC55GHGM9MM&pd_rd_r=a4cf0659-cf29-4df5-8f0a-6e32e6c57a29&pd_rd_wg=gzED3&qid=1570646486
    https://www.amazon.com/s/?k=oneplus+7t+pro&ref=sugsr_0&pd_rd_w=CSMhL&pf_rd_p=7be70e42-b5c0-4077-873a-35a472a6fbd4&pf_rd_r=GDWNZNBEYPC55GHGM9MM&pd_rd_r=a4cf0659-cf29-4df5-8f0a-6e32e6c57a29&pd_rd_wg=gzED3&qid=1570646486
    https://www.amazon.com/s/?k=oneplus+7t+pro+phone&ref=sugsr_1&pd_rd_w=CSMhL&pf_rd_p=7be70e42-b5c0-4077-873a-35a472a6fbd4&pf_rd_r=GDWNZNBEYPC55GHGM9MM&pd_rd_r=a4cf0659-cf29-4df5-8f0a-6e32e6c57a29&pd_rd_wg=gzED3&qid=1570646486
    https://www.amazon.com/s/?k=oneplus+7t+pro+phone&ref=sugsr_1&pd_rd_w=CSMhL&pf_rd_p=7be70e42-b5c0-4077-873a-35a472a6fbd4&pf_rd_r=GDWNZNBEYPC55GHGM9MM&pd_rd_r=a4cf0659-cf29-4df5-8f0a-6e32e6c57a29&pd_rd_wg=gzED3&qid=1570646486
    https://www.amazon.com/s/?k=oneplus+7&ref=sugsr_2&pd_rd_w=CSMhL&pf_rd_p=7be70e42-b5c0-4077-873a-35a472a6fbd4&pf_rd_r=GDWNZNBEYPC55GHGM9MM&pd_rd_r=a4cf0659-cf29-4df5-8f0a-6e32e6c57a29&pd_rd_wg=gzED3&qid=1570646486
    https://www.amazon.com/s/?k=oneplus+7&ref=sugsr_2&pd_rd_w=CSMhL&pf_rd_p=7be70e42-b5c0-4077-873a-35a472a6fbd4&pf_rd_r=GDWNZNBEYPC55GHGM9MM&pd_rd_r=a4cf0659-cf29-4df5-8f0a-6e32e6c57a29&pd_rd_wg=gzED3&qid=1570646486
    https://www.amazon.com/s/?k=oneplus+7+pro&ref=sugsr_3&pd_rd_w=CSMhL&pf_rd_p=7be70e42-b5c0-4077-873a-35a472a6fbd4&pf_rd_r=GDWNZNBEYPC55GHGM9MM&pd_rd_r=a4cf0659-cf29-4df5-8f0a-6e32e6c57a29&pd_rd_wg=gzED3&qid=1570646486
    https://www.amazon.com/s/?k=oneplus+7+pro&ref=sugsr_3&pd_rd_w=CSMhL&pf_rd_p=7be70e42-b5c0-4077-873a-35a472a6fbd4&pf_rd_r=GDWNZNBEYPC55GHGM9MM&pd_rd_r=a4cf0659-cf29-4df5-8f0a-6e32e6c57a29&pd_rd_wg=gzED3&qid=1570646486
    https://www.amazon.com/s/?k=one+plus+7t&ref=sugsr_4&pd_rd_w=CSMhL&pf_rd_p=7be70e42-b5c0-4077-873a-35a472a6fbd4&pf_rd_r=GDWNZNBEYPC55GHGM9MM&pd_rd_r=a4cf0659-cf29-4df5-8f0a-6e32e6c57a29&pd_rd_wg=gzED3&qid=1570646486
    https://www.amazon.com/s/?k=one+plus+7t&ref=sugsr_4&pd_rd_w=CSMhL&pf_rd_p=7be70e42-b5c0-4077-873a-35a472a6fbd4&pf_rd_r=GDWNZNBEYPC55GHGM9MM&pd_rd_r=a4cf0659-cf29-4df5-8f0a-6e32e6c57a29&pd_rd_wg=gzED3&qid=1570646486
    https://www.amazon.com/s/?k=oneplus+7+t&ref=sugsr_5&pd_rd_w=CSMhL&pf_rd_p=7be70e42-b5c0-4077-873a-35a472a6fbd4&pf_rd_r=GDWNZNBEYPC55GHGM9MM&pd_rd_r=a4cf0659-cf29-4df5-8f0a-6e32e6c57a29&pd_rd_wg=gzED3&qid=1570646486
    https://www.amazon.com/s/?k=oneplus+7+t&ref=sugsr_5&pd_rd_w=CSMhL&pf_rd_p=7be70e42-b5c0-4077-873a-35a472a6fbd4&pf_rd_r=GDWNZNBEYPC55GHGM9MM&pd_rd_r=a4cf0659-cf29-4df5-8f0a-6e32e6c57a29&pd_rd_wg=gzED3&qid=1570646486
    https://www.amazon.com/s/?k=oneplus+6t&ref=sugsr_6&pd_rd_w=CSMhL&pf_rd_p=7be70e42-b5c0-4077-873a-35a472a6fbd4&pf_rd_r=GDWNZNBEYPC55GHGM9MM&pd_rd_r=a4cf0659-cf29-4df5-8f0a-6e32e6c57a29&pd_rd_wg=gzED3&qid=1570646486
    https://www.amazon.com/s/?k=oneplus+6t&ref=sugsr_6&pd_rd_w=CSMhL&pf_rd_p=7be70e42-b5c0-4077-873a-35a472a6fbd4&pf_rd_r=GDWNZNBEYPC55GHGM9MM&pd_rd_r=a4cf0659-cf29-4df5-8f0a-6e32e6c57a29&pd_rd_wg=gzED3&qid=1570646486
    https://www.amazon.com/s/?k=oneplus&ref=sugsr_7&pd_rd_w=CSMhL&pf_rd_p=7be70e42-b5c0-4077-873a-35a472a6fbd4&pf_rd_r=GDWNZNBEYPC55GHGM9MM&pd_rd_r=a4cf0659-cf29-4df5-8f0a-6e32e6c57a29&pd_rd_wg=gzED3&qid=1570646486
    https://www.amazon.com/s/?k=oneplus&ref=sugsr_7&pd_rd_w=CSMhL&pf_rd_p=7be70e42-b5c0-4077-873a-35a472a6fbd4&pf_rd_r=GDWNZNBEYPC55GHGM9MM&pd_rd_r=a4cf0659-cf29-4df5-8f0a-6e32e6c57a29&pd_rd_wg=gzED3&qid=1570646486
    https://www.amazon.com/s?k=oneplus+7t&ref=nb_sb_noss_1#
    https://www.amazon.com/s?k=oneplus+7t&ref=nb_sb_noss_1#
    https://www.amazon.com/s?k=oneplus+7t&ref=nb_sb_noss_1#s-skipLinkTargetForFilterOptions
    https://www.amazon.com/gp/help/customer/display.html?nodeId=468556
    https://www.amazon.com/gp/help/customer/contact-us
    https://www.amazon.com/product-reviews/B07SD7Z3J7/ref=acr_search_hist_5??ie=UTF8&filterByStar=five_star&showViewpoints=0
    https://www.amazon.com/product-reviews/B07SD7Z3J7/ref=acr_search_hist_5??ie=UTF8&filterByStar=five_star&showViewpoints=0
    https://www.amazon.com/product-reviews/B07SD7Z3J7/ref=acr_search_hist_4??ie=UTF8&filterByStar=four_star&showViewpoints=0
    https://www.amazon.com/product-reviews/B07SD7Z3J7/ref=acr_search_hist_4??ie=UTF8&filterByStar=four_star&showViewpoints=0
    https://www.amazon.com/product-reviews/B07SD7Z3J7/ref=acr_search_hist_3??ie=UTF8&filterByStar=three_star&showViewpoints=0
    https://www.amazon.com/product-reviews/B07SD7Z3J7/ref=acr_search_hist_3??ie=UTF8&filterByStar=three_star&showViewpoints=0
    https://www.amazon.com/product-reviews/B07SD7Z3J7/ref=acr_search_hist_1??ie=UTF8&filterByStar=one_star&showViewpoints=0
    https://www.amazon.com/product-reviews/B07SD7Z3J7/ref=acr_search_hist_1??ie=UTF8&filterByStar=one_star&showViewpoints=0



```python
for element in browser.find_elements_by_class_name("a-price-whole"):
    print(element.text)
```

    438
    604
    399
    319
    444
    829
    339
    309
    12
    9
    489
    349
    339
    559
    12
    9
    9
    8
    11
    34
    24
    11



```python
browser.close()
```


    -----------------------------------------------

    NoSuchWindowExceptionTraceback (most recent call last)

    <ipython-input-73-d836b8a2b4da> in <module>
    ----> 1 browser.close()
    

    ~/anaconda3/envs/flatiron-env/lib/python3.6/site-packages/selenium/webdriver/remote/webdriver.py in close(self)
        686             driver.close()
        687         """
    --> 688         self.execute(Command.CLOSE)
        689 
        690     def quit(self):


    ~/anaconda3/envs/flatiron-env/lib/python3.6/site-packages/selenium/webdriver/remote/webdriver.py in execute(self, driver_command, params)
        319         response = self.command_executor.execute(driver_command, params)
        320         if response:
    --> 321             self.error_handler.check_response(response)
        322             response['value'] = self._unwrap_value(
        323                 response.get('value', None))


    ~/anaconda3/envs/flatiron-env/lib/python3.6/site-packages/selenium/webdriver/remote/errorhandler.py in check_response(self, response)
        240                 alert_text = value['alert'].get('text')
        241             raise exception_class(message, screen, stacktrace, alert_text)
    --> 242         raise exception_class(message, screen, stacktrace)
        243 
        244     def _value_or_default(self, obj, key, default):


    NoSuchWindowException: Message: no such window: target window already closed
    from unknown error: web view not found
      (Session info: chrome=77.0.3865.90)



### Assessment
