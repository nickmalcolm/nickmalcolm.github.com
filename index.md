---
permalink: /
title: Home
---

## Kia Ora!

<img alt="Nick Malcolm" height="192" src="/assets/images/nicks_face.jpg" style="padding-left: 20px;float: right;">

I'm Nick, an application security consultant, a public speaker, a trainer, a sometime software developer, and most importantly of all a dad and husband. [Read more about me...](/about)

This blog is updated now and again with talks I've given, thoughts I've had, and things I hope others can learn from.

---

## Latest Posts

{% for post in site.posts %}
<h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
<div><p>{{ post.excerpt | remove: '<p>' | remove: '</p>' }}<br />&nbsp;<br /><a href="{{ post.url }}">Read more...</a></p></div>

---
{% endfor %}

