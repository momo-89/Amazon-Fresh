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

For hungry pandas, add the following.
```
import urllib
import json
data = {}
data['longitude'] = '-73.93698'
data['latitude'] = '40.74927'
data['version'] = '2.7.4'
data['pageno'] = '1'
data['categoryid'] = '187'
url = 'http://app.usa.hungrypanda.co/api/user/shops/bycategoryid?filterJson=%7B%22freeDeliveryPrice%22%3A0%2C%22payment%22%3A-1%2C%22isNewStore%22%3A0%2C%22delivery%22%3A-1%2C%22fullSub%22%3A-1%2C%22isNewUser%22%3A0%2C%22isForNewOrder%22%3A0%7D'
req = urllib.request.Request(url, headers=data)

with urllib.request.urlopen(req) as resp:
    the_page = json.loads(resp.read().decode('utf-8'))
    for shop in the_page['result']['shopIndexList']:
        if '超' in shop['shopName'] and shop['shopStatus'] == 0:
            try:
                clickatell = Http('9aQ7rldNQhS1r1bX_6SqFw==')
                clickatell.sendMessage(['+19178817289'], "hungry pandas supermarket opening")
            except:
                pass
```
