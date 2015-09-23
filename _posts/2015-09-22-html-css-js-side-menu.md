---
layout: post
title: "HTML/CSS/JS - A Toggled Side-menu"
comments: true
publish: true
---

A key part of any web page front-end is navigation, enabling the user to go from one section to another easily and intuitively.

This week we will talk about coding a toggled side-menu which, incidentally, should work nicely on any device, including smartphones and tablets.

Through this exercise we will revise:

- general HTML document structure
- CSS and JavaScript integration
- CSS rules targeting HTML elements by `class`/`id`
- JavaScript event listeners and event handling

New things we will cover include:

- HTML 
  - `nav`, `ul` and `li` elements
  - `a` (anchor) and `h1` elements
  - `viewport meta` tag

- CSS properties
  - `position`, `list-style-type`, `text-decoration`
  - `line-height`, `text-align` 
  - `hover` pseudo-class and `cursor`
  - `transition`

- JavaScript 
  - `querySelector` function 
  - `if` statement

The goal is to produce something like [this](http://mississaugacoding.2fh.co/sidemenu).


##Code

The complete code from this session is shown below. The same code has also been pushed to [our Github repository](https://github.com/MississaugaCoding/toggled-side-menu).

###index.html
{% highlight html %}
<!doctype html>
<html>
    <head>
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Toggled Side-menu</title>
        <link rel="stylesheet" href="./public/css/style.css" type="text/css" />
    </head>
    <body>
        <nav class="sidemenu">
            <ul>
                <li>
                    <a href="#home">Home</a>
                </li>
                <li>
                    <a href="#about">About</a>
                </li>
                <li>
                    <a href="#contact">Contact Us</a>
                </li>
            </ul>
            <div class="menutoggle">&gt;</div>
        </nav>
        
        <div class="content">
            <h1 id="home">Home</h1>
            <p class="text">
                This is our home pageLorem ipsum dolor sit amet, consectetur adipisicing elit. Unde ut quae recusandae enim debitis incidunt voluptatum nisi repellendus. Minus, maxime, voluptatum maiores adipisci fuga dignissimos eaque eveniet ex atque dolores eos voluptates aspernatur inventore officia cupiditate a quas quisquam velit?
            </p>
            <p class="text">
                Lorem ipsum dolor sit amet, consectetur adipisicing elit. Unde ut quae recusandae enim debitis incidunt voluptatum nisi repellendus. Minus, maxime, voluptatum maiores adipisci fuga dignissimos eaque eveniet ex atque dolores eos voluptates aspernatur inventore officia cupiditate a quas quisquam velit?
            </p>
            <p class="text">
                Lorem ipsum dolor sit amet, consectetur adipisicing elit. Unde ut quae recusandae enim debitis incidunt voluptatum nisi repellendus. Minus, maxime, voluptatum maiores adipisci fuga dignissimos eaque eveniet ex atque dolores eos voluptates aspernatur inventore officia cupiditate a quas quisquam velit?
            </p>
            
            <h1 id="about">About</h1>
            <p class="text">
                Some info about usLorem ipsum dolor sit amet, consectetur adipisicing elit. Unde ut quae recusandae enim debitis incidunt voluptatum nisi repellendus. Minus, maxime, voluptatum maiores adipisci fuga dignissimos eaque eveniet ex atque dolores eos voluptates aspernatur inventore officia cupiditate a quas quisquam velit?
            </p>
            <p class="text">
                Lorem ipsum dolor sit amet, consectetur adipisicing elit. Unde ut quae recusandae enim debitis incidunt voluptatum nisi repellendus. Minus, maxime, voluptatum maiores adipisci fuga dignissimos eaque eveniet ex atque dolores eos voluptates aspernatur inventore officia cupiditate a quas quisquam velit?
            </p>
            <p class="text">
                Lorem ipsum dolor sit amet, consectetur adipisicing elit. Unde ut quae recusandae enim debitis incidunt voluptatum nisi repellendus. Minus, maxime, voluptatum maiores adipisci fuga dignissimos eaque eveniet ex atque dolores eos voluptates aspernatur inventore officia cupiditate a quas quisquam velit?
            </p>
            
            <h1 id="contact">Contact Us</h1>
            <p class="text">
                Our contact detailsLorem ipsum dolor sit amet, consectetur adipisicing elit. Unde ut quae recusandae enim debitis incidunt voluptatum nisi repellendus. Minus, maxime, voluptatum maiores adipisci fuga dignissimos eaque eveniet ex atque dolores eos voluptates aspernatur inventore officia cupiditate a quas quisquam velit?
            </p>
            <p class="text">
                Lorem ipsum dolor sit amet, consectetur adipisicing elit. Unde ut quae recusandae enim debitis incidunt voluptatum nisi repellendus. Minus, maxime, voluptatum maiores adipisci fuga dignissimos eaque eveniet ex atque dolores eos voluptates aspernatur inventore officia cupiditate a quas quisquam velit?
            </p>
            <p class="text">
                Lorem ipsum dolor sit amet, consectetur adipisicing elit. Unde ut quae recusandae enim debitis incidunt voluptatum nisi repellendus. Minus, maxime, voluptatum maiores adipisci fuga dignissimos eaque eveniet ex atque dolores eos voluptates aspernatur inventore officia cupiditate a quas quisquam velit?
            </p>
        </div>
        
        <script type="text/javascript" src="./public/js/script.js"></script>
    </body>
</html>
{%endhighlight%}

###public/css/style.css
{% highlight css %}
body {
    font-family: Helvetica;
    font-size: 1.5em;
}

.sidemenu {
    position: fixed;
    top: 0px;
    left: 0px;
    max-width: 200px;
    width:100%;
    height:100%;
    background-color: cornflowerblue;
    margin-left: -200px;
    transition: margin-left 500ms ease-in-out;
}

.content {
    margin-left:250px;
}

.sidemenu ul {
    list-style-type: none;
}

.sidemenu ul li {
    padding: 5px 0px 5px 0px;
}

.sidemenu a {
    color:white;
    text-decoration:none;
}

.sidemenu a:hover {
    text-decoration: underline;
}

.menutoggle {
    color:white;
    background-color: cornflowerblue;
    position:absolute;
    top: 0;
    left: 200px;
    width:50px;
    height:50px;
    text-align:center;
    line-height:50px;
}

.menutoggle:hover {
    cursor: pointer;
}
{%endhighlight%}


###public/js/script.js
{% highlight javascript %}
var sidemenu = document.querySelector('.sidemenu');
var menutoggle = document.querySelector('.menutoggle');

menutoggle.addEventListener('click',toggleSideMenu);

function toggleSideMenu() {
    
    if ( sidemenu.style.marginLeft === '0px' ) {
        sidemenu.style.marginLeft = '-200px';
        menutoggle.innerHTML = '>';
    } else {
        sidemenu.style.marginLeft = '0px';
        menutoggle.innerHTML = '<';
    }
    
}
{%endhighlight%}


##References &amp; Resources

- [HTML nav Tag](http://www.w3schools.com/tags/tag_nav.asp)
- [HTML ul Tag](http://www.w3schools.com/tags/tag_ul.asp)
- [CSS position Property](https://css-tricks.com/absolute-relative-fixed-positioining-how-do-they-differ/)
- [CSS transition Property](http://www.w3schools.com/css/css3_transitions.asp)
- [JavaScript querySelector() Function](http://www.w3schools.com/jsref/met_document_queryselector.asp)
- [JavaScript if Statement](http://www.w3schools.com/js/js_if_else.asp)
- [Using viewport meta Tag](https://developer.mozilla.org/en/docs/Mozilla/Mobile/Viewport_meta_tag)
- [Responsive Web Design](http://www.w3schools.com/css/css_rwd_viewport.asp)

