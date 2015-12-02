---
layout: post
title: "HTML/CSS/JS - Bootstrap Carousel Example"
comments: true
publish: true
---

This week we picked another one of the several Bootstrap components - the image slider or carousel - and coded one from scratch.

For your reference and practice, here is the code we had built by the end of the session.

###index.html
{% highlight html %}
<!doctype html>
<html>

<head>
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <title>Bootstrap Carousel Example</title>

    <!-- Bootstrap CSS -->
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css" />

    <!-- Link for optional custom CSS goes here -->
    <link rel="stylesheet" href="style.css" type="text/css" />

</head>

<body>

    <div class="container">

        <div class="page-header">
            <h1>Bootstrap Carousel Example</h1>
        </div>

        <div id="mycarousel" class="carousel slide" data-ride="carousel" data-interval="1500">

            <ul class="carousel-indicators">
                <li data-target="#mycarousel" data-slide-to="0" class="active"></li>
                <li data-target="#mycarousel" data-slide-to="1"></li>
                <li data-target="#mycarousel" data-slide-to="2"></li>
                <li data-target="#mycarousel" data-slide-to="3"></li>
                <li data-target="#mycarousel" data-slide-to="4"></li>
            </ul>

            <div class="carousel-inner">
                <div class="item active">
                    <img src="images/image1.jpg" alt="">
                    <div class="carousel-caption">
                        <h2>Caption Heading</h2>
                        <p>Lorem ipsum dolor sit amet.</p>
                    </div>
                </div>
                <div class="item"><img src="images/image2.jpg" alt="">
                    <div class="carousel-caption">
                        <button class="btn btn-lg btn-primary">Learn More</button>
                    </div>
                </div>
                <div class="item"><img src="images/image3.jpg" alt=""></div>
                <div class="item"><img src="images/image4.jpg" alt=""></div>
                <div class="item"><img src="images/image5.jpg" alt=""></div>
            </div>

            <a href="#mycarousel" class="carousel-control left" data-slide="prev">
                <span class="glyphicon glyphicon-chevron-left"></span>
            </a>
            <a href="#mycarousel" class="carousel-control right" data-slide="next">
                <span class="glyphicon glyphicon-chevron-right"></span>
            </a>

        </div>

    </div>

    <!-- jQuery -->
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/2.1.4/jquery.min.js"></script>

    <!-- Bootstrap JavaScript -->
    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/js/bootstrap.min.js"></script>

    <!-- Custom JavaScript -->
    <script src="script.js"></script>

</body>

</html>
{% endhighlight %}



###style.css
{% highlight css %}
.carousel {
    height: 420px;
}

.item {
    height: 420px;
    background-color: lightgrey;
}

.item > img {
    margin: 0 auto;
    padding-top: 15px;
}

p {
    padding-bottom:5px;
}

.carousel-indicators li {
    background-color: black;
}

.carousel-indicators .active {
    background-color: cornflowerblue;
}
{% endhighlight %}


##References &amp; Resources

- [HTML Custom Attributes](https://developer.mozilla.org/en/docs/Web/Guide/HTML/Using_data_attributes)
- [A Good Article Explaining CSS Specificity](http://vanseodesign.com/css/css-specificity-inheritance-cascaade/)
- [CSS Selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors)
- [CSS Combinators](http://www.w3schools.com/css/css_combinators.asp)
- [The Bootstrap Site](http://getbootstrap.com/)
- [The jQuery Site](https://jquery.com/)
- [W3Schools Bootstrap Tutorial](http://www.w3schools.com/bootstrap/)
- [W3Schools jQuery Tutorial](http://www.w3schools.com/jquery/)




