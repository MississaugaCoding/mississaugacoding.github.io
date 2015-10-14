---
layout: post
title: "HTML/CSS/JS - More Q&A & Review"
comments: true
publish: true
---

This week we continued to answer some general questions regarding the HTML/CSS/JavaScript topics covered so far.

Here are some interesting points that came up during the session.


**How do I centre images on my web page?**

The temptation is to use the `<center>` tag but this is deprecated in HTML5 as clearly explained [here](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/center) and [here](http://www.w3schools.com/tags/tag_center.asp.).

The recommended way is to use CSS, such as:

{% highlight css %}
img.myimage {
    display: block;
    margin-left: auto;
    margin-right: auto; 
}
{% endhighlight %}

This assumes your HTML looks something like: `<img class="myimage" src="pic.jpg" alt="My Picture" />`. Note the class attribute there.

See [here](http://www.w3.org/Style/Examples/007/center.en.html#block) for more about how to centre elements on a web page. 


