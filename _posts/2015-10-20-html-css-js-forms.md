---
layout: post
title: "HTML/CSS/JS - Forms"
comments: true
publish: true
---

Whether it's a log-in screen, online questionnaire or contact page, forms are a very common occurrence on the worldwide web.

This week we'll have a look at coding a simple form, submitting it, performing some basic input validation, and saving the data entered into a database.  

To make the excercise useful, the plan is to cover both the front-end and back-end aspects of this topic. By back-end we mean the part where we actually send the input data out to the server, and save that data in the database. 

In order to be able to follow along and get the most out of this session, you may want to install something like [WampServer](http://www.wampserver.com/en/) on your laptop ahead of the session. This gives you the server and database pieces of the puzzle.

Alternatively, and probably much easier, you may want to [sign up free onto Cloud9](https://c9.io/web/sign-up/free) as suggested in [this blog post](http://mississaugacoding.github.io/2015/10/06/html-css-js-review/) from some weeks ago. More details as to what Cloud9 is (and is not) can be found [here](http://mississaugacoding.github.io/2015/10/13/html-css-js-more-review/) and officially [here](https://docs.c9.io/docs/).

Unfortunately we did not get enough time to finish going through the example. Next week we will review what we did this week and continue where we left off.

This is the code as we left it. <strong>Please note that this is not a final, complete solution. It's just where we left off.<strong>

###index.html
{% highlight html %}
<!doctype html>
<html>
  <head>
    <title>Forms</title>
    <link rel="stylesheet" href="./public/css/style.css" type="text/css" />
  </head>
  <body>
    
    <div id="main">
      
      <form id="myform" method="post">
        
        Full Name:<br/>
        <input id="fullname" type="text" name="fullname" />
        
        <br/><br/>
        <input type="button" id="btnSave" value="Save"/>
        
      </form>
      
    </div>
    
    <br/><br/>
    <div id="msg"></div>
    
    
    <script type="text/javascript" src="./public/js/script.js"></script>
  </body>
</html>
{% endhighlight %}

###script.js 
{% highlight javascript %}
var btn = document.getElementById('btnSave');
var fld = document.getElementById('fullname');
var msg = document.getElementById('msg');
var frm = document.getElementById('myform');

btn.addEventListener('click', submitForm);

function submitForm() {
    
    msg.innerHTML = '';  
    
    if ( fld.value==='' ) {
        
        msg.innerHTML = 'Please key in a name.';
        
    } else {
        
        
        /* THIS SECTION OF THE CODE HAS YET TO BE COMPLETED  */
        
        // prepare form data
        var data = new FormData(frm);
        
        // send data to server via AJAX request to server
        // create
        var xhr = new XMLHttpRequest();
        
        // open     --- TO BE CONTINUED ---
        //xhr.open(  need arguments here   );
        
        // send data
        //xhr.send(data);
        
    }
    
}
{% endhighlight %}

###style.css
{% highlight css %}
div#msg {
    color:red;
}
{% endhighlight %}


Meanwhile, to help you prepare, here is the back-end SQL code for creating the database table, and the PHP code for saving the form data to that table:

###SQL to create database table
{% highlight sql %}
CREATE TABLE IF NOT EXISTS `person` (
  `id` int(10) unsigned NOT NULL AUTO_INCREMENT,
  `fullname` varchar(50) DEFAULT NULL,
  `gender` char(1) DEFAULT NULL,
  `city` varchar(50) DEFAULT NULL,
  `language` varchar(50) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 AUTO_INCREMENT=1 ;
{% endhighlight %}


###backend/savedata.php
{% highlight php %}
<?php

// fetch POSTed data
// possibly fetch other fields here
$name = filter_input(INPUT_POST, 'fullname');

// connect to the database
// ** replace connection parms according to your set-up **
$dbConn = mysqli_connect("127.0.0.1", "user", "pass", "dbname", 3306);

// prepare insert sql statement 
// possibly add other fields to insert and bind
$sqlInsert = "INSERT INTO `person` (`name`) VALUES (?)";
$stmt = mysqli_prepare($dbConn, $sqlInsert);
mysqli_stmt_bind_param($stmt, 's', $name);

// execute the insert sql statement 
mysqli_stmt_execute($stmt);

// close statement and connection 
mysqli_stmt_close($stmt);
mysqli_close($dbConn);

exit();
{% endhighlight%}



##References &amp; Resources

- [HTML form Tag](http://www.w3schools.com/tags/tag_form.asp)
- [Form method attribute: post vs. get](http://www.w3schools.com/tags/att_form_method.asp)
- [HTML input Tag](http://www.w3schools.com/tags/tag_input.asp)
- [What's AJAX?](https://developer.mozilla.org/en-US/docs/AJAX/Getting_Started)
- [AJAX Tutorial](http://www.w3schools.com/ajax/default.asp)
- [FormData](https://developer.mozilla.org/en-US/docs/Web/API/FormData/FormData)
- [XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest)



