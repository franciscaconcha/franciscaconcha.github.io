---
layout: blog
title: the blog
permalink: blog
---

{% for post in site.posts %}
{% if post.categories contains 'blog' %}
<div class="post">
<h3 class="title"><a href="{{ post.url }}">{{ post.title }}</a></h3>
<p class="meta">Date: {{ post.date | date: ' %d %B, %Y' }}</p>
<div class="entry">
{{ post.content | strip_html | truncatewords: 100 }}
</div>
</div>
<br>
{% endif %}
{% endfor %}
