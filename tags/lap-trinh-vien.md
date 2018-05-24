---
layout: default
title: Lập trình viên
excerpt: Nghề lập trình viên, một nghề tưởng rằng công việc rất nhẹ nhàng, văn phòng đẹp giờ giấc thoải mái, nhưng không ai biết rằng đằng sau đó là một công việc rất vất vả, nhưng đam mê vẫn ở trong những lập trình viên trẻ, mong muốn tạo ra những phần mềm tiện ích. Tổng hợp các bài viết về lập trình viên hay nhất, để chúng ta hiểu rõ hơn về họ.
permalink: /tags/lap-trinh-vien
---
<div id="index">
<div class="category_detail">
    <h1>{{page.title}}</h1>
    <p>{{page.excerpt}}</p>
</div>
{% for post in site.posts %}
{% if post.tags contains 'lap-trinh-vien' %}
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
