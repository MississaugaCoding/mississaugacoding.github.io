---
layout: post
title: HTML/CSS/JS - Intro Session 2
comments: true
publish: true
---

This week we will continue covering the basic concepts of HTML, CSS and JavaScript.

We will introduce new HTML tags, CSS properties and touch on some JavaScript as well.

This is where we left our HTML and CSS files last week:

**index.html**
{% highlight html %}
<!doctype html>
<html>

    <head>
    
        <title>My Web Page</title>
        
    </head>

    <body>
 
        <!-- some comment --> 
        <p>Some text on my web page</p>

    </body>

</html>
{% endhighlight %}

**style.css**
{% highlight css %}
p {
    color: purple; /* or whichever colour you chose */
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

Two very important HTML attributes to know about, and use, are: id and class

{% highlight html %}
<p  id="mytext" > Some text on my web page </p>
{% endhighlight %}

The 'id' attribute allows us to (optionally) give a unique identifier to any HTML element on our web page.

The 'class' attribute is very similar but for a group of HTML elements.

Both these attributes allow us to refer to a specific HTML element or element(s).

Why that is important will be made apparent in a few minutes, but first...

###Let's introduce some JavaScript into the mix

_Variables_

A key concept in any programming langauge is the concept of variables. Here's how a variable is defined in JavaScript.

{% highlight javascript %}
var myVar = 'some value';
alert(myVar);
{% endhighlight %}

_Built-in functions_

{% highlight javascript %}
var myElem = document.getElementById('mytext');
{% endhighlight %}

Note:

  - variable assignment
  - naming rules
  - alert() is a JS built-in function 
  - dot notation as in document.
  - getElementById() another built-in function

_Programmer-defined functions_

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

