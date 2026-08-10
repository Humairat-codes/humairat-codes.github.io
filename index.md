---
layout: home
title: "Home"
---

# Welcome to My CSE Blog!

Here are my latest posts on core Computer Science topics:

{% for post in site.posts %}
* [{{ post.title }}]({{ post.url }}) - *{{ post.date | date: "%B %d, %Y" }}*
{% endfor %}
