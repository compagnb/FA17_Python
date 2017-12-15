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
* To access the information that the API is broadcasting, we need to make a request. This is done by requesting a certain URL. Under the **documentation** tab, they will give you a sample url that looks similar to this:
```
http://api.wunderground.com/api/APIKey/conditions/q/CA/San_Francisco.json
```
* The position where **APIKey** will differ, as it should match that password that you were assigned after signing up. 
* **conditions** can be exchanged for other information too. For other options, refer to the documentation for the API.
* **CA**, and **San_Francisco.json** can also be changed to match the state and city we choose. 
	
* If we put this url into the browser, you should recieve something called a **JSON Object**... it will look like this:
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
 			"url": "http://icons-ak.wxug.com/graphics/wu2/logo_130x80.png",
  			"title": "Weather Underground",
  			"link": "http://www.wunderground.com"
 		},
  		"display_location": {
  			"full": "San Francisco, CA",
  			"city": "San Francisco",
  			"state": "CA",
  			"state_name": "California",
  			"country": "US",
  			"country_iso3166": "US",
 			"zip": "94101",
  			"latitude": "37.77500916",
  			"longitude": "-122.41825867",
  			"elevation": "47.00000000"
  		},
  		"observation_location": {
  			"full": "SOMA - Near Van Ness, San Francisco, California",
  			"city": "SOMA - Near Van Ness, San Francisco",
  			"state": "California",
  			"country": "US",
  			"country_iso3166": "US",
  			"latitude": "37.773285",
  			"longitude": "-122.417725",
  			"elevation": "49 ft"
  		},
  		"estimated": {},
  		"station_id": "KCASANFR58",
  		"observation_time": "Last Updated on June 27, 5:27 PM PDT",
  		"observation_time_rfc822": "Wed, 27 Jun 2012 17:27:13 -0700",
  		"observation_epoch": "1340843233",
  		"local_time_rfc822": "Wed, 27 Jun 2012 17:27:14 -0700",
  		"local_epoch": "1340843234",
  		"local_tz_short": "PDT",
  		"local_tz_long": "America/Los_Angeles",
  		"local_tz_offset": "-0700",
  		"weather": "Partly Cloudy",
  		"temperature_string": "66.3 F (19.1 C)",
  		"temp_f": 66.3,
  		"temp_c": 19.1,
  		"relative_humidity": "65%",
  		"wind_string": "From the NNW at 22.0 MPH Gusting to 28.0 MPH",
  		"wind_dir": "NNW",
  		"wind_degrees": 346,
  		"wind_mph": 22.0,
  		"wind_gust_mph": "28.0",
  		"wind_kph": 35.4,
  		"wind_gust_kph": "45.1",
  		"pressure_mb": "1013",
  		"pressure_in": "29.93",
  		"pressure_trend": "+",
  		"dewpoint_string": "54 F (12 C)",
  		"dewpoint_f": 54,
  		"dewpoint_c": 12,
  		"heat_index_string": "NA",
  		"heat_index_f": "NA",
  		"heat_index_c": "NA",
  		"windchill_string": "NA",
  		"windchill_f": "NA",
 		"windchill_c": "NA",
  		"feelslike_string": "66.3 F (19.1 C)",
  		"feelslike_f": "66.3",
  		"feelslike_c": "19.1",
  		"visibility_mi": "10.0",
  		"visibility_km": "16.1",
  		"solarradiation": "",
  		"UV": "5",
  		"precip_1hr_string": "0.00 in ( 0 mm)",
  		"precip_1hr_in": "0.00",
  		"precip_1hr_metric": " 0",
 		"precip_today_string": "0.00 in (0 mm)",
 		"precip_today_in": "0.00",
  		"precip_today_metric": "0",
  		"icon": "partlycloudy",
  		"icon_url": "http://icons-ak.wxug.com/i/c/k/partlycloudy.gif",
  		"forecast_url": "http://www.wunderground.com/US/CA/San_Francisco.html",
  		"history_url": "http://www.wunderground.com/history/airport/KCASANFR58/2012/6/27/DailyHistory.html",
  		"ob_url": "http://www.wunderground.com/cgi-bin/findweather/getForecast?query=37.773285,-122.417725"
  }
}		
```

## Connecting Python To A Website
* To grab the information from an Open API through our program, we first need to open up the contents of the URL (like we just did with the URL). 
* This will require us to us the urlib2 module. More documentation on this module can be found at https://docs.python.org/2/library/urllib2.html. This is not part of the original Python install, so unless you manually install (with a PIP command), it will only give you an error message. 
* Once the module is intalled, we can import it at the top of our program like we did with turtle. 
* Then we can send a request command to open a URL by using the urlopen() method and stores the JSON Object in a variable.
```
apiData = urllib2.urlopen('http://api.wunderground.com/api/APIKey/conditions/q/CA/San_Francisco.json')
```
* Now that the object has been stored into a variable, we need to manipulate it in order to tell us the exact information we are looking for.
	
## Working With JSON Objects
* JSON Objects are like python maps (but are a little more complicated), they hold and exchange a information. The reason why we are using JSON Objects, and not Python maps, is because the website broadcasts information in JavaScript format. 
* Notice how all the information is organized. There are parents (response & current_observation), children (version, termsofService, features, image, display_location), and grandchildren (conditions, url, title, link, full, city, state, state_name, country, country_iso3166, etc.) In order to access the grandchildren, we first need to access the parent and the child it belongs to.
* To manipluate this data, the **json module** is needed. Documentation on this module can be found at https://docs.python.org/2/library/json.html. Similar to the urlib2 module, this is not part of the original Python install, so unless you manually install (with a PIP command), it will only give you an error message. 
* Since this object holds a bunch of information, we need to **read** and **parse** the data. This will break it down into smaller pieces and convert it to a string variable that we can hold in Python. 
```
jsonString = apiData.read()
parsedJson = jsonLoads(jsonString)
```
* Now that the data is parsed, it is easier to pull the information stored in the children and grandchildren. To pull the information for the location, we do so like this:
```
location = parsedJson['display_location']['city']
```
* Notice how we pin point the information we are pulling out... by listing where it is found in the structure.
* Now try and do one for the temperature. 

## Challenge:
* Make a program that asks for a location from the user and give the temperature. 
* Make an add on for the space invader game that we built that changes the weather for the temperature.

## Vocabulary
* API: (Application Program Interface) a set of  programming instructions and standards for accessing web based software applications.
* API Key: Password used to access an API
* JSON Object: (JavaScript Object Notation) is very much like a python map, it is a way of storing information.  In JavaScript, an object gets called like this:
```
var myObj = { "name":"John", "age":31, "city":"New York" };
```
* Parse: break down information into smaller parts

