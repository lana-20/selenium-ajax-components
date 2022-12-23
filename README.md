# Handling AJAX Components with Explicit Wait
## Selenium Automation Challenges

Sometimes Selenium fails to function correctly if a dynamic event or change takes place during the test cycle. It's a free open source software. 
Freeware comes with its own challenges, unlike QTP/UFT by HP, paid licensed software, which provides its own technical support.
In Selenium, there is no constant and consistent support. Experienced professional engineers can provide solutions to Selenium automation challenges.

One of the challenges is handling [AJAX](https://www.w3schools.com/whatis/whatis_ajax.asp) components. AJAX is a technique for creating robust and dynamic web pages.

AJAX = Asynchronous JavaScript And XML. It is not a programming language. AJAX uses a combination of:
- A browser built-in XMLHttpRequest object (to request data from a web server)
- JavaScript and HTML DOM (to display or use the data)

AJAX allows web pages to be updated asynchronously by exchanging data with a web server behind the scenes. This means that it is possible to update/retrieve parts of a web page, without reloading the whole page (without a page transition).

AJAX can perform the following:
1. Read data from a web server - after a web page has loaded
2. Update a web page without reloading the page
3. Send data to a web server - in the background

The biggest challenge in handling an Ajax call is knowing the loading time of the web page. 
The usage of AJAX techniques in the web apps has introduced uncertainty in the sense that loading of the web page and the web elements present in it may happen at a different time span.
Since a web page loads in merely some fractions of a second, a Quality Engineer (SDET) finds it difficult to test such apps via automation tools. 
Furthermore, because Ajax apps often use different encoding and serialization techniques to submit/POST the date, crating automated test requests might also be problematic.
Selenium has to use a _wait_ method in order to synchronize the script with the Ajax component loading time.

<img src="https://user-images.githubusercontent.com/70295997/209401938-87b0bb16-c8e3-405b-b171-1d633ef6b8e6.png" width=500>

### Example 1: AJAX Dropdowns

This is a simple example. Let's say I have 2 dropdowns.  One dropdown is Country, the second dropdown is State.

![image](https://user-images.githubusercontent.com/70295997/209400350-8d1286cc-43af-495a-9ad7-98977704faf4.png)

Select Hawaii:

<img src="https://user-images.githubusercontent.com/70295997/209400444-74810177-71d9-4788-9854-f9d52fe64d50.png" width=250>

When selecting USA, all the USA states show in the 2nd dropdown accordingly.
When a client selects USA, a backend Ajax call is given to the server. 
The server reads this call, which says it wants all the States data for the Country ‘USA’. 
It takes all data from the database (for all the states in the country) and gives it to the client on the browser. 
It takes a fraction of a second. This type of component is known as Ajax. 


Now, select Sandy Point:

<img src="https://user-images.githubusercontent.com/70295997/209400566-6b06f044-d937-49bb-bdeb-adc968db3251.png" width=250>

It takes some time. Selenium doesn’t wait for the state to show up, it selects Sandy Point immediately. 
But this state is not available yet. It's still chewing through the Bahamas states like Bimini, Exuma, Inagua, and so on. 
Selenium WebDriver has to use a proper __explicit wait__ (a.k.a. WebDriverWait with Expected Conditions) to handle the Ajax call:

<img src="https://user-images.githubusercontent.com/70295997/209401278-8634113b-d09b-4a83-8ded-2c72211461cb.png" width=150>

By executing the _wait_ command, Selenium suspends execution of the current test case(s) and waits for the new/expected value/field. When the new value appears, WebDriver executes the test cases.


...

### Example 2: AJAX Images

...

To mimic the Fluent Wait available in Java, I use the Explicit Wait in Python and define the poll time frequency in addition to the timeout longevity. This way I can implement the Wait interface with both a timeout and a polling interval. Each _wait_ instance determines the max total timeout to wait for a condition, along with the frequency with which to poll/verify the condition.

        from selenium.webdriver.support.ui import WebDriverWait
        from selenium.webdriver.support import expected_conditions as EC

        WebDriverWait(driver, 7, poll_frequency=5).until(EC.alert_is_present()

7-8 years ago, in Selenium RC, the Explicit Wait did not exist yet. There were no Ajax components that people created on their sites.
There were only the Page Load Timeout and Implicit Wait in those initial days of Selenium. 
Finally the devs gave us the amazing Explicit Wait utility, which works 99% of the time.


----

[Use Selenium wait for page to load with Python](https://www.lambdatest.com/blog/selenium-wait-for-page-to-load/)

[How to Use Selenium WebDriver Waits using Python](https://techbeamers.com/selenium-webdriver-waits-python/)


