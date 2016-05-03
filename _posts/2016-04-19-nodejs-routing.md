---
layout: post
title: "Basic Routing In NodeJS"
comments: true
publish: true
---

Next we shall add some basic routing to our back-end server, but first what is routing and why do we need it?

### What do we mean by 'routing'?

Routing is a mechanism by which information passed in with the client request is in turn used by the server program to build and send back the server's response.

This information is passed in with the request, for example, as a pathname like in:

`http://server-url:8081/clients` 

and/or as parameters in the query string, such as:

`http://server-url:8081/client?id=123`

Routing enables our one server program to handle several different types of requests, and to serve the appropriate response for each request accordingly.


### Adding routes to our back-end server code

In order to be able to parse the request for pathnames and query string parameters, we require another core module:

`var url  = require('url');`

Using this module, in the request handler function, we can parse out the pathname like so:

`var route = url.parse(request.url).pathname;`

We can then use a `switch-case` block to execute the applicable code based on what's in the pathname. A `switch-case` is essentially a fancy `if` statement, but makes for cleaner, more readable code, something like this:

{% highlight javascript %}
switch (route) {
    
    case '/':
        response.write( 'This is the home page.' );
        break;
        
    case '/clients':
        response.write( JSON.stringify(dataClients) );
        break;
            
    case '/products':
        response.write( JSON.stringify(dataProds) );
        break;
        
}
{% endhighlight %}

Just for the purpose of this example, we will hard-code some JSON data records right in the server code to simulate the server fetching some data. Obviously, in real life the server would query out the required records from a database. We shall cover this aspect as a separate topic later.

{% highlight javascript %}
// data would normally come from a database of some sort
var dataClients = [
    {"id": 1,"name": "Jane","pic":"http://lorempixel.com/200/200/cats/Jane"}, 
    {"id": 2,"name": "Jack","pic":"http://lorempixel.com/200/200/cats/Jack"}, 
    {"id": 3,"name": "Joe", "pic":"http://lorempixel.com/200/200/cats/Joe" }, 
    {"id": 4,"name": "Jill","pic":"http://lorempixel.com/200/200/cats/Jill"}
];
    
var dataProds = [
    {"id": 110,"name": "cars"}, 
    {"id": 111,"name": "pizza"}, 
    {"id": 112,"name": "software"}, 
    {"id": 113,"name": "phones"}
];
{% endhighlight %}


### How does the front-end change to take advantage of routing?

To call the set routes from the front-end, we simply add the pathname to the url in the AJAX call, in our app.js, for example:

{% highlight javascript %}
// make request for all client records from server
// and display response as a list of client names
$.get('http://server-url:8081/clients', function(resp){
    var data = JSON.parse(resp);
    $('div#list').html('<ul></ul>');
    data.forEach( function(c) {
        $('div#list ul').append('<li>' + c.name + '</li>');
    });
});
{% endhighlight %}


### Passing in parameters with the request

Aside from the pathname, we can further specify our request by passing in parameters. 

Let's say we wanted to request a particular client record, the one with a certain id. 

We can obtain this client id. from the web page (a form, a link, whatever) and pass in this id. parameter in one of two ways, either:

`$.get('http://server-url:8081/client?id=' + clientId , function(resp){ ...`

or as the second argument in the AJAX call:

`$.get('http://server-url:8081/client', {"id":clientId} , function(resp){ ...`

Either way, on the server, we once again use the `url` core module to extract this id. parameter, like so:

{% highlight javascript %}
switch (route) {
    
    ....
    
    case '/client':
        // extract the parms passed in with the request
        var parms = url.parse(req.url,true).query; 
            
        // find the particular client using filter() method
        var client = dataClients.filter( function(c) { 
            return c.id == parms.id; 
        });
            
        res.write( JSON.stringify(client) );
        break;
        
    ....
    
{% endhighlight %}

To make this request, and process the response, on the front-end (in app.js) we would have something like:

{% highlight javascript %}

....

// make request for a particular client record
// and display response 
$.get('http://server-url:8081/client?id=1', function(resp){
    var data = JSON.parse(resp);
    $('div#list').html('');
    data.forEach( function(c) {
        $('div#list').append('<p>Id:' + c.id + '</p>');
        $('div#list').append('<p>Name:' + c.name + '</p>');
        $('div#list').append('<div><img src="' + c.pic + '" /></div>');
    });
});

....

{% endhighlight %}
            

Here is a link to the full example code on [GitHub](https://github.com/lcarbonaro/nodejs/tree/master/session23)


## References &amp; Resources

- [NodeJS](https://nodejs.org/)