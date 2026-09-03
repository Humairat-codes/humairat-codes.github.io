---
layout: home
title: "Home"
---

# Welcome to My CSE Blog!

Here are my latest posts organized by subject:

{% assign categories = site.categories %}
{% for category in categories %}
  ## {{ category[0] }}
  {% for post in category[1] %}
    * [{{ post.title }}]({{ post.url }}) - *{{ post.date | date: "%B %d, %Y" }}*
  {% endfor %}
{% endfor %}
