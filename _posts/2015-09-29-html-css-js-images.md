---
layout: post
title: "HTML/CSS/JS - Images"
comments: true
publish: true
---

It is said a picture speaks a thousand words, so it's no surprise that adding images to a web page is a very common requirement.

This week we will explore ways of coding image content, including regular images, backgrounds, and loading images automatically as the viewer scrolls the page.

In addition to using the HTML/CSS/JavaScript code concepts we've discussed so far, we'll discover some new tags, properties and commands, including:

- HTML 
  - `img` tag

- CSS properties
  - `transform`
  - `opacity`
  - `background-image`, `background-size`, `background-attachment`, `background-repeat`

- JavaScript 
  - `offsetHeight` (height of the element including vertical padding and borders, in pixels)
  - `window.pageYOffset` (number of pixels that the document has already been scrolled vertically)
  - `window.innerHeight` (the inner height in pixels of the browser window or viewport)
  - using `innerHTML` to modify HTML within an element

##Code - Full Background Image

###index.html
{% highlight html %}
<!doctype html>
<html>
    <head>
        <title>Full Background Image</title>
        <link rel="stylesheet" href="./public/css/style.css" type="text/css" />
    </head>
    <body>
        
        <nav>
            <a href="#sect1">Home</a>
            <a href="#sect2">About</a>
            <a href="#sect3">Contact Us</a>
        </nav>
        
        <div class="content" id="sect1">
            <img src="./public/images/smallphoto2.jpg"></img>
            <p class="text">Home text Lorem ipsum dolor sit amet, consec tetur adipisicing elit. Officiis, suscipit, ullam eum voluptate conseq uatur minima adipisci aliquid molestiae 
            </p>
        </div>
        
        <div class="content" id="sect2">
            <p class="text">About Lorem ipsum dolor sit amet, consectetur adipisicing elit. Vero, vitae, obcaecati, sequi, exercitationem culpa impedit perferendis eos voluptas aperiam perferendis eos voluptas.</p>
        </div>
        
        <div class="content" id="sect3">
            <p class="text">Contact Lorem ipsum dolor sit amet, consectetur adipisicing elit. Vero, vitae, obcaecati, sequi, exercitationem culpa impedit perferendis eos voluptas aperiam facilis error beatae ad eveniet in animi exp licabo eos voluptas.</p>
        </div>
       
    </body>
</html>
{% endhighlight %}

###public/css/style.css
{% highlight css %}
* {
    margin:0;
}

html, body {
    height: 100%;
    font-family: Georgia;
    font-size: 1.5em;
}

.content img {
    float:left;
    margin: 0;
    padding: 150px 15px 0px 150px;
}

.content {
    height: 100%;
    background-repeat: no-repeat;
    background-attachment: fixed;
    background-size: cover;
}

p {
    padding: 150px;
    font-style: italic;
    color: beige;
}

nav {
    position: fixed;
    width: 100%;
    height: 70px;
    background-color: black;
    opacity: 0.5;
}

nav a {
    text-decoration: none;
    color: white;
    margin-left: 30px;
    line-height: 70px;
}

nav a:hover {
    text-decoration: underline;
}

/*
Assumes the existence of image files
under folder /public/images/
*/

#sect1 {
    background-image: url("../images/photo1.jpg");
    
}  

#sect2 {
    background-image: url("../images/photo2.jpg");
}
#sect3 {
    background-image: url("../images/photo3.jpg");
}
{% endhighlight %}


##Code - Auto-load Image Content

