---
layout: video_list
title: Video trên kênh youtube của Lập Trình Cuộc Sống
permalink: /video.html
excerpt: Các video về lập trình, đời sống lập trình viên trên kênh youtube của Lập trình cuộc sống chấm com
videos:
  -
    title: Học lập trình nên tự học hay học ở trung tâm?
    id: sgkNOWEbLSw
  -
    title: Thiết kế website cá nhân trên photoshop
    id: 9RQkB365RwQ
  -
    title: Sinh viên IT ngày xưa như thế nào? Dùng máy tính mạnh không?
    id: ClsOD7jAsQ4
  -
    title: Cảm giác khi thử lập trình pascal, trở về tuổi thơ dữ dội sau 10 năm 
    id: 0UO9UKjVQ68
  -
    title: Troll zero9 - Lập trình viên nghĩ gì khi xem clip của zero9 
    id: xsI6r6zYTp0
  -
    title: Gặp bug thì làm gì? Lập trình viên chiến đấu với bọn tester như thế nào? 
    id: wFQ1h8RNcEs
  -
    title: Đi thực tập IT bị cho nghỉ việc và nói rằng không có thời gian đào tạo 
    id: Zo8pGBDi6SA
  -
    title: Python làm được gì? Có nên học ngôn ngữ lập trình Python không? 
    id: 278ig6WPjiI
  -
    title: Phỏng vấn php người ta thường hỏi những câu hỏi gì?
    id: oHPvmdny9QM
  -
    title: Khi đi làm php người ta dùng những công cụ gì? 
    id: fOFKwV7OW7U
  -
    title: Crush nhờ cài win thì phải làm gì? 
    id: AecrHFq_9BI
  -
    title: Nhờ cài win hộ, dân IT cảm thấy như thế nào? 
    id: zNCk6jctVW8
  -
    title: Mình đã học lập trình như thế nào?
    id: qvjWF0HWeWw
  -
    title: Tạo blog nhanh chóng miễn phí với github
    id: CpmE5RTpPwQ
  -
    title: Phỏng vấn xin việc IT như thế nào? 
    id: GaMExVaxHc8
  -
    title: Nghề lập trình - tiền hay đam mê
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



