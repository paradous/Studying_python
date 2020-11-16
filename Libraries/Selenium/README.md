# Selenium 101

## Installing on Ubuntu for Chromium
First, install the chromium driver:

```Shell
sudo apt-get install chromium-chromedriver
```
Then, in your code, set your driver as:
```Python
driver = webdriver.Chrome("/usr/lib/chromium-browser/chromedriver")
```
