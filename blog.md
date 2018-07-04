---
layout: blog
title: the blog
permalink: blog
---

{% for post in site.posts %}
<div class="post">
<small>{{ post.date | date: "%d %B %Y" }}</small>
<h2 class="title"><a href="{{ post.url }}">{{ post.title }}</a></h2>
<span padding-top="-10px"><small>tags [</small>
  {% for tag in post.tags %}
    {% capture tag_name %}{{ tag }}{% endcapture %}
    <a href="/tag/{{ tag_name }}"><code class="highligher-rouge"><nobr>{{ tag_name }}</nobr></code>&nbsp;</a>
  {% endfor %}
<small>]</small></span>

<div class="entry">
{{ post.content | strip_html | truncatewords: 100 }}
</div>
</div>
<br>
<br>
{% endfor %}

