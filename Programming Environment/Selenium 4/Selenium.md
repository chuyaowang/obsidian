# Selenium

> [Official Page](https://www.selenium.dev/documentation/overview/)

A WebDriver testing framework. It translates code into actions that are sent to [WebDrivers](WebDriver.md) to control browsers.

## Installation

[Python](Python.md) package
Create a new environment with [conda](conda.md#Create%20environment).
[Install pip](conda.md#Use%20with%20pip)
Install Selenium with `pip install selenium`

## Driver Object

An `EdgeDriver` object is created to start a MS Edge session. This object launches a **WebDriver Process** to communicate with and control the browser. It is efficient to start a process and let all the `EdgeDriver` object use this process.

## Locating Elements

[Documentation](https://selenium-python.readthedocs.io/locating-elements.html)
### X Path

A way to find html elements on webpages

[Source](https://www.perfecto.io/blog/xpath-in-selenium#:~:text=XPath%20in%20Selenium%20is%20a,both%20HTML%20and%20XML%20documents.)

## driver.implicitly_wait

A way to let the driver wait for the request element to appear. If the element appears before the set time, the code proceeds; if it does not, an error is thrown.

Another way is to use `time.sleep(n)`, the driver will be stopped for exactly n seconds.