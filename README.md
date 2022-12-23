# Handling AJAX Components with Explicit Wait
## Selenium Automation Challenges

Sometimes Selenium fails to function correctly if a dynamic event or change takes place during the test cycle. It's a free open source software. 
Freeware comes with its own challenges, unlike QTP/UFT by HP, paid licensed software, which provides its own technical support.
In Selenium, there is no constant and consistent support. Experienced professional engineers can provide solutions to Selenium automation challenges.

One of the challenges is handling AJAX components.

[AJAX](https://www.w3schools.com/whatis/whatis_ajax.asp) can perform the following:
1. Read data from a web server - after a web page has loaded
2. Update a web page without reloading the page
3. Send data to a web server - in the background

AJAX = Asynchronous JavaScript And XML. It is not a programming language. AJAX uses a combination of:
- A browser built-in XMLHttpRequest object (to request data from a web server)
- JavaScript and HTML DOM (to display or use the data)

AJAX allows web pages to be updated asynchronously by exchanging data with a web server behind the scenes. This means that it is possible to update parts of a web page, without reloading the whole page.

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
But this state is not available yet. It’s still chewing through the Bahamas states like Bimini, Exuma, Inagua, and so on. 
So I have to put a proper __explicit wait__ here to handle the Ajax component:

<img src="https://user-images.githubusercontent.com/70295997/209401278-8634113b-d09b-4a83-8ded-2c72211461cb.png" width=150>




...

### Example 2: AJAX Images

...

7-8 years ago, in Selenium RC, the Explicit Wait did not exist yet. There were no Ajax components that people created on their sites.
There were only the Page Load Timeout and Implicit Wait in those initial days of Selenium. 
Finally the devs gave us the amazing Explicit Wait utility, which works 99% of the time.
