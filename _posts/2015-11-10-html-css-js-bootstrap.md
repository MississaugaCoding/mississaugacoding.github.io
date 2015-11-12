---
layout: post
title: "HTML/CSS/JS - Bootstrap & jQuery: A First Look"
comments: true
publish: true
---

Bootstrap bills itself as "the most popular HTML, CSS and JavaScript framework for developing responsive, mobile-first web projects".

Modesty apart, it is primarily a whole bunch of style rules (CSS) that Mark Otto and Jacob Thornton put together while working at Twitter, and which Twitter then decided to share freely with the rest of us.

Bootstrap does include some JavaScript functions, and in fact you would need to include jQuery in your page as well. 

You do not necessarily need to know jQuery to use Bootstrap, but it helps, and knowing jQuery does have its own benefits.

jQuery's claim to fame is "write less, do more". It is a JavaScript library that simplifies (somewhat) what we've been doing so far in plain vanilla JavaScript: get a page element; listen for, and handle, events on that element; modify and/or add page elements, make AJAX calls, and so on. jQuery was originated by John Resig.

In our talk this week we'll explore the reasons why one would use these frameworks, and how to start using them.

Here is the code example we built and discussed during the session.

###index.html
{% highlight html %}
<!doctype html>
<html>

<head>
  <meta name="viewport" content="width=device-width, initial-scale=1">

  <title>Bootstrap Example</title>

  <!-- Bootstrap CSS -->
  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css" />

  <!-- Link for optional custom CSS goes here -->
  <link rel="stylesheet" href="style.css" />

</head>

<body>

  <nav class="navbar navbar-inverse navbar-fixed-top">
    <div class="container-fluid">
      <div class="navbar-header">
        <button type="button" class="navbar-toggle" data-toggle="collapse" data-target="#divMenuList">
          <span class="icon-bar"></span>
          <span class="icon-bar"></span>
          <span class="icon-bar"></span>
        </button>
        <a class="navbar-brand" href="#">My Bootstrap Example</a>
      </div>
      <div id="divMenuList" class="collapse navbar-collapse">
        <ul class="nav navbar-nav">
          <li><a href="#">Home</a></li>
          <li class="dropdown">
            <a class="dropdown-toggle" data-toggle="dropdown" href="#">About<span class="caret"></span></a>
            <ul class="dropdown-menu">
              <li><a href="#">Team</a></li>
              <li><a href="#">Vision</a></li>
              <li><a href="#">Members</a></li>
            </ul>
          </li>
          <li><a href="#">Contact Us</a></li>
        </ul>
      </div>
    </div>
  </nav>

  <div class="container">
      <h3>Some Heading</h3>
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ratione, quis, harum, aliquid natus ab quasi omnis saepe cumque itaque placeat magnam repudiandae iure autem ea necessitatibus accusamus assumenda nesciunt voluptatum facilis
        eligendi odit fugiat tenetur dolorem libero minus provident sequi officiis hic nemo quod quisquam possimus excepturi similique porro fugit voluptatem impedit. Quia, fugiat minus id velit obcaecati quibusdam officia nemo ea. Esse, maiores, sed,
        maxime molestias eos minus cumque in modi quis autem perferendis debitis adipisci provident perspiciatis earum libero corporis asperiores ea. Dicta, nemo, totam, nam rem facilis consequatur commodi quia debitis optio harum blanditiis officiis
        non quo.</p>
  </div>

  <!-- jQuery -->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/2.1.4/jquery.min.js"></script>
  <!-- Bootstrap JavaScript -->
  <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/js/bootstrap.min.js"></script>

  <!-- script tag for optional custom JS goes here -->

</body>

</html>
{% endhighlight %}


###style.css
{% highlight css %}
/* 
this demonstrates that you can still add 
your own custom CSS along with Bootstrap 
*/
body {
    padding-top: 40px;
}
{% endhighlight %}


##References &amp; Resources

- [The Bootstrap Site](http://getbootstrap.com/)
- [The jQuery Site](https://jquery.com/)
- [W3Schools Bootstrap Tutorial](http://www.w3schools.com/bootstrap/)




