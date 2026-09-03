---
layout: home
title: "Home"
---

# 📚 My CSE Blog

Here are my latest posts organized by subject:

{% for category in site.categories %}
### 📁 {{ category[0] }}

{% for post in category[1] %}
📄 [{{ post.title }}]({{ post.relative_url }}) — *{{ post.date | date: "%B %d, %Y" }}*
{% endfor %}

---
{% endfor %}
