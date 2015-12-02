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

In our first talk we explored the reasons why one would use these frameworks, and how to start using them. We then went ahead and built a web page menu example using Bootstrap classes. 

In our second talk, we looked at some jQuery methods, including event listeners and handlers.

Here is the Bootstrap code example we built and discussed during the first session.

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


And here is the jQuery code example we toyed around with during the second session.


###index.html
{% highlight html %}
<!doctype html>
<html>

<head>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>jQuery Example</title>
    
    <!-- Bootstrap CSS -->
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css" />
    
    <!-- Link for optional custom CSS goes here -->
    <link rel="stylesheet" href="./public/css/style.css" type="text/css" />
    
</head>

<body>

    <div class="container">
        <div class="page-header">
            <h1>jQuery</h1>
        </div>
        
        <p id="p1" class="mytext">
            Paragraph ONE Lorem ipsum dolor sit amet, consectetur adipisicing elit. Inventore, debitis, omnis, architecto eos voluptatem soluta laudantium provident repellendus excepturi nesciunt quia corporis delectus quaerat deserunt suscipit. Laudantium laborum asperiores repellat mollitia et a incidunt corporis minus rerum! Repellat, provident, ipsam similique magni ipsum eos quas praesentium enim dolorem ex reprehenderit rem id ad. Officiis, et, aspernatur dolor porro explicabo quibusdam dignissimos mollitia tenetur ipsa corporis quo sapiente debitis magnam cupiditate nisi nam id soluta. Animi, laborum, modi laudantium ea accusantium placeat incidunt tempore iusto aperiam vero vel cumque in est harum et possimus laboriosam quidem voluptatibus totam expedita recusandae architecto!
        </p>
        
        <p id="p2" class="mytext">
            Paragraph TWO Inventore, debitis, omnis, architecto eos voluptatem soluta laudantium provident repellendus excepturi nesciunt quia corporis delectus quaerat deserunt suscipit. Laudantium laborum asperiores repellat mollitia et a incidunt corporis minus rerum! Repellat, provident, ipsam similique magni ipsum eos quas praesentium enim dolorem ex reprehenderit rem id ad. Officiis, et, aspernatur dolor porro explicabo quibusdam dignissimos mollitia tenetur ipsa corporis quo sapiente debitis magnam cupiditate nisi nam id soluta. Animi, laborum, modi laudantium ea accusantium placeat incidunt tempore iusto aperiam vero vel cumque in est harum et possimus laboriosam quidem voluptatibus totam expedita recusandae architecto! Animi, laborum, modi laudantium ea accusantium placeat incidunt tempore iusto aperiam vero vel cumque in est harum et possimus laboriosam quidem voluptatibus totam expedita recusandae architecto! Lorem ipsum dolor sit amet, consectetur adipisicing elit. Sunt dicta voluptatibus consequuntur sed. Temporibus modi porro esse corporis accusantium. Ad, cumque alias distinctio aspernatur dolorem officiis expedita. Rem, temporibus, non voluptates fugiat blanditiis iste voluptatum odit enim laudantium molestiae cum voluptas tempora ea a dolorum ipsum repellendus architecto esse dignissimos.
        </p>
        
        <p id="p3"></p>
        
        <button id="btn1" class="btn btn-primary btn-lg">Toggle</button>
        
        <h3 class="sub-header">DOM Traversal</h3>
        <ul id="list">
            <li>One</li>
            <li>Two</li>
            <li>Three</li>
            <li>SubList
                <ul id="sublist">
                    <li>SubOne</li>
                    <li>SubTwo</li>
                    <li>SubThree</li>
                </ul>
            </li>
        </ul>

    </div>

    <!-- jQuery -->
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/2.1.4/jquery.min.js"></script>
    
    <!-- Bootstrap JavaScript -->
    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/js/bootstrap.min.js"></script>
    
    <!-- script tag for custom JS goes here -->
    <script type="text/javascript" src="./public/js/script.js"></script>
</body>

</html>
{% endhighlight %}


###script.js
{% highlight javascript %}
// note: all jQuery code needs to be wrapped inside a document ready function

$(document).ready(function(){
    
    /* note: syntax to call jQuery methods generally consists of:
    - dollar sign
    - selector in brackets (and quotes)
    - dot
    - jQuery method name (with arguments if any)
    */
    
    // select by tag name
    $('p').fadeOut(2000);
    
    // select by id
    $('#p1').fadeIn(2000);
    $('#p2').fadeIn(2000);
    
    // select by class
    $('.mytext').fadeOut(2000);
    
    
    // some other methods
    $('#p2').show();
    $('#p1').slideDown(2000);
    $('#p1').slideUp(2000);
    $('#p2').fadeToggle(2000);
    
    // method chaining
    $('#p1').slideToggle(1500).delay(1000).fadeToggle(1500);
    
    // event listening and handling
    $('#btn1').on('click', handleButtonClick );
    
    function handleButtonClick() {
    
        // add/modify inner html to an element    
        $('#p3').toggle().html('My third paragraph');
    
        // add/modify css of an element
        $('#p3').css({
            'color': 'red',
            'font-weight': 'bold'
        });
        
        // traverse to first item in sublist and add a css class
        $('#sublist li').first().addClass('orange');
        
        // traverse to second list item (count starts from zero)
        $('#list li:eq(1)').toggleClass('blue');
        
        // next / previous
        $('#list li').first().next().fadeToggle().fadeToggle();
        
        $('#list li').last().prev().html('THIS LIST ITEM HAS CHANGED TOO');
        
    }
    
});
{% endhighlight %}


###style.css
{% highlight css %}
.blue {
    color: blue;
    font-weight: bold;
}

.orange {
    color: orange;
    font-weight: bold;
    border: 1px solid black;
}
{% endhighlight %}


##References &amp; Resources

- [The Bootstrap Site](http://getbootstrap.com/)
- [The jQuery Site](https://jquery.com/)
- [W3Schools Bootstrap Tutorial](http://www.w3schools.com/bootstrap/)
- [W3Schools jQuery Tutorial](http://www.w3schools.com/jquery/)