---
---


{% for post in site.posts %}
<h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
{{ post.excerpt }}

<a href="{{ post.url }}">Read more...</a>

---
{% endfor %}
