---
layout: post
title: "HTML/CSS/JS - Using JSON APIs"
comments: true
publish: true
---
At our last session we discussed the JSON data format and went over some examples of what we can do with JavaScript objects. 

Those examples centred around some JSON data that we were reading in from a file. Not a common scenario in reality, but it served to illustrate the key theoretical points and concepts. So next we will code some practical applications of those concepts. 

There are lots of third-party JSON APIs freely available on the web, and today's example will show how you can use one of these APIs for your web pages.

Here is the complete example we coded during the session.

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
            <h1>Using JSON APIs - Reddit Example</h1>
        </div>

        <!-- we will inject html into this div later -->
        <div id="divResults"></div>  

    </div>

    <!-- main html content ends here   -->

    
    <!-- Mustache template is not rendered by browser -->
    <!-- It is a pattern upon which we will superimpose the JSON data we get back from the AJAX call -->
    <template id="tmpResults">
      {% raw %}
      {{#children}}  <!-- start looping through the array called children in the result JSON data -->
      
      <div> <!-- added a div so each image appears on its own line -->
      
          <img src="{{data.preview.images.0.source.url}}"/>  <!-- important to navigate to the right node -->
      
          <!-- added this in the template to show how many 'likes' the photo has received  -->
          <p><span class="glyphicon glyphicon-thumbs-up"></span> {{data.ups}}</p>
      
      </div>
      {{/children}}  <!-- loop ends -->
      {% endraw %}
    </template>
    
    

    <!-- jQuery -->
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/2.1.4/jquery.min.js"></script>

    <!-- Bootstrap JavaScript -->
    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/js/bootstrap.min.js"></script>

    <!-- Mustache template library -->
    <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/mustache.js/2.2.1/mustache.min.js"></script>

    <!-- script tag for custom JS goes here -->
    <script type="text/javascript" src="script.js"></script>

</body>

</html>
{% endhighlight %}

###script.js
{% highlight javascript %}
/*
JSON API Example: Reddit
API documentation: https://www.reddit.com/dev/api 
Example call: https://www.reddit.com/r/cats/top.json
*/

$(document).ready(function() {

    // do the AJAX call via the jQuery $.get() method
    // in this case, first argument is our data source - where is the JSON data coming from?
    // the second argument is a callback, in the form of an anonymous function - what do we want to do once we get the JSON data?
    $.get('https://www.reddit.com/r/cats/top.json', function(resp){
        
        // rendering the content by applying the pattern to the JSON data
        var pattern = $('#tmpResults').html(); // get the template pattern
        var content = Mustache.render( pattern , resp.data );  //  apply the pattern to the JSON data
        $('#divResults').html(content); // inject the content into the div
        
    });

});
{% endhighlight %}

###style.css
{% highlight css %}
img {
    width:350px; /* the images from the Reddit JSON API call vary in size; this way we get a more uniform display by forcing a width */
}

p {
    font-weight: bold;
    font-size: 1.5em;
    padding-bottom: 5px;
}
{% endhighlight %}


##References &amp; Resources

- [Reddit API](https://www.reddit.com/dev/api)
- [Programmable Web](http://www.programmableweb.com/)
- [Mashape](https://market.mashape.com/explore)