###index.html
{% highlight html %}
<!DOCTYPE html>
<html>
    <head>
        <title>Auto-Loading Content</title>
        <link rel="stylesheet" href="./public/css/style.css" type="text/css" />
    </head>
    <body>
        
        <div class="content">
           
           <img src="./public/images/smallphoto1.jpg" />
           <p class="text">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Vero, vitae, obcaecati, sequi, exercitationem culpa impedit perferendis eos voluptas aperiam facilis error beatae ad eveniet in animi explicabo repudiandae veritatis atque tenetur sed dolorum praesentium porro temporibus minima excepturi accusamus non odio labore reprehenderit repellat. Lorem ipsum dolor sit amet, consectetur adipisicing elit. Vero, vitae, obcaecati, sequi, exercitationem culpa impedit perferendis eos voluptas. Lorem ipsum dolor sit amet, consectetur adipisicing elit. Vero, vitae, obcaecati, sequi, exercitationem culpa impedit perferendis eos voluptas aperiam facilis error beatae ad eveniet in animi explicabo 
           </p>
           
           <img src="./public/images/smallphoto2.jpg" />
           <p class="text">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Vero, vitae, obcaecati, sequi, exercitationem culpa impedit perferendis eos voluptas aperiam facilis error beatae ad eveniet in animi explicabo repudiandae veritatis atque tenetur sed dolorum praesentium porro temporibus minima excepturi accusamus non odio labore reprehenderit repellat. Lorem ipsum dolor sit amet, consectetur adipisicing elit. Vero, vitae, obcaecati, sequi, exercitationem culpa impedit perferendis eos voluptas. Lorem ipsum dolor sit amet, consectetur adipisicing elit. Vero, vitae, obcaecati, sequi, exercitationem culpa impedit perferendis eos voluptas aperiam facilis error beatae ad eveniet in animi explicabo 
           </p>

        </div>
       
        <!-- custom JavaScript --> 
        <script type="text/javascript" src="./public/js/script.js"></script>
    </body>
</html>
{% endhighlight %}

###public/css/style.css
{% highlight css %}
/*
Assumes the existence of image files
under folder /public/images/
*/

html {
    background-image: url("../images/photo1.jpg");
    background-repeat: no-repeat;
    background-attachment: fixed;
    background-size: cover;
}

body {
    font-family: Georgia;
    font-size: 1.5em;
}

p {
    padding: 20px;
    font-style: italic;
    color: beige;
}

img {
    margin: 0;
    padding: 20px;
}
{% endhighlight %}

###public/js/script.js
{% highlight javascript %}
window.addEventListener('scroll', checkScrolling);
var con = document.querySelector('.content');

function checkScrolling() {
    
    // height of the element including vertical padding 
    // and borders, in pixels
    var contentHeight = con.offsetHeight;      
	
	// number of pixels that the document has already
	// been scrolled vertically
	var scrolled = window.pageYOffset  ;       
	
	// the inner height of the browser window
	var yPos = scrolled + window.innerHeight;  
	
	// this if statement detects whether we have
	// scrolled to the end of the page
	if ( yPos >= contentHeight ) {
	    
	    /*
	    The code below is meant to show a quick way of adding in 
	    some new content. Though it works and serves the purpose, 
	    it is meant just as a demo. Typically here one would
	    code an AJAX call to some sort of backend web service
	    API, that would then create the new content and inject
	    it dynamically.
	    */
	    
	    con.innerHTML += '<p>some added text content'+yPos+'</p>';
		
		// assumes images stored under folder /public/images/
		con.innerHTML += '<img src="./public/images/smallphoto3.jpg" />';
		con.innerHTML += '<img src="./public/images/smallphoto4.jpg" />';
		con.innerHTML += '<img src="./public/images/smallphoto5.jpg" />';
        
	}
}
{% endhighlight %}


##References &amp; Resources

- [HTML img](http://www.w3schools.com/tags/tag_img.asp)
- [CSS transform](http://www.w3schools.com/cssref/css3_pr_transform.asp)
- [CSS background](http://www.w3schools.com/css/css_background.asp)
- [CSS opacity](http://www.w3schools.com/css/css_image_transparency.asp)
- [JavaScript offsetHeight](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/offsetHeight)
- [JavaScript window.pageYOffset](http://www.w3schools.com/jsref/prop_win_pagexoffset.asp)
- [JavaScript window.innerHeight](https://developer.mozilla.org/en-US/docs/Web/API/Window/innerHeight)
- [JavaScript innerHTML ](http://www.w3schools.com/js/js_htmldom_html.asp)
- [Unsplash.com for royalty/watermark-free hi-res images](http://unsplash.com)

