---
layout: post
title: "HTML/CSS/JS - More JSON API Examples"
comments: true
publish: true
---

In the previous session we built a web page based on one of the numerous JSON APIs freely available on the Internet. In this session we look at another, slightly more involved, example. 

While the vast majority of JSON APIs are free to use, some of them do require that you register beforehand, and that your AJAX calls to the service include your own unique API key, which is given to you upon registration. This is the case with the APIs demonstrated in this session.

Another aspect we'll look at in this session is sending data to the API. As mentioned some weeks ago, the jQuery AJAX methods - `$.get()` and `$.post()` - can send as well as receive data. For example, we would need to send the API key for those APIs that require it. Or, say if we're making an AJAX call to get the co-ordinates of a specific place, we would need to send the name of the location.

Full sample code of what we built during the session will be posted here later.

Example JSON API calls:

- [Google Geocoding JSON API](https://maps.googleapis.com/maps/api/geocode/json?address=mississauga&key=AIzaSyA_M7VnGki-4-0YfjMT18ZTJDGxbi2QMYQ)

- [World Weather JSON API](https://api.worldweatheronline.com/free/v2/weather.ashx?q=43,-79&format=json&key=ec746df3a2e403fd5ec97aeddfcec)


##References &amp; Resources

- [Google Geocoding JSON API Docs](https://developers.google.com/maps/documentation/geocoding/intro)
- [Google Maps Example](http://www.w3schools.com/googleapi/google_maps_basic.asp)
- [World Weather JSON API Docs](https://developer.worldweatheronline.com/page/explorer-free)

