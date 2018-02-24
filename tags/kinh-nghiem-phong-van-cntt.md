---
layout: default
title: Kinh nghiệm phỏng vấn xin việc ngành công nghệ thông tin
excerpt: Hiện nay, nhu cầu việc làm ngành công nghệ thông tin rất cao, tuy nhiên các bạn ứng viên vẫn chưa biết cách để thuận lợi hơn trong quá trình phỏng vấn, xin chia sẻ các kinh nghiệm phỏng vấn xin việc trong ngành công nghệ thông tin rất hữu ích khi bạn đi xin việc làm.
permalink: /tags/kinh-nghiem-phong-van-xin-viec-cntt
---
<div id="index">
<div class="category_detail">
    <h1>{{page.title}}</h1>
    <p>{{page.excerpt}}</p>
</div>
{% for post in site.posts %}
{% if post.tags contains 'kinh-nghiem-phong-van-xin-viec-cntt' %}
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
