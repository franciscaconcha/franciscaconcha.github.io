---
layout: blog
title: Word cluster
permalink: blog
---

{% for post in site.posts %}
<div class="post">
<small><font color="#78909c">{{ post.date | date: "%d %B %Y" }}</font></small>
<h2 class="title"><a href="{{ post.url }}"><font color="#C58882">{{ post.title }}</font></a></h2>
<span padding-top="-10px"><small><font color="#78909c"><i class="fa fa-fw fa-tags"></i> [</font></small>
{% for tag in post.tags %}
    {% capture tag_name %}{{ tag }}{% endcapture %}
    <a href="/tag/{{ tag_name }}"><small><nobr>{{ tag_name }}</nobr>&nbsp;</small></a>
  {% endfor %}
<small><font color="#78909c">]</font></small></span>

<div class="entry">
{{ post.content | strip_html | truncatewords: 100 }}
{% if post.excerpt != post.content %}
    <a href="{{ site.baseurl }}{{ post.url }}">Keep reading</a>
{% endif %}
</div>
</div>
{% include share-bar-small.html %}
<br>
<br>
{% endfor %}

