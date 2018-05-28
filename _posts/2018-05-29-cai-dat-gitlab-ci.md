---
layout: post
title: Giải thích và hướng dẫn cài đặt Gitlab Continuous Deployment một cách dễ hiểu nhất
category: Chuyện lập trình
tags:
 - tu-hoc-linux
 - hoc-ubuntu
 - bi-quyet-hoc-lap-trinh
related_posts:
 - title: 
   link: http://laptrinhcuocsong.com/nhung-phan-mem-nen-cai-dat-tren-ubuntu.html
 - title: 
   link: http://laptrinhcuocsong.com/cai-dat-moi-truong-lap-trinh-web-tren-ubuntu-phan-1.html
 - title: 
   link: http://laptrinhcuocsong.com/thay-doi-che-do-io-schedule-de-tang-toc-ubuntu.html
 - title:
   link: http://laptrinhcuocsong.com/tai-sao-dan-lap-trinh-thuong-fa.html
---

Có lẽ bạn đã từng nghe ở đâu đó continuous integration (CI - tích hợp liên tục) và continuous deployment (DC - triển khai liên tục). Trong bài viết này mình sẽ cố gằng giải thích về CI, DC và hướng dẫn các bạn cài đặt CI, DC sử dụng Gitlab một cách dễ hiểu nhất.

## CI - Tích hợp liên tục là gì?

Nghe tên thôi là cũng gần gần hiểu rồi, nôm na nó là phương pháp phát triển phần mềm yêu cầu dev nộp code thường xuyên, nộp code hàng ngày. Code được "tích hợp" liên tục lên test server để sớm phát hiện ra lỗi.

## CD - Triển khai liên tục là gì?

Đồng hành cùng tích hợp liên tục, triển khai liên tục là thường xuyên release phiên bản mới lên môi trường test, việc này được diễn ra tự động. Ví dụ bình thường, để xuất bản website, bạn phải làm rất nhiều thứ, từ upload code lên server, chạy migrate dữ liệu, cấu hình file config các kiểu, rất tốn thời gian và dễ sai sót. Nội dung chính của bài viết này sẽ hướng dẫn bạn cài đặt làm sao để nó "tự động" được.

## Continuous Deployment với Gitlab CI - CD

Gitlab CI - CD là một tool tự động deploy ứng dụng, thật ra thì có rất nhiều tool tương tự (ví dụ Jenkins) nhưng tại công ty mình dùng gitlab nên mình chỉ viết về cái này thôi :))

Thêm cái hình sơ đồ cho nó nguy hiểm:

![gitlab](images/gitlab-ci-flow.png)

1. Đầu tiên, một thằng dev nào đó push code lên gitlab.

2. Khi code trên gitlab thay đổi, Gitlab sẽ gọi thằng Gitlab runner đã được cài sẵn trên server của mình.

3. Gitlab runner nghe thấy, nó sẽ làm tất cả các công việc còn lại, lấy code về, cài các packages, copy file, sửa file config... vân vân và vân vân, nó làm tất cả những gì chúng ta chỉ định cho nó.

Đến đây thì có lẽ các bạn đã thấy sướng rồi, việc của dev chỉ là push code lên thôi, tất cả các việc còn lại là tự động.

## Cài đặt như thế nào?

## 1. Phần 1: Gitlab CI

Để gitlab hiểu được rằng repo của chúng ta có sử dụng tính năng tự động deploy, chúng ta cần tạo file .gitlab-ci.yml đặt ở thư mục gốc của project. Đây là file .gitlab-ci.yml đơn giản của mình:

```javascript
# For test server
deploy-test:
  before_script:
    ## this get from https://docs.gitlab.com/ee/ci/ssh_keys/
    ## Install ssh-agent if not already installed, it is required by Docker.
    ##
    - 'which ssh-agent || ( yum update -y && yum install openssh-client -y )'

    ## Run ssh-agent (inside the build environment)
    - eval $(ssh-agent -s)

    ## Add the SSH key stored in SSH_PRIVATE_KEY variable to the agent store
    - echo "$SSH_PRIVATE_KEY" | tr -d '\r' | ssh-add - > /dev/null

    ## Create the SSH directory and give it the right permissions
    - mkdir -p ~/.ssh
    - chmod 700 ~/.ssh

    ## User commands
    - whoami
    - cd /var/www/html/project_folder
  script:
    #rewrite all to maintain.html
    - sed -i 's/index.php/maintain.html/g' .htaccess
    - git reset --hard HEAD
    - git pull
    - cp app/install/.server_test_db.php app/config/database.php 
    - php index.php migrate
    # rewrite to index.php again
    - sed -i 's/maintain.html/index.php/g' .htaccess
  only:
    - test-server
```

Giải thích:

Chúng ta đã đặt một job tên là deploy-test
before_script: là đoạn script mặc đinh, nó sẽ chạy trước tiên, ở đây nó sẽ xác nhận private key (tí mình sẽ nói ở phần dưới), và cd vào thư mục dự án.
script: là tất cả những lệnh mà bạn muốn gitlab runner sẽ chạy, cụ thể ở ví dụ này, mình sửa file .htaccess để đưa website về chế độ bảo dưỡng, lấy code về, copy file cấu hình database vào đúng vị trí, chạy migrate dữ liệu và mở lại website. Tóm lại là bạn muốn nó làm gì thì cứ điền câu lệnh cần làm vào đây.
only: là nhánh bạn cần deploy, ở đây mình tạo luôn một nhánh tên là test-server trên gitlab rồi, cứ cái nhánh này có thay đổi code thì job sẽ chạy.

## Phần 2: Cài đặt gitlab runner:

Như giải thích ở hình trên, gitlab runner là một tool được cài trên server, chăm chú lắng nghe, khi nào được bảo làm gì thì làm đó.

Cách cài thì trên document của nó có rồi, nhưng theo kinh nghiệm của mình, bạn đừng cài bản 10, mà cài bản 9 như sau:

```javascript
curl -L https://packages.gitlab.com/install/repositories/runner/gitlab-ci-multi-runner/script.rpm.sh | sudo bash

sudo yum install gitlab-ci-multi-runner
```

Cài đặt xong, bây giờ phải kết nối thằng gitlab runner này với repo của mình, trước hết bạn lên gitlab, vào Settings - CI - DC mở phần Runners settings để lấy token

![gitlab](images/gitlab-runner-token.png)

Giờ thì bạn tạo runner mới bằng lệnh này:

```javascript
sudo gitlab-ci-multi-runner register
```

Quá trình tạo runner nó sẽ hỏi đủ các kiểu, cứ trả lời theo nó thôi, khi nó hỏi token thì paste token ở bước trước vào.

## Phần 3: Kết nối gitlab runner với repo của mình:

Để kết nối được chúng ta cần add key vào gitlab, để gitlab có thể gọi đến server của chúng ta. Bạn chạy `ssh-keygen` để tạo ssh key như bình thường, nếu có key rồi thì thôi.

Mở nó ra rồi copy nội dung private key:

```javascript
vi ~/.ssh/id_rsa
```

Quay trở lại gitlab, dán toàn bộ nội dung đã copy dán vào, tên variable key là `SSH_PRIVATE_KEY`

![gitlab](images/gitlab-ci-secret-variable.png)

Đến đây thì bạn đã hoàn thành cài đặt Gitlab CI - CD nếu có bất kỳ thắc mắc gì bạn có thể contact mình, viết dài quá :(

![gitlab](images/gitlab-ci-pipelines.png)

Chúc các bạn thành công
