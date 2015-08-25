---
layout: post
title: HTML/CSS/JS - Intro Session 2
comments: true
publish: false
---

This week we will continue covering the basic concepts of HTML, CSS and JavaScript.

We will introduce new HTML tags, CSS properties and touch on some JavaScript as well.

This is where we left our HTML and CSS files last week:

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

    </body>

</html>
{% endhighlight %}

###style.css
{% highlight css %}
p {
    color: blue; /* or whichever colour you chose */
}
{% endhighlight %}

###Some more CSS properties

Here are some more CSS properties we can use to further style our solitary paragraph.

{% highlight css %}
font-size 
font-family
font-weight
text-align
border
padding
{% endhighlight %}

###Two more HTML elements: Drop-downs & Buttons

Drop-downs, also known as combo-boxes or select boxes, give the user a predefined set of choices.

{% highlight html %}
<select>
  <option value="S">Small</option>
  <option value="M">Medium</option>
  <option value="L">Large</option>
</select>
{% endhighlight %}

Buttons are another common element on web pages.

{% highlight html %}
<button>Click Me Now</button>
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

The _id_ and _class_ attributes allow us to refer to a specific HTML element or element(s).

 - let us refer to our HTML elements in CSS and in JavaScript.
 

###Let's introduce some JavaScript into the mix

As we did in the case of CSS, we need to let our HTML know about our JavaScript.

{% highlight html %}
<script src="script.js"></script>
{% endhighlight %}

####Variables

Here's how a variable is defined in JavaScript.

{% highlight javascript %}
var empName = 'Jane Doe';
var empExt = 4279;
alert(empName);
alert(empExt);
alert('Name:' + empName + '  Ext:' + empExt);
{% endhighlight %}

Note:

  - the word _var_
  - variable assignment
  - naming rules
  - case-sensitive
  - common simple types: numeric, string, boolean

####Built-in functions

_alert()_ is a JavaScript function.

Another built-in function is _getElementById()_ 
- fetches an HTML element from our page so we can do something to it, e.g. style it dynamicallyAnother

{% highlight javascript %}
var myElem = document.getElementById('mytext');
{% endhighlight %}

Note:

  - dot notation as in _document._
 

####Programmer-defined functions

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

Functions can be called either within the JavaScript code itself or via ....

####Event Listeners

{% highlight javascript %}
var btn = document.getElementById('myButton');
btn.addEventListener('click', myFunction);
{% endhighlight %}

The above two lines of JavaScript code

  - get the button element from the HTML document and save it to a variable
  - tells the browser to execute myFunction when the button is clicked

In JavaScript we can also dynamically, on the fly, apply styling to an element, for example:

{% highlight javascript %}
document.getElementById('mytext').style.fontSize = '50px';
{% endhighlight %}

As an exercise, add to our example web page the facility to 

  - choose a colour from a drop-down and 
  - set the text of our paragraph to be displyed in that colour.


####Additional Resource Links
- [W3Schools JavaScript Tutorial](http://www.w3schools.com/js/)
- [Mozilla JavaScript Guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide)