---
layout: post
title: HTML/CSS/JS - Intro Session 2
comments: true
publish: true
--- 

This week we will continue covering the basic concepts of HTML, CSS and JavaScript.

We will introduce new HTML tags and CSS properties, before touching on some JavaScript as well.

This is where we left off our HTML and CSS files:

### index.html
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

### style.css
{% highlight css %}
p {
    color: blue; /* or whichever colour you chose */
}
{% endhighlight %}

### Some more CSS properties

Here are some more CSS properties we can use to further style our solitary paragraph.

{% highlight css %}
font-size 
font-family
font-weight
text-align
border
padding
{% endhighlight %}

### Two more HTML elements: Drop-downs & Buttons

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

There are many, many more HTML element tags and CSS properties, each with their own attributes and settings respectively.

Some other, very commonly used HTML elements include:

  - _a_
  - _ul_ , _li_
  - _input_
  - _div_
  - _h1_ through _h6_
  - _img_
  - _table_

 
These resource links are provided for your perusal:

- [Mozilla HTML Reference](https://developer.mozilla.org/en/docs/Web/HTML/Element)
- [Mozilla CSS Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference)