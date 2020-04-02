First, download `chromedriver` https://chromedriver.chromium.org/downloads

Second, use `pip` to install `clickatell` and `selenium`

Third, run the following code from the jupyter notebook. You will see a browser open. Log into your amazon and go to the Amazon Fresh checkout page.
```
from selenium import webdriver
driver = webdriver.Chrome('/Users/wmo402/Downloads/chromedriver')
```

Then run the following code.
```
import time
import clickatell
from clickatell.http import Http
while True:
    driver.get('https://www.amazon.com/gp/buy/shipoptionselect/handlers/display.html?hasWorkingJavascript=1')
    try:
        driver.find_element_by_css_selector(".a-box-group[id^='root'] .a-box:not(.disabledRadioBox)")
        try:
            # the api needs your phone number to be on the list
            # you can either register on clickatell by yourself
            # or you can ask me to add you into the list
            # I can only add up to 3 numbers
            clickatell = Http('9aQ7rldNQhS1r1bX_6SqFw==')
            clickatell.sendMessage(['+19178817289'], "got a slot")
        except:
            pass
    except:
        pass
    time.sleep(30)
```
