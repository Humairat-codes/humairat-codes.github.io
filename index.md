---
layout: home
title: "Home"
---

# 📚 My CSE Blog

{% for category in site.categories %}
### 📁 {{ category[0] }}

{% for post in category[1] %}
📄 [{{ post.title }}]({{ post.url }}) — *{{ post.date | date: "%B %d, %Y" }}*
{% endfor %}

{% endfor %}
