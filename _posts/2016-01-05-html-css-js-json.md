---
layout: post
title: "HTML/CSS/JS - Using JSON with jQuery & Templates"
comments: true
publish: true
---

Dynamic, data-driven web applications nowadays often use JavaScript Object Notation - JSON - to communicate with a back-end database or web service of some sort.

JSON is a simple, light-weight format for storing and passing data. It is native to JavaScript, but it is also supported in various other languages and web technologies.

A simple example of this format, assigned to a variable:

`var json = {"fname":"Joe"};`

It is a name-value pair notation. Note the field name in **double quotes**, followed by a colon, followed by the value, and all of that enclosed in curly braces. 

We can have multiple name-value pairs, for example:

`var json = {"id":1, "fname":"Joe", "lname":"Smith", "member":true};`

Common value types are string (in **double quotes**), numeric and boolean.

We can also have multiple JavaScript objects, or arrays of objects, as well as nested objects.

{% highlight javascript %}
var json = { 
  "clients": [
    { "id": 1, "fname": "Tony", "lname": "Stark", "member" : false }, 
    { "id": 2, "fname": "Clark", "lname": "Kent", "member" : true } 
  ] 
};
{% endhighlight %}

Think of objects as records, and name-value pairs as fields.

JSON can also exist as a file, usually with a `.json` extension, for example: data.json

{% highlight json %}
{ 
  "clients": [
    { "id": 1, "fname": "Tony", "lname": "Stark", "member" : false }, 
    { "id": 2, "fname": "Clark", "lname": "Kent", "member" : true } 
  ] 
}
{% endhighlight %}

Note that in this case there's no variable name and no semi-colons, just the JSON expression.

##Passing JSON data to HTML page

To display data on an HTML page, use JSON as if it were a variable (concatentation etc.) employing the dot notation as needed to access the fields within the object. For example:

###index.html
{% highlight html %}
<!doctype html>
<html>
<head>
    <title>JSON</title>
</head>
<body>
     
    <div id="divClients"></div>
    
    <!-- jQuery -->
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/2.1.4/jquery.min.js"></script>
    
    <!-- Custom JS -->
    <script type="text/javascript" src="script.js"></script>
    
</body>
</html>
{% endhighlight %}

###script.js
{% highlight javascript %}
// a JavaScript object in JSON
var json = {"id":1, "fname":"Joe", "lname":"Smith", "member":true};  

// displays 'Joe Smith'
$('#divClients').html(json.fname + " " + json.lname);  
{% endhighlight %}

##jQuery AJAX methods

JSON data can also be read in from a file (or some sort of database querying script / web service / end point / API). 

For this purpose the jQuery library provides us with simplified AJAX methods. These are shorthand methods that greatly simplify AJAX calls. (Remember `var xhr = new XMLHttpRequest()` etc. etc. ?)

The simplest of these jQuery AJAX shorthand methods are `$.get()` and `$.post()`. 

Despite the names, both methods can send/receive data, to/from the back-end server. For the purposes of this introduction, we will focus on receiving JSON data.

For example, using the same JSON but in a file:

{% highlight json %}
{"id":1, "fname":"Joe", "lname":"Smith", "member":true}
{% endhighlight %}

{% highlight javascript %}
$.get('data.json', function(data){
    $('#divClients').html(data.fname + " " + data.lname);
});
{% endhighlight %}

In this example, note that we're passing two arguments to the `$.get()` method:

- the data source, in this case a file name
- the callback function, i.e. what to do after the request is finished and we have a response
 
(If we were sending any data with the request, this would be passed in as another argument.)

##Looping through multiple JSON objects

If the response (the file, in this case) contains multiple objects we need a way to loop through these objects. One way is to use the JavaScript `forEach()` method.

For example:

###data.json
{% highlight json %}
{ 
  "clients": [
    { "id": 1, "fname": "Tony", "lname": "Stark", "member" : false }, 
    { "id": 2, "fname": "Clark", "lname": "Kent", "member" : true },
    { "id": 3, "fname": "Peter", "lname": "Parker", "member" : true },
    { "id": 4, "fname": "James", "lname": "Kirk", "member" : false } 
  ] 
}
{% endhighlight %}

###script.js
{% highlight javascript %}
$(document).ready(function() {

    $.get('data.json', function(mydata) {
    
        // initialise some variables
        var div = $('#divClients');
        var p; 
        
        // loop through the data
        mydata.clients.forEach(function (client) { 
            p = document.createElement('p'); 
            p.innerHTML = client.id + '. ' + 
                client.lname + ', ' + client.fname; 
            div.append(p); 
        });
        
    });
    
});
{% endhighlight %}

Note how the `forEach()` method takes a callback function, which in turn takes a variable name. This variable name `client` is what we use inside the loop to refer to the individual object or record, and get its fields.

##Templates
This process of reading in multiple JSON objects can be further simplified by using templates.

A template is a pattern that we wish to apply to each object in the array. HTML 5 introduced a new `template` tag for this purpose.

There are several JavaScript templating libraries. For this example we will use Mustache. (See link in references section.)


###index.html
{% highlight html %}
<!doctype html>
<html>
<head>
    <title>JSON</title>
</head>
<body>
     
    <div id="divClients"></div>
    
    <!-- template for use with Mustache  -->
    <template id="mytemplate">
        {% raw %}{{#clients}}
            <p>{{id}}. {{lname}}, {{fname}}</p>
        {{/clients}}{% endraw %}
    </template>
    
    <!-- jQuery -->
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/2.1.4/jquery.min.js"></script>
    
    <!-- Mustache template library -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/mustache.js/2.2.1/mustache.min.js"></script>
    
    <!-- Custom JS -->
    <script type="text/javascript" src="script.js"></script>
    
</body>
</html>
{% endhighlight %}

###script.js
{% highlight javascript %}
$(document).ready(function() {

    $.get('data.json', function(mydata) {
    
        $('#divClients').html( Mustache.render( $('#mytemplate').html() , mydata ) );
        
    });
    
});
{% endhighlight %}








##References &amp; Resources

- [JSON format](http://json.org/)
- [JSON validator](https://jsonformatter.curiousconcept.com/)
- [jQuery AJAX shorthand methods](https://api.jquery.com/category/ajax/shorthand-methods/)
- [HTTP GET & POST methods](http://www.w3schools.com/tags/ref_httpmethods.asp)
- [Mustache template library](http://cdnjs.com/libraries/mustache.js/)
