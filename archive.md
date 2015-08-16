---
layout: page
title: Archive
---

{% for post in site.posts %}
{% if post.publish %}
  * {{ post.date | date_to_string }} &nbsp; [ {{ post.title }} ]({{ post.url }})
{% endif %}
{% endfor %}