---
layout: blog
title: the blog
permalink: blog
---

{% for post in site.posts %}
<div class="post">
<h3 class="title"><a href="{{ post.url }}">{{ post.title }}</a></h3>
{% if post.tags %}
  {% comment %}
=======================
The purpose of this snippet is to list all the tags you have in your site.
=======================
{% endcomment %}
<small>tags:
{% for tag in post.tags %}
	<a href="#{{ tag | slugify }}"> {{ tag }} </a>
{% endfor %}
</small>
{% endif %}

<p class="view">by {{ post.author | default: site.author }}</p>

<div class="entry">
{{ post.content | strip_html | truncatewords: 100 }}
</div>
</div>
<br>
<br>
{% endfor %}

