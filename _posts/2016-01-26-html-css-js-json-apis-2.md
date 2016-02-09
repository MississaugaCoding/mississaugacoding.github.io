---
layout: post
title: "HTML/CSS/JS - More JSON API Examples"
comments: true
publish: true
---

In the previous session we built a web page based on one of the numerous JSON APIs freely available on the Internet. In this session we look at another, slightly more involved, example. 

While the vast majority of JSON APIs are free to use, some of them do require that you register beforehand, and that your AJAX calls to the service include your own unique API key, which is given to you upon registration. This is the case with the APIs demonstrated in this session.

Another aspect we'll look at in this session is sending data to the API. As mentioned some weeks ago, the jQuery AJAX methods - `$.get()` and `$.post()` - can send as well as receive data. For example, we would need to send the API key for those APIs that require it. Or, say if we're making an AJAX call to get the co-ordinates of a specific place, we would need to send the name of the location.

Here is the full code for the example we were working on. Any questions, please feel free to use the discussion area just below this post.


###index.html
{% highlight html %}
<!doctype html>
<html>

<head>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Using JSON APIs</title>

    <!-- Bootstrap CSS -->
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css" />

    <!-- Link for optional custom CSS goes here -->
    <link rel="stylesheet" href="style.css" type="text/css" />

</head>

<body>

    <!-- main html content starts here -->

    <div class="container">
        <div class="page-header">
            <h1>Using JSON APIs - Google Geocoding, Maps & WorldWeather</h1>
        </div>

        <!-- search input -->
        <div class="input-group input-group-lg">
            <input type="text" class="form-control input-lg" id="txtLocation" placeholder="What's the current weather in ..." />
            <span class="input-group-btn">
                <button class="btn btn-primary btn-lg">Show Me The Weather</button>
            </span>
        </div>  <!-- input-group --> 

        <div id="divResults">
            <div id="divMap"></div>
            <div id="divWeather"></div>
        </div>

    </div>

    <!-- main html content ends here   -->

    <template id="tmpResults">
        <p>Conditions: {{current_condition.0.weatherDesc.0.value}}</p>
        <p>Temperature: {{current_condition.0.temp_C}}C</p>
        <p>Feels Like: {{current_condition.0.FeelsLikeC}}C</p>
        <p>Wind: {{current_condition.0.winddir16Point}} at {{current_condition.0.windspeedKmph}}Km/hr</p>
        <p>Humidity: {{current_condition.0.humidity}}%</p>
        <p>Today's High: {{weather.0.maxtempC}}C</p>
        <p>Today's Low: {{weather.0.mintempC}}C</p>
    </template>

    <!-- jQuery -->
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/2.1.4/jquery.min.js"></script>

    <!-- Bootstrap JavaScript -->
    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/js/bootstrap.min.js"></script>

    <!-- Mustache template library -->
    <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/mustache.js/2.2.1/mustache.min.js"></script>

    <!-- Google Maps API (library) -->
    <script src="https://maps.googleapis.com/maps/api/js"></script>

    <!-- script tag for custom JS goes here -->
    <script type="text/javascript" src="script.js"></script>

</body>

</html>
{% endhighlight %}


###script.js
{% highlight javascript %}
$(document).ready(function() {

    $('button').on('click', function() {

        var location = $('#txtLocation').val();
        
        if (location !== '') {

            // get co-ords for location entered (latitude,longitude)
            // e.g. https://maps.googleapis.com/maps/api/geocode/json?address=mississauga&key=your-google-api-key

            var googleAPIKey = 'your-google-api-key';
            var googleAPIUrl = 'https://maps.googleapis.com/maps/api/geocode/json';
            var googleParms = { "address": location, "key": googleAPIKey };

            $.get(googleAPIUrl, googleParms, function(resp) {

                var lat = resp.results[0].geometry.location.lat;
                var lng = resp.results[0].geometry.location.lng;

                // get map of location
                displayMap(lat, lng);

                // get current weather at those co-ords
                // e.g. https://api.worldweatheronline.com/free/v2/weather.ashx?q=43,-79&format=json&key=your-weather-api-key
                
                var weatherAPIKey = 'your-weather-api-key';
                var weatherAPIUrl = 'https://api.worldweatheronline.com/free/v2/weather.ashx';
                var weatherParms  = { "key": weatherAPIKey, "format":"json", "q": lat + "," + lng };
                
                $.get( weatherAPIUrl, weatherParms, function(resp2) {
                    
                    var pattern = $('#tmpResults').html();
                    var content = Mustache.render(pattern, resp2.data);
                    
                    $('#divWeather').html(content);
                    
                });

            });
            
        }

    });


    function displayMap(lat, lng) {
        var mapProperties = {
            center: new google.maps.LatLng(lat, lng),
            zoom: 10,
            mapTypeId: google.maps.MapTypeId.ROADMAP
        };
        var map = new google.maps.Map(document.getElementById("divMap"), mapProperties);
    }


});
{% endhighlight %}

###style.css
{% highlight css %}
#divMap {
    width: 600px;
    height:400px;
    float:left;
    
}

#divWeather {
    display: inline;
    float:left;
    padding-left:15px;
    font-weight: bold;
    font-size: 1.5em;
    
}

#divResults {
    padding-top: 15px;
}
{% endhighlight %}

##References &amp; Resources

- [Google Geocoding JSON API Docs](https://developers.google.com/maps/documentation/geocoding/intro)
- [Google Maps Example](http://www.w3schools.com/googleapi/google_maps_basic.asp)
- [World Weather JSON API Docs](https://developer.worldweatheronline.com/page/explorer-free)
<br/>
- [Google Geocoding JSON API call example](https://maps.googleapis.com/maps/api/geocode/json?address=mississauga&key=AIzaSyA_M7VnGki-4-0YfjMT18ZTJDGxbi2QMYQ)
- [World Weather JSON API call example](https://api.worldweatheronline.com/free/v2/weather.ashx?q=43,-79&format=json&key=ec746df3a2e403fd5ec97aeddfcec)

