---
layout: post
title: Apache trên centos không có quyền ghi file, dù đã chmod 777
excerpt: SELinux (Security-Enhanced Linux) dùng để khóa điều khiển truy cập vào các ứng dụng, tăng bảo mật, nhưng cũng có một vài điều gây khó chịu cho người sử dụng như việc gây chậm cho hệ thống hay khiến cho một vài ứng dụng trở nên khó cài đặt.
category: Linux - ubuntu
tags:
 - tu-hoc-linux
 - hoc-ubuntu
related_posts:
 - title: 
   link: https://laptrinhcuocsong.com/cai-dat-moi-truong-lap-trinh-web-tren-ubuntu-phan-1.html
 - title: 
   link: https://laptrinhcuocsong.com/cai-dat-moi-truong-lap-trinh-web-tren-ubuntu-phan-2.html
 - title: 
   link: https://laptrinhcuocsong.com/lap-trinh-tren-ubuntu-cac-phan-mem-web-developer-can-cai-dat.html
 - title:
   link: https://laptrinhcuocsong.com/thay-doi-che-do-io-schedule-de-tang-toc-ubuntu.html
related_videos:
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

---

Từ nay mình ghi chép trên trang này luôn, ghi chép linh tinh các vấn đề nhỏ nhỏ mà trong quá trình làm việc mình gặp phải, coi như cái sổ tay.

Khách hàng bên JAV báo hệ thống không ghi được file log. Zồi ôi, cái này thì đơn giản, gấp rút ssh vào server.

Ơ nhưng sao đã chmod 755 rồi vẫn không ghi được file nhỉ? Permission denied?
Chắc là thằng apache đang chạy trên user không được quyền ghi file ở thư mục đó. Thôi thì chown luôn sang cho nó.

`
$ chown -R apache:apache /var/www/mysite/logs
`

Vẫn không được, hừ, đã thế bố chmod 777 luôn:

`
$ chmod -R 777 /var/www/mysite/logs
`

Hí hửng check lại, wtf, vẫn không ghi được file? Cuối cùng mò mãi, thì ra nó đang bật SELinux
SELinux (Security-Enhanced Linux) dùng để khóa điều khiển truy cập vào các ứng dụng, tăng bảo mật, nhưng cũng có một vài điều gây khó chịu cho người sử dụng như việc gây chậm cho hệ thống hay khiến cho một vài ứng dụng trở nên khó cài đặt.

Cách giải quyết là: Tắt bố nó đi =))

Nghe có vẻ kém bảo mật, thiếu đạo đức nghề nghiệp tí nhưng không sao, fix cho chạy cái đã, bảo mật để bọn Nhật Bổn nó lo :D

`
 $ setenforce 0
`

Lệnh trên lập tức tắt luôn SELinux và mọi thứ hoạt động trơn tru, tuy nhiên nếu khởi động lại server thì nó lại tự bật lên như cũ.


Giờ thì tắt tịt nó luôn bằng cách mở file  `/etc/selinux/config`  và sửa  `SELINUX=enforcing` thành  `SELINUX=disabled`

`
$ vi /etc/selinux/config
`

Rồi sửa thành như thế này:

`
# This file controls the state of SELinux on the system.
# SELINUX= can take one of these three values:
#       enforcing - SELinux security policy is enforced.
#       permissive - SELinux prints warnings instead of enforcing.
#       disabled - SELinux is fully disabled.
SELINUX=disabled
# SELINUXTYPE= type of policy in use. Possible values are:
#       targeted - Only targeted network daemons are protected.
#       strict - Full SELinux protection.
SELINUXTYPE=targeted
`

Sau đó ra ngoài đi hút thuốc :))