---
---


{% for post in site.posts %}
<h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
<div><p>{{ post.excerpt | remove: '<p>' | remove: '</p>' }}<br /><a href="{{ post.url }}">Read more</a></p></div>
{% endfor %}
