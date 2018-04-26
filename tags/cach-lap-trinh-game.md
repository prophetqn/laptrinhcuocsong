---
layout: default
title: Cách lập trình game
excerpt: Nhiều bạn muốn học lập trình game, tuy nhiên vẫn chưa biết cách lập trình một game cụ thể như thế nào, đây là các bài viết hướng dẫn lập trình game bằng những kiến thức lập trình rất căn bản. Sử dụng kiến thức cơ bản như: vòng lặp game, chuyển động nhân vật trong game... rất có ích cho các bạn mới bắt đầu.
permalink: /tags/cach-lap-trinh-game
---
<div id="index">
<div class="category_detail">
    <h1>{{page.title}}</h1>
    <p>{{page.excerpt}}</p>
</div>
{% for post in site.posts %}
{% if post.tags contains 'cach-lap-trinh-game' %}
<article class="post" itemscope itemtype="http://schema.org/Article">
  <h1 itemprop="name"><a itemprop="url" href="{{ site.site_url }}{{ post.url }}" title="{{ post.title | xml_escape }}" >{{ post.title | xml_escape }}</a></h1>
  {% if post.thumbnail %}
  <a href="{{ post.url }}"><img itemprop="image" src="{{ site.site_url }}/images/{{ post.thumbnail }}" alt="{{ post.title | xml_escape }}" class="post_thumbnail"></a>
  {% else %}
  <a href="{{ post.url }}"><img itemprop="image" src="{{ site.site_url }}/images/thumbnail_default.png" alt="{{ post.title  | xml_escape }}" class="post_thumbnail"></a>
  {% endif %}
  <div class="excerpt" itemprop="description">
    {{ post.excerpt }}
  </div>
  <div class="clear"></div>
</article>
{%endif%}
{% endfor %}
</div>