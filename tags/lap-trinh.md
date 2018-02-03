---
layout: default
title: Lập trình
permalink: /tags/lap-trinh
---
<div id="index">
<div class="category_detail">
    <h1>Lập trình</h1>
    <p>Các bài viết với thẻ "lập trình"</p>
</div>
{% for post in site.posts %}
{% if post.tags contains 'lap-trinh' %}
<article class="post" itemscope itemtype="http://schema.org/Article">
  <h1 itemprop="name"><a itemprop="url" href="{{ site.site_url }}{{ post.url }}" title="{{ post.title | xml_escape }}" >{{ post.title | xml_escape }}</a></h1>
  {% if post.thumbnail %}
  <a href="{{ post.url }}"><img itemprop="image" src="{{ site.site_url }}images/{{ post.thumbnail }}" alt="{{ post.title | xml_escape }}" class="post_thumbnail"></a>
  {% endif %}
  <div class="excerpt" itemprop="description">
    {{ post.excerpt }}
  </div>
  <div class="clear"></div>
</article>
{%endif%}
{% endfor %}
</div>
