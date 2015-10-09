---
layout: post
title: "HTML/CSS/JS - Q&A, Review & Practice"
comments: true
publish: true
---

This week we took the time to review some of the HTML/CSS/JavaScript topics covered so far, and to answer any related questions.

Here are some specific points of interest that came up during the session, together with any relevant example code snippets and resource links.


**Can I re-size images dynamically or do they have to be cropped/resized before I use them?**

Images can be resized on the fly through CSS, using the `height` or `width` properties. For example:

{% highlight css %}
img {
    height: 75px;
}
{% endhighlight %}

{% highlight css %}
img {
    width: 50%;
}
{% endhighlight %}

Be aware that setting both `height` and `width` can mess up the aspect ratio of the image, particularly if you set these to fixed pixel values.

However, note also that cropping the image to the required size beforehand may save both bandwidth (and therefore improve page loading time), as well as extra work by the browser engine to resize the image once it's downloaded. Image quality may also degrade on resizing dynamically. 

All told, it is probably best to prepare image content of the right size and quality beforehand.


**What's the difference between a `<span>` and a `<div>`?**

By default, a `<span>` is an inline element while a `<div>` is a block element. 

A block element normally starts on a new line and takes up the whole width of the viewport, whereas an inline element normally does not. 

Note that the default behaviour for both block and inline elements can be modified by setting CSS rules.

[More about HTML block & inline elements here.](http://www.w3schools.com/html/html_blocks.asp)


**Should I use `==` or `===` in an if-statement condition?**

The equality operator `==` compares value while the identity (or strict equality) operator `===` compares both value and type. For example:

{% highlight javascript %}
var x = 1;
x == '1'  // true because comparing values of 1
x === '1' // false because comparing a numeric value of 1 to a string value of '1'
{% endhighlight %}

This concept is also common in other programming languages.

[More about comparison operators here.](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comparison_Operators)


**Defining a JavaScript function as a variable - pros and cons?**

In other words, function declarations vs. function expressions. 

The jury may still be out on this one, but one thing to keep in mind is that function declarations get hoisted whereas function expressions do not.

To illustrate:

{% highlight javascript %}

// invoking function 'foo' before defining it
// works because the function is defined with 
// a function declaration, which gets 'hoisted'
foo();   


// invoking function 'bar' before defining it
// does not work because the function is defined
// with a function expression, which does not
// get 'hoisted'
bar();


function foo() {
    alert('called foo');
}


var bar = function() {
    alert('called bar');
}

{% endhighlight %}

In fact, if you run this script with the console on (F12), it gives an `Uncaught TypeError: bar is not a function`.

Here is a more [in-depth article](http://www.adequatelygood.com/JavaScript-Scoping-and-Hoisting.html) on the subject.


**How do I know what JavaScript features are supported in my browser?**

JavaScript is currently in its ES5 (ECMAScript 5) version with some of the most recent browser editions beginning to support features from ES6 (aka Harmony), although this latest standard is not fully supported by any browser yet.

Web sites like [Mozilla Developer Network](https://developer.mozilla.org/en-US/) and [W3 Schools](http://www.w3schools.com) give a good indication of browser compatibility for the various HTML/CSS/JavaScript elements, attributes, properties and functions. Another good site to peruse for this purpose is [Can I Use](http://www.caniuse.com).


**What technologies are involved in web applications? What should I learn?**

This [talk by Will Stern](https://www.youtube.com/watch?v=pB0WvcxTbCA) of LearnCode.Academy gives an up-to-date view on the must-knows and nice-to-knows, as well as some great insights into where web development is headed.

A quick tip on setting up a development environment, especially for people who cannot install (or couldn't be bothered to install) all the different bits and pieces on their (work?) laptop: check out [Cloud9](http://c9.io). It gives you a complete (free) IDE, editor, support for all the main web programming languages, database, GitHub integration, everything you'll need to experiment and try things out, all running in your browser.












