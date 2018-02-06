---
layout: post
title: Video
permalink: /video.html
excerpt: Các video về lập trình, đời sống lập trình viên trên kênh youtube của Lập trình cuộc sống chấm com
videos:
  - 
    title: Một giờ trong đời của lập trình viên (speed 6x)
    id: jwuxH1BeNG0
  -
    title: Live stream hướng dẫn lập trình game hứng trứng
    id: reN5y17YzCI
  -
    title: Lập trình phần mềm paint trên web
    id: pDSxzvyJ6k8
  -
    title: Cùng làm menu bằng css3 và javascript thuần, không dùng thư viện
    id: xfcDMzcqdZ4
---
<div id="videos">
  {% for video in page.videos %}
  <div class="video">
    <a target="_blank" href="https://www.youtube.com/watch?v={{ video.id }}">
      <img src="https://img.youtube.com/vi/{{ video.id }}/0.jpg" alt="{{ video.title }}" />
    </a>
    <h3><a target="_blank" href="https://www.youtube.com/watch?v={{ video.id }}">{{ video.title }}</a></h3>
    <div class="clear"></div>
  </div>
  {% endfor %}
</div>



