---
layout: post
title: HTML/CSS/JS - Intro Sessions
comments: true
publish: true
---

This post will include notes from intro sessions, as well as some resource links. Members will also be able to post their questions or comments.

###What is HTML?
- Hyper Text Mark-up Language
- currently the standard is at version 5
- gives the web page its underlying structure
  - which is to say, a web page is made up of elements (headings, paragraphs, links, forms, etc.) and these elements are defined using HTML
- the browser reads the HTML file and renders the elements on the screen as they are defined
- **structure**


###What is CSS?
- Cascading Style Sheets
- currently the standard is at version 3
- allows us to style the elements on the web page, e.g. size, colour, font etc.
- **style**


###What is Javascript?
- a programming language (unlike HTML and CSS)
- currently the standard is at version 5
- allows us to add interactivity to the web page, e.g.
  - when user clicks this button, show a message
  - when a form is submitted, check inputs
- also allows us to manipulate the HTML document structure (aka DOM)
  - i.e. dynamic (vs. static) web pages
- **interactivity**


###A bit more about HTML 
- generic tag syntax:
{% highlight html %}
<tagname attribute1="attribute1-value" attribute2="attribute2-value" ... > text </tagname>
{% endhighlight %}

Note:

  - angle brackets or chevrons
  - there is always a tagname
  - attributes, if any, vary according to tags
  - the text may consist of other tags, i.e. nested HTML
  - closing tags, if any, denoted by forward slash
    - some HTML elements do not have an explicit closing tag

- basic document structure:
{% highlight html %}
<!doctype html>
<html>

    <head>
    
        <title>My Web Page</title>
        
    </head>

    <body>

        <p>Some text on my web page</p>

    </body>

</html>
{% endhighlight %}

Note:

  - HTML is *not* case-sensitive; current convention is all lower-case
  - white space (blank lines, indentation) *not* required, but recommended for better readability


###A bit more about CSS
- basic selector syntax:
{% highlight css %}
selector {
    property: value;
    ...
}
{% endhighlight %}


####Some Resource Links
- [W3Schools HTML](http://www.w3schools.com/html/)
- [W3Schools CSS](http://www.w3schools.com/css/)
- [Mozilla HTML Introduction](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Introduction)