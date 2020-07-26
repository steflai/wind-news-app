# wind-news-app
Python app that displays news headline according to wind direction and speed 


News scroller app 

API’s needed 
Math for sine
Weather: Dark Sky 
Wind direction (windBearing = The direction that the wind is coming from in degrees, with true north at 0° and progressing clockwise)
Wind speed 
Geocode API 
Google Geocoding https://developers.google.com/maps/documentation/geocoding/intro
Issue with this however it doesn’t return location info that is categorized 
https://rapidapi.com/Noggle/api/reverse-geocoding-and-geolocation-service
Try this one as it returns specifically ‘city’ and automatically returns the nearest 3 cities 
http://www.geonames.org/export/web-services.html (find nearby populated place) 


How to get to target location 
Start with lat/lng of user -- ability to change it, otherwise default to NYC 
Depending on direction and strength of wind, generate a target lat/lng 
Each degree is approximately 69 miles (111 kilometers) apart. For reference: 
NYC to SF is 2900 miles 
NYC to London is 3500 miles 
NYC to HK is 8045 miles 
NYC to BA is 5295 miles 


Windspeed (darksky returns meters per second) 
0 to 2 - calm to low - display local news + 50 miles 
2 to 4 - light breeze - 100 miles  
4 to 7 - medium breeze - 300 miles 
7 - 10 - strong breeze - 500 miles 
10 to 13 - strong wind - 1000 miles 
13 to 17 - high wind - 2500 miles 
17 to 20 - high wind / gale - 5000 miles 
20 + - 8000 miles 


Calculating new lat/lng
NSEW - simply add x degrees (x = distance / 69)
Finding A and B 
A = C * sin(m) 
B = C * sin(n)
If between 0 and 90 degrees 
New lat = lat + A
New lng = lng + B
If between 90 and 180 
Angle m = 180 - windBearing 
New lat = lat - B
New lng = lng + A 
If between 180 and 270 
Angle m = 270 - windBearing 
New lat = lat - A 
New lng = lng - B
If 270 + 
Angle m = 360 - windBearing 
New lat = lat + B 
New lng = lng - A   


City name of that lat/lng to be used as search term for news 
What happens if in the middle of the ocean?? 
Make presets? 
News: https://newsapi.org/docs


Search by city name 
Use description, better (more contentful) than just title. Also display source name and author


Display 
Feed Parser - to make it scroll https://pythonhosted.org/feedparser/introduction.html#parsing-a-feed-from-a-string
Flask?! Django? 
HTML / wordpress plugin ? write to text file that is then read by display mechanism 
Set cron 
100 articles per?  
