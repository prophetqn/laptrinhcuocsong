---
layout: default
title: Nghề lập trình viên hiện nay
excerpt: Nghề lập trình viên hiện nay đang là một nghề khá hot mà các bạn trẻ muốn theo đuổi, nghề lập trình lương khá cao, tuy nhiên cần phải có nhiều đam mê để trở thành một lập trình viên thành công. 
permalink: /tags/nghe-lap-trinh-vien-hien-nay
---
<div id="index">
<div class="category_detail">
    <h1>{{page.title}}</h1>
    <p>{{page.excerpt}}</p>
</div>
{% for post in site.posts %}
{% if post.tags contains 'nghe-lap-trinh-vien-hien-nay' %}
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
