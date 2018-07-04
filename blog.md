---
layout: blog
title: the blog
permalink: blog
---
<link href="//netdna.bootstrapcdn.com/font-awesome/4.0.3/css/font-awesome.css" rel="stylesheet">
{% for post in site.posts %}
<div class="post">
<h2 class="title"><a href="{{ post.url }}">{{ post.title }}</a></h2>
<span padding-top="-10px">tags [
  {% for tag in post.tags %}
    {% capture tag_name %}{{ tag }}{% endcapture %}
    <a href="/tag/{{ tag_name }}"><code class="highligher-rouge"><nobr>{{ tag_name }}</nobr></code>&nbsp;</a>
  {% endfor %}
]</span>

<div class="entry">
{{ post.content | strip_html | truncatewords: 100 }}
</div>
</div>
<br>
<br>
{% endfor %}

