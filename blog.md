---
title: "All Posts"
---

# Blog

{% for post in site.posts %}
<h3>
  <a href="{{ post.url }}">{{ post.title }}</a>
</h3>
{{ post.excerpt }}

**[Continue reading...]({{ post.url }})**

<small>Written {{ post.date | date: "%-d %B %Y" }}</small>

---
{% endfor %}
