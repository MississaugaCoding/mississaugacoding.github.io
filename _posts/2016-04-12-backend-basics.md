---
layout: post
title: "NodeJS - Back-end Set-up & Basics"
comments: true
publish: true
---

### Installing NodeJS

Download and install the latest version of NodeJS from the [NodeJS site](https://nodejs.org/).

If you opt to use a cloud IDE such as [Cloud9](https://c9.io/), NodeJS will come already installed with your workspace.

To test that NodeJS is installed correctly in your environment, type in `node -v`. This should respond with a version number.

### Creating our first back-end server

Anywhere in your workspace environment create a folder, say `backend`. Inside that folder create a file called `server.js`

### server.js
{% highlight javascript %}
var http = require('http');

function onRequest( request, response ) {
    response.write('hello world');
    response.end();
}

var server = http.createServer(onRequest);
server.listen(process.env.PORT || 3000);
{% endhighlight %}

### Running our back-end server

We can start this server running by issuing the command `node server.js` from the same folder.

We can see this server running by pointing a browser to `localhost:3000`. It should respond with the response string `hello world`.

(For Cloud9 users, point your browser to: `https://your-workspace-name.c9users.io/` ).

### Returning a JSON response

As our response we can return some data in JSON format. For now we'll just hard-code that data as a JSON variable and pass it back as the response.

### server.js
{% highlight javascript %}
var http = require('http');

function onRequest( request, response ) {
    var data = { "id":1 , "name":"Joe" , "member":true };
    response.write( JSON.stringify(data) );
    response.end();
}

var server = http.createServer(onRequest);
server.listen(process.env.PORT || 3000);
{% endhighlight %}

Restart the server by pressing `ctrl-c` and then issuing the `node server.js` command again. Refresh the browser to see the new JSON response.

### Nodemon

To save having to restart the server with each change to the server code, install `nodemon`. This is a NodeJS module that monitors the server file for any changes.

You install this by issuing the following command: `npm install nodemon`

From here on in, you can run the server with: `nodemon server.js` and this will monitor the code file for any changes and automatically restart the server as needed.

### Calling our server from a front-end

Let's complete the exercise by coding a simple front-end that will make an AJAX request to our back-end server.

First add this line to `server.js` (first line in function onRequest) so that the back-end can be called from anywhere.

`response.setHeader('Access-Control-Allow-Origin','*');`

Next, code this simple front-end by creating a folder, say `frontend`, anywhere in your workspace, and adding these files to it. (This should be very straightforward HTML/CSS/JS from our previous sessions.)

### index.html
{% highlight html %}
<!DOCTYPE html>
<html>
    <head>
        <title>title</title>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        
        <!-- Custom CSS -->
        <link rel="stylesheet" href="style.css" type="text/css" />
        
    </head>
    <body>
        <div></div>
        
        <!-- jQuery -->
        <script src="https://ajax.googleapis.com/ajax/libs/jquery/2.2.2/jquery.min.js"></script>
        
        
        <!-- Custom JS -->
        <script type="text/javascript" src="app.js"></script>
    </body>
</html>
{% endhighlight %}

### style.css
{% highlight css %}
div {
    font-size: 2.0em;
}
{% endhighlight %}

### app.js
{% highlight javascript %}
$(document).ready(function() {
    $.get('http://localhost:3000', function(resp) {
        var data = JSON.parse(resp);
        $('div').html('Response from server says that name is ' + data.name);
    });
});
{% endhighlight %}

Run this front-end by opening the `index.html` file in a browser. It should display the one-line html we've coded.

(For Cloud9 users, remember to set the url in the `$.get()` AJAX call to `https://your-workspace-name.c9users.io/` ).

## References &amp; Resources

- [NodeJS](https://nodejs.org/)