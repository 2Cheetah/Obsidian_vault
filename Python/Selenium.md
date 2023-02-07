# Selenium headless browser
#selenium

[Readthedocs](https://selenium-python.readthedocs.io/index.html)
[Selenium documentation](https://www.selenium.dev/selenium/docs/api/py/index.html)
[Homepage](https://www.selenium.dev/)

## Installation

```bash
poetry add selenium
```

## Usage

Example:
```python
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.common.by import By


options = webdriver.ChromeOptions()
options.add_argument("--incognito")
options.add_argument("--disable-blink-features=AutomationControlled")

with webdriver.Chrome(options=options) as driver:
    driver.get("http://alfa.me/coin")
    coin_button = driver.find_element(By.XPATH, '/html/body/div/div/div/button')
    coin_button.click()
```

`options.add_argument("--disable-blink-features=AutomationControlled")` hides from website that it's headless browser.

Example from Readthedocs:
```python
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.common.by import By

driver = webdriver.Firefox()
driver.get("http://www.python.org")
assert "Python" in driver.title
elem = driver.find_element(By.NAME, "q")
elem.clear()
elem.send_keys("pycon")
elem.send_keys(Keys.RETURN)
assert "No results found." not in driver.page_source
driver.close()
```

[Website to check if the headless browser is detected by sites](https://intoli.com/blog/not-possible-to-block-chrome-headless/chrome-headless-test.html)