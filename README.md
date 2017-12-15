# Scraping Data From Open APIs
In this exercise we will be scraping weather data from Weather Weather Underground to use in a program that give the user the weather of the requested location.

## Creating A Free Weather Underground Account
* Visit **https://www.wunderground.com/** and click the join button to create an account.
* Enter your **email** and a **password** in the requested fields. Then **agree to the terms** and hit **submit**.
* Weather Underground will then ask if you want to upgrade to add free, **close this window**... There is no need to do this at this point in time.
* Once logged in, if you scroll to the end of the page and click the [**Weather API link**]. (https://www.wunderground.com/weather/api)
* Click on the **pricing link**, or https://www.wunderground.com/weather/api/d/pricing.html, in the api menu.
* Select **STRATUS PLAN**, and then hit **Purchase Key**. You will see the cost of $0.00 applied.
* Once this is completed, fill in the **Contact Name**, **Project Contact Email** (your email), **Project Name** , **Project Website**, in addition to the other questions they ask. After all of the questions are answered, click on the agreement to terms and **purchase key**.
* After this final submission, you will be brought to a page that gives you a **Key ID**. The Key ID will be the password we use to get into the API. 

## Working With JSON Objects
* JSON Objects are like python maps (but are a little more complicated), they hold and exchange a information. The reason why we are using JSON Objects, and not Python maps, is because the website broadcasts information in JavaScript format. 
* Below is a sample of the object that will be broadcast from Weather Underground. 

```
{
	"response": {
		"version": "0.1",
		"termsofService": "http://www.wunderground.com/weather/api/d/terms.html",
		"features": {
			"conditions": 1
		}
	},	
	"current_observation": {
		"image": {
			"url":"http://icons-ak.wxug.com/graphics/wu2/logo_130x80.png",
			"title":"Weather Underground",
			"link":"http://www.wunderground.com"
		},
		"display_location": {
			"full":"San Francisco, CA",
			"city":"San Francisco",
			"state":"CA",
			"state_name":"California",
			"country":"US",
			"country_iso3166":"US",
			"zip":"94101",
			"magic":"1",
			"wmo":"99999",
			"latitude":"37.77500916",
			"longitude":"-122.41825867",
			"elevation":"47.00000000"
		}, .....
		
```
* Notice how all the information is organized. There are parents (response & current_observation), children (version, termsofService, features, image, display_location), and grandchildren (conditions, url, title, link, full, city, state, state_name, country, country_iso3166, etc.)
	* In order to access the grandchildren, we first need to access the parent and the child it belongs to.


##

## Vocabulary
* API: (Application Program Interface) a set of  programming instructions and standards for accessing web based software applications.
* API Key:
* JSON Object: (JavaScript Object Notation) is very much like a python map, it is a way of storing information.  In JavaScript, an object gets called like this:
```
var myObj = { "name":"John", "age":31, "city":"New York" };
```

