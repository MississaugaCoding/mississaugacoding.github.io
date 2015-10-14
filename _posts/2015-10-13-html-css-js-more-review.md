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


**What's this Cloud9 you keep harping on about?**

[Cloud9](http://c9.io) offers a free, easy-to-use, complete virtual IDE (Integrated Development Environment). 

It can be used for all the major open-source web development languages including HTML, CSS, JavaScript, PHP and others. It even provides database servers and tools such as MySQL, MongoDB, and PostgreSQL. Every workspace comes with its own virtual Apache web server instance, and it also includes terminal access (a Linux shell prompt) through which one can install other tools, libraries etc. as needed. 

Cloud9 also integrates nicely with GitHub (about which more later, hopefully). 

Why use an online IDE? For one thing, there’s nothing to install and configure. Typically, for developing a web-based application you would need to install a bunch of things on your PC, like a decent editor, a web server, database, an FTP client, Git etc., and then switch from one tool to the other as you build and test your application. In Cloud9 all the development tools you need are grouped and easily accessible in one place - your web browser. 

Secondly, an online IDE gives you a portable development environment on which to work virtually anywhere, at any machine as long as there’s a decent browser and a decent Internet connection. No need to worry about synchronising the various copies of code (for example, at work, at home, on a PC, on a laptop) - just one accessible, up-to-date version in the cloud.

It is important to point out what the Cloud 9 IDE is not: it is not a production grade server and it is not a substitute for web hosting. It is mainly a sandbox where you can try things out, learn, experiment, test and play, with all the tools and toys you would normally need, all made accessible from one central interface.

Check out the [Cloud9 documentation](https://docs.c9.io/docs/).







