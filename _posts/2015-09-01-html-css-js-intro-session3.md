---
layout: post
title: HTML/CSS/JS - Intro Session 3
comments: true
publish: true
--- 

As we continue covering the basic concepts of front-end web development, the main focus this week will be JavaScript.

This is where we left off our HTML and CSS files, more or less:

###index.html
{% highlight html %}
<!doctype html>
<html>

    <head>
    
        <title>My Web Page</title>
        <link rel="stylesheet" href="style.css" /> 
        
    </head>

    <body>
 
        <!-- some comment -->  
        <p>Some text on my web page</p>

        <!-- drop-down or combo-box with pre-defined options -->
        <select>
            <option value="S">Small</option>
            <option value="M">Medium</option>
            <option value="L">Large</option>
        </select>

        <!-- just a button -->
        <button>Click Me Now</button>

    </body>

</html>
{% endhighlight %}

###style.css
{% highlight css %}
p {
    color: blue;
    font-size: 1.5em; 
    font-family: Verdana;
    font-weight: bold;
    text-align: center;
    border: 2px solid silver;
    padding: 4px;
}
{% endhighlight %}

A very important HTML attribute to know about, and use, is _id_.

{% highlight html %}
<p  id="mytext" > Some text on my web page </p>
{% endhighlight %}

{% highlight html %}
<button id="myButton" >Click Me Now</button>
{% endhighlight %}

The _id_ attribute lets us give a unique identifier to any HTML element on our web page.

The _class_ attribute is very similar but for a group of HTML elements.

The _id_ and _class_ attributes are useful because they allow us to refer to specific HTML element or element(s) from our CSS and from our JavaScript.
 

###So, finally, let's talk some JavaScript

As we did in the case of CSS, we need to let our HTML document know about our JavaScript code.

{% highlight html %}
<script src="script.js"></script>
{% endhighlight %}

Note:

  - can be placed in either _<head>_ or _<body>_ sections
  - rule of thumb: 
    - 3rd party libraries in _<head>_ section
    - custom JavaScript in _<body>_ section 
      -  e.g. just before _</body>_ to ensure elements referenced have been rendered 
  

<p class="ul">Variables:</p>

Here's how a variable is defined in JavaScript.

{% highlight javascript %}
var empName = 'Jane Doe';
var empExt = 4279;
{% endhighlight %}

Note:

  - the keyword _var_
  - variable assignment operator
  - naming rules and conventions
    - letters, numbers, _ , $
    - cannot start with a number
    - meaningful
    - camel-case
  - **case-sensitive**
  - common simple types: numeric, string, boolean

<p class="ul">Built-in functions:</p>

_alert()_ is a built-in JavaScript function. 

- display values of variables and expressions
- crude but useful tool for a quick check/test

{% highlight javascript %}
alert(empName);
alert(empExt);
alert('Name:' + empName + '  Ext:' + empExt);
{% endhighlight %}

Another built-in JavaScript function is _getElementById()_ 

- fetches an HTML element from our page so we can do something to it, e.g. to style it dynamically

{% highlight javascript %}
var myElem = document.getElementById('mytext');
myElem.style.fontSize = '50px';
{% endhighlight %}

Note:

  - dot notation as in _document._ and _style.fontSize_
 

<p class="ul">Programmer-defined functions:</p>

{% highlight javascript %}
function myFunction() {
  var a = 123;
  alert(a);
}
{% endhighlight %}

Note the difference between defining a function and executing it.

The above defines a function, but to actually call it we need to add:

{% highlight javascript %}
myFunction();
{% endhighlight %}

Functions can also be called via ...

<p class="ul">Event Listeners:</p>

In JavaScript we can watch for particular events and react to them.

- to watch out ("listen") for particular UI event (e.g. click) on particular element (e.g. button)
- to execute some code (e.g. handler function) whenever that event occurs 

{% highlight javascript %}
var btn = document.getElementById('myButton');
btn.addEventListener('click', myFunction);
{% endhighlight %}

The above two lines of JavaScript code

  - get the button element from the HTML document and save it to a variable
  - tells the browser to execute myFunction when the button is clicked

As an exercise, let's add to our example web page the facility to: 

  - choose a colour from a drop-down and 
  - set the text of our paragraph to be displayed in that colour.

Suggested steps:

- make sure each element has a unique id
- get the button element
- add an event listener so that button click would call a function
- create the function
- get the selected colour
- get the paragraph element
- apply the colour to the paragraph element
 

Sample solution:

###index.html
{% highlight html %}
<!DOCTYPE html>
<html>
    <head>
        <title>My Web Page</title> 
        <link rel="stylesheet" href="style.css" />  
    </head>
    <body>
    
        <!-- All elements have been given an id attribute -->
        <!-- To enable us to refer to elements from Javascript -->
        
        <p id="myText">Some text on my web page</p>
        
        <select id="selColour">
            <option value="blue">Blue</option>
            <option value="black">Black</option>
            <option value="red">Red</option>
            <option value="green">Green</option>
            <option value="yellow">Yellow</option>
        </select>
        
        <button id="btnColour">Make It So!</button>
        
        <!-- Script tag brings in Javascript into our HTML. -->
        <!-- Placed here to make sure all referenced --> 
        <!-- elements have already been defined.     -->
        <script src="script.js"></script>
        
    </body>
</html>
{% endhighlight %}

###script.js
{% highlight javascript %}
// get button element 
var btn = document.getElementById('btnColour');

// set up an event listener on button element 
// this means whenever user clicks the button, 
// call the function applyColour() 
btn.addEventListener('click', applyColour);

// function to change the colour of our paragraph text
function applyColour() {
    // get the comb-box element
    var sel = document.getElementById('selColour');
    var col = sel.value; // get the selected value
    
    // get the paragraph element
    var par = document.getElementById('myText');
    par.style.color = col;   // style paragraph text colour
}
{% endhighlight %}

No changes to style.css were required at all.

###Additional Resource Links
- [W3Schools JavaScript Tutorial](http://www.w3schools.com/js/)
- [Mozilla JavaScript Guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide)