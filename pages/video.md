---
layout: post
title: Video trên kênh youtube của Lập Trình Cuộc Sống
permalink: /video.html
excerpt: Các video về lập trình, đời sống lập trình viên trên kênh youtube của Lập trình cuộc sống chấm com
videos:
  -
    title: Nghề lập trình: Tiền hay đam mê?
    id: bLC6yA73lFw
  -
    title: Ngôn ngữ lập trình nào dễ học nhất? Rèn luyện tư duy lập trình
    id: bJqNTFSnNa0
  -
    title: Làm product và làm outsource khác nhau như thế nào?
    id: pAMh5j53BXI
  -
    title: Sự khác nhau giữa lập trình viên miền Bắc và miền Nam
    id: N0K7ZONRs6w
  -
    title: Đang code mà buồn tè thì làm thế nào?
    id: 5lkDOd8PKHc
  -
    title: Lập trình viên và chuyện tình yêu, chia tay, buồn, cắm đầu vào code
    id: Nbu8tBtef3c
  -
    title: Live stream - backend hay frontend dễ kiếm việc làm hơn
    id: VvPv9kiB01A
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
  -
    title: Làm game html5 đơn giản
    id: kuwn8vkmqyM
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



