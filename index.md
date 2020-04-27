---
permalink: /
title: Home
---

## Kia Ora!

<img alt="Nick Malcolm" height="192" src="/assets/images/nicks_face.jpg" style="padding-left: 20px;float: right;">

I'm Nick, an information security consultant, a public speaker, a trainer, a sometime software developer, and - most important of all - a dad and husband. [Read more about me...](/about)

This blog is updated now and again with talks I've given, thoughts I've had, and things I hope others can learn from.

---

## Latest Posts

{% for post in site.posts limit:3 %}
<h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
{{ post.excerpt }}

[Continue reading...]({{ post.url }})

---
{% endfor %}

Showing the latest 3 posts. **[Read older posts...](/blog)**

