---
layout: post
title: "HTML/CSS/JS Extended"
comments: true
publish: true
---

##Overview

Last week we covered some new HTML elements and started with JavaScript. For a quick recap, HTML is the static form of a webpage, the CSS is what styles our webpage, and the JavaScript is what manipulates our HTML elements, as well as its CSS.

This week we will revisit what we did in the past two weeks and list other ways of doing the same thing. Also, we will cover more CSS and JavaScript and learn about their best practices.

##Previous Code

This is all the code we covered together, for in-depth explanation of the below snippets, go through [Session 2]({% post_url 2015-08-25-html-css-js-intro-session2 %}) and [Session 3]({% post_url 2015-09-01-html-css-js-intro-session3 %}). 

###index.html

{% highlight html %}
<!doctype html>
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


##Alternative Methods

There are few languages that restrict that way they execute. JavaScript is considered to be flexible compared to other languages. For example our function `applyColour` can be written in 2 other ways: 

**Storing the function in a variable**
{% highlight javascript %}
var btn = document.getElementById('btnColour');

var applyColour = function(){
 	// get the comb-box element
	var sel = document.getElementById('selColour');
    var col = sel.value;
    
    var par = document.getElementById('myText');
    par.style.color = col;
}

btn.addEventListener('click', applyColour);

{% endhighlight %}

Notice: The variable must be declared **before** applying it to the event listener.

**Embedding the function into the event listenener**
{% highlight javascript %}
var btn = document.getElementById('btnColour');

btn.addEventListener('click', function(){
 	// get the comb-box element
	var sel = document.getElementById('selColour');
    var col = sel.value;
    
    // get the paragraph element
    var par = document.getElementById('myText');
    par.style.color = col;
});

{% endhighlight %}

Notice: The drawback from this method is that the function cannot be **reused** somewhere else. In other words, since we didn't store our function in some variable and replaced the variable in the event listener with the function directly, it will only affect the target element. 

Storing the method is useful when you are sure that it will be referenced in more than one place in your script.

##Organizing Files

It is a good habit to organize your files and name them according to their purpose. Also, creating directories to separate the files is important. Therefore, let's keep our `index.html` page in our root directory (where the files are now), and let's create a folder/directory and call it `public`, in that folder create another two and call them `css` and `js`, to store all our CSS and JavaScript respectively. 

Your project file should look something like this now:

{% highlight bash %}
.
├── index.html
├── public
|   ├── css
|   	├── style.css
|   ├── js
|   	├── script.js
{% endhighlight %}

Now we need to edit the path to the CSS and Javascript in our `index.html`

{% highlight html %}
<link rel="stylesheet" href="./public/css/style.css" />
{% endhighlight %}

{% highlight html %}
<script src="./public/js/script.js"></script>
{% endhighlight %}

That's about it! Now let's us dive more into JavaScript

##Operators 

We already covered the **assignment operator** (=) to assign values to variables, now let's talk about **arithmetic operators** ( + - *  / ).

{% highlight javascript %}
var result = (5 + 6) * 10;

alert(result);
{% endhighlight %}

We can use these operators between variables. Let's say we have a percentage that we need to add to our result every time:

{% highlight javascript %}
var startValue = (5 + 6) * 10;

var rateValue = 5;
var ratePercentage = rateValue/100; // 5%  

var result = startValue + (startValue * ratePercentage);

alert(result);

{% endhighlight %}

**Other operators**:

- `=`
- `+=` -> `x += y`
	- Same as `x = x + y`
- `-=` -> `x -= y`
	- Same as `x = x - y`
- `*=` -> `x *= y`
	- Same as `x = x * y`
- `/=` -> `x /= y`
	- Same as `x = x / y`
- `%=` -> x %= y (remainder)
	- Same as `x = x % y`

There is also `x++` and `x--` which is equivalent to `x = x +1` and `x = x - 1` respectively.; 

**Comparison and Logical Operators**:

- `==` 	equal to
- `===`	equal value and equal type
- `!=` 	not equal
- `!==` 	not equal value or not equal type
- `>` 	greater than
- `<` 	less than
- `>=` 	greater than or equal to
- `<=` 	less than or equal to

##Scopes

In JavaScript, scope is the set of variables, objects, and functions you have access to.

To better explain the above statement, let's write down some examples:


**Variable defined outside the function (GLOBAL Variable):**
{% highlight javascript %}

var myName = "John";

function someFunction(){
	alert(myName); //works
}

{% endhighlight %}

**Variable defined inside the function and referenced outside of it (LOCAL Variable):**
{% highlight javascript %}

function someFunction(){
	var myName = "John";
}

alert(myName); //won't work

{% endhighlight %}

**Automatic GLobal** is when the value is assigned to a variable without the `var` object. For example: `x = 9`, anywhere in the script, **even inside the function** (try it out).

**The Lifetime of JavaScript Variables**:

- The lifetime of a JavaScript variable **starts** when it is declared. 
- Local variables are deleted when the function is completed.
- Global variables are deleted when you close the page.

##JavaScript by Example

Now let's learn more about JavaScript by doing a small exercise. Remember our fancy script that deals with percentage? Let's create our own calculator that takes in any value and percentage, and outputs the answer for us.

**Changes to `index.html`:**

- HTML element that takes in a number.
- HTML element that takes in a rate value.
- HTML element that is used to display our final result.

All the styling will go through our `style.css` file in our CSS folder. And all the magic will happen inside our JavaScript file `script.js`.


