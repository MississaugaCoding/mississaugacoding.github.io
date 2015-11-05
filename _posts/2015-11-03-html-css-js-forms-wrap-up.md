---
layout: post
title: "HTML/CSS/JS - Forms Wrap-up"
comments: true
publish: true
---

This week we wrapped up our discussion about forms by looking at some other frequently used modes of form input, such as drop-downs, radio buttons and checkboxes. 

Here is the finalised, and working, example code:

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
        <input id="fullname" type="text" name="fullname"/><br/>
        
        City:<br/>
        <select name="city">
          <option value="MI">Mississauga</option>
          <option value="BR">Brampton</option>
          <option value="TO">Toronto</option>
        </select><br/>
        
        Gender:<br/>
        
        <input id="mgender" type="radio" name="gender" value="M"/>
        <label for="mgender">Male</label>
        
        <input id="fgender" type="radio" name="gender" value="F"/>
        <label for="fgender">Female</label>
        <br/>
        
        Language:<br/>
        <label>
          <input type="checkbox" name="english" value="EN"/>English
        </label>
        <label>
          <input type="checkbox" name="french" value="FR"/>French
        </label>
        <label>
          <input type="checkbox" name="other" value="OT"/>Other
        </label>
        
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
var frm = document.getElementById('myform');
var btn = document.getElementById('btnSave');
var msg = document.getElementById('msg');
var fld = document.getElementById('fullname');
fld.focus();

btn.addEventListener('click', submitForm);

function submitForm() {

    msg.innerHTML = '';
    
    if ( fld.value === '' ) {
        
        msg.innerHTML = 'Please enter a name.';
        fld.focus();  // places cursor in the form field
        
    } else {
        
        // prepare the form data
        var data = new FormData(frm)
        
        // AJAX request
        // create
        var xhr = new XMLHttpRequest();
        
        // open
        xhr.open('post', 'backend/savedata.php', true);
        
        // send
        xhr.send(data);
        
        // a better way would be to add an event listener 'readystatechange' on xhr
        // but this will do for now...
        msg.innerHTML = 'Record has been saved.';
        frm.reset();  // clears the form for next input
        fld.focus();
    }
    
}
{% endhighlight %}

###backend/savedata.php
{% highlight php %}
<?php

// fetch POSTed data
// possibly fetch other fields here
$name = filter_input(INPUT_POST, 'fullname');
$city = filter_input(INPUT_POST, 'city');
$gender = filter_input(INPUT_POST, 'gender');

$english = filter_input(INPUT_POST, 'english');
$french = filter_input(INPUT_POST, 'french');
$other = filter_input(INPUT_POST, 'other');

$lang = trim($english . " " . $french . " " . $other);

// connect to the database
// ** replace connection parms according to your set-up **
$dbConn = mysqli_connect("127.0.0.1", "username", "password", "dbname", 3306);

// prepare insert sql statement 
// possibly add other fields to insert and bind
$sqlInsert = "INSERT INTO `person` (`fullname`,`city`, `gender`, `language`) VALUES (?,?,?,?)";
$stmt = mysqli_prepare($dbConn, $sqlInsert);
mysqli_stmt_bind_param($stmt, 'ssss', $name, $city, $gender, $lang);

// execute the insert sql statement 
mysqli_stmt_execute($stmt);

// close statement and connection 
mysqli_stmt_close($stmt);
mysqli_close($dbConn);

exit();
{% endhighlight%}

We also talked about troubleshooting some common JavaScript mishaps, and using Chrome Dev Tools (F12) to help find and resolve them. These common errors include:

- mismatched id references, between HTML `id` attribute and JavaScript `getElementById`
- misspelt JavaScript function calls e.g. `XMLHttpRequest` not `XMLHTTPRequest` and `innerHTML` not `innerHtml`
- wrong CSS stylesheet file name / JavaScript file name 

In all these cases, keep in mind case-sensitivity.

A couple of other points relevant to getting the final version to work:

1. Make sure the line that does the INSERT in your PHP file is not commented out! I doubt that would be the case in anyone else's code, and I still have no idea why it was commented out in mine, but it was. As a result, nothing was being saved to the database, obviously.

2. No spaces in HTML attributes, e.g. `id="myform"` not `id = "myform"`

3. Backticks vs. quotes. Make sure the field names in the INSERT statement (in the PHP file) are enclosed in backticks, not in quotes. It's an SQL thing.


##References &amp; Resources

- [HTML drop-downs (select,option)](http://www.w3schools.com/tags/tag_select.asp)

- [HTML radio buttons](http://www.w3schools.com/html/tryit.asp?filename=tryhtml_radio)

- [HTML checkboxes](http://www.w3schools.com/html/tryit.asp?filename=tryhtml_checkbox)


