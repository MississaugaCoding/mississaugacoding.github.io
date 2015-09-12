---
layout: post
title: "HTML/CSS/JS - Extended - Part II"
comments: true
publish: true
---

##Overview

Last week we went over some important aspects of JavaScript and applied them in our Calculator. We also went over new HTML elements and explained the difference between in-line and block elements. This session, we will explain how CSS deals with HTML elements by providing their `id` and/or `class` attributes. We also see how JavaScript can minpulate CSS in a better sense. 

##Previous Code

Everything we cover during the sessions are pushed onto [Github](https://github.com/). You can find the code [here](https://github.com/MississaugaCoding/example-html-css-js).

##CSS

Let's go ahead and design our page a little bit. This is what we already have:

{%highlight css%}
p{
    color: blue;
    font-size: 1.5em; 
    font-family: Verdana;
    font-weight: bold;
    text-align: center;
    border: 2px solid silver;
    padding: 4px;
}
{%endhighlight%}

The tag `p` targets all the `<p></p>` elements in our HTML page. This is useful if you want to set a default style for certain HTML elements. But what if we want to specify what we want to style? What if we want to override current styling? 

Something important to understand is that there are two HTML attributes that can be used to help select the elements we want. It is also important to name them in a meaningful way. These two attributes are `id` and `class`.

`id` is usually used to identify individual elements, and `class` is used to group elements together. Both attributes can be used on the same element, but you cannot have more than one of each on the same element.

example: 
{%highlight html%}
<p id="first-heading" class="headings">My Heading</p>
{%endhighlight%}

So what do we have now? In our `index.html`, we have an `id` called `calculator-container` on our `div` element. Let's try and style it.

{%highlight css%}
#calculator-container{
	border: 3px solid purple;
	margin: 50px;
	padding: 20px;
}
{%endhighlight%}

Nothing new, all we did was to add a border and add some spacing from out of the border using `margin` property and space from the inside using the `padding` property. **One thing to notice here how we specified the element using the `#`sign. This is used to capture an `id` whereas the dot (`.`) sign is used to capture a class.**

Let us try to **override** one of our `p` elements, `calculator-heading`. 

{%highlight css%}
#calculator-heading{
	color: black;
	font-size: 1em;
	text-align: left;
	border-width: 10px;
	padding: 15px;
}
{%endhighlight%}

Notice how we used the same properties in here and only modified the **border width** and nothing else.

All good, let's deal with classes now. We have `calculator` and we will need to identify it using the dot notation. 

{%highlight css%}
.calculator{
	border: 2px dashed purple;
	padding: 15px;
	text-align: left;
	font-size: 0.8em;
}
{%endhighlight%}

But this doesn't make sense since we are only applying the styling to one element. So let's change something in our `index.html`.

{%highlight html%}
<p class="result-container">
    Result is: <span id="result"></span>
</p>
{%endhighlight%}

to this

{%highlight html%}
<p class="calculator" id="result-container">
    Result is: <span id="result"></span>
</p>
{%endhighlight%}

Now we are applying our styling in two parts. 

##JavaScript Manipulation

We know how to deal with id's and classes. Let's make our JavaScript take part with our display. That is, modifying the CSS of our page based on some events.

First, let's modify our `style.css`.
{%highlight css%}
#result-container{
	display: none;
}
{%endhighlight%}

This will hide our HTML element. In our `script.js`, we will display our html tag after we obtain our result.

In our **executeCalculator** method, add these lines in the very end:
{%highlight js%}
var resultContainer = document.getElementById('result-container');
resultContainer.style.display = "block";
resultContainer.style.borderStyle = "solid";
resultContainer.style.borderColor = "red";
{%endhighlight%}

That's it! 