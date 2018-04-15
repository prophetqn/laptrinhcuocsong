---
layout: default
title: Cách trở thành hacker mũ đen
excerpt: Dạy bạn làm hacker mũ đen đầy đủ các hướng dẫn dễ hiểu nhất. Các bài học đầu tiên cơ bản nhất để trở thành hacker mũ đen. Hacker mũ đen là những người thâm nhập vào các trang web, tấn công vào các hệ thống nhằm phục vụ lợi ích cá nhân như đánh cắp thông tin người dùng hay tài khoản ngân hàng.
permalink: /tags/cach-tro-thanh-hacker-mu-den
---
<div id="index">
<div class="category_detail">
    <h1>{{page.title}}</h1>
    <p>{{page.excerpt}}</p>
</div>
{% for post in site.posts %}
{% if post.tags contains 'hacking-co-ban' %}
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