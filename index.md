---
layout: default
title: Home
---

# ⚡ CSE CORE KNOWLEDGE BASE

{% assign categories = site.posts | map: 'categories' | flatten | uniq %}

{% for category in categories %}
  ## 📁 {{ category }}
  <ul>
    {% for post in site.posts %}
      {% if post.categories contains category %}
        <li>
          <a href="{{ post.url | relative_url }}"><strong>{{ post.title }}</strong></a> 
          <small>— {{ post.date | date: "%B %d, %Y" }}</small>
        </li>
      {% endif %}
    {% endfor %}
  </ul>
{% endfor %}
