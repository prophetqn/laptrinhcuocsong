---
layout: post
title: Làm app android chỉ bằng html, css và javascript thuần, phần 1 - Viết code javascript
category: Chuyện lập trình
tags:
 - lap-trinh-javascript
related_post:
 - title: 
   link: http://laptrinhcuocsong.com/nhung-phan-mem-nen-cai-dat-tren-ubuntu.html
 - title: 
   link: http://laptrinhcuocsong.com/cai-dat-moi-truong-lap-trinh-web-tren-ubuntu-phan-1.html
 - title: 
   link: http://laptrinhcuocsong.com/thay-doi-che-do-io-schedule-de-tang-toc-ubuntu.html
 - title:
   link: http://laptrinhcuocsong.com/tai-sao-dan-lap-trinh-thuong-fa.html
related_videos:
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
---

Sê-ri này gồm 4 phần:

> Phần 1: Viết code javascript<br>
Phần 2: Mông má lại cho đẹp bằng css<br>
Phần 3: App signing và build thành apk
Phần 4: Đưa app lên Google Play

```javascript
var app = function(){
    this.ui       = new ui(this);
    this.network  = new network(this);
    this.data     = [];
    this.level    = 0;
    this.question = null;
    
    var self      = this;

    // Boot all first time load
    this.boot = function(){
        this.ui.setScene('welcome');
        this.ui.listenEvents();
        this.loadData();
    }

    // Load data from api
    this.loadData = function(){
        this.network.get(
            DATA_URL,
            function(data){
                self.data = data;
                self.ui.hide('loadingText');
                self.ui.show('startButton');
            },
            function(error){
                alert(error);
            }
        )
    }

    // Preload an image
    this.loadImage = function(){
        this.ui.show('imageLoading');
        this.network.loadImage(
            self.data[self.level].image,
            function(image){
                self.ui.hide('imageLoading');
                self.ui.showImage(image);
            }
        );
    }

    // Start new game
    this.start = function(){
        this.ui.setScene('image');
        this.loadImage();
    }

    // Pick a ramdom question then show it
    this.pickAndShowQuestion = function(){
        // Pick a random question
        var questions = this.data[this.level].questions;
        var random    = Math.round(Math.random() * (questions.length - 1));
        this.question = questions[random];

        // Show it
        this.ui.showQuestion(this.question);
        this.ui.setScene('question');
    }

    // Check for answer on button click
    this.checkAnswer = function(answer){
        if (answer == this.question.correct){
            this.nextLevel();
        }
        else {
            this.ui.setScene('gameOver');
        }
    }

    // Next level
    this.nextLevel = function(){
        if (this.level == this.data.length - 1){
            alert("Bạn đã chiến thắng");
            this.restart();
            return;
        }

        this.level++;
        this.ui.updateLevelNumber();
        this.ui.setScene('image');
        this.loadImage();
    }

    // Restart game
    this.restart = function(){
        this.level = 0;
        this.ui.updateLevelNumber();
        this.ui.setScene('welcome');
    }
    
}
```


```javascript
var network = function(app){

    // Get data, this function use very-basic ajax request
    this.get = function(url, successCallback, errorCallback){
        var request = new XMLHttpRequest();
        request.open('GET', url);
        request.onload = function() {
            if (request.status === 200) {
                successCallback(JSON.parse(request.responseText));
            }
            else {
                errorCallback(request.status);
            }
        };
        request.send();
    }

    // Preload an image
    this.loadImage = function(imageUrl, successCallback, errorCallback){
        var img = new Image();
        img.onload = function(){
            successCallback(img);
        }
        img.onerror = function(){
            errorCallback();
        }
        img.src = imageUrl;
    }
}
```

```javascript
var ui = function(app){

    this.app = app;

    var self = this;

    // Get HTML element by id
    this.getElement = function(elementId){
        return document.getElementById(elementId);
    }

    // Show an element
    this.show = function(elementId){
        this.getElement(elementId).style.display = 'block';
    }

    // Hide an element
    this.hide = function(elementId){
        this.getElement(elementId).style.display = 'none';
    }

    // Set current scene
    this.setScene = function(sceneName){
        // Get all elements have class .scene
        var elements = document.getElementsByClassName('scene');
        // Then hide them
        [].forEach.call( elements, function(element) {
            element.style.display = 'none';
        });
        // Then show element has id screenName
        this.show(sceneName);
    }

    // Show image
    this.showImage = function(image){
        this.getElement('imageWrapper').innerHTML = '';
        this.getElement('imageWrapper').appendChild(image);
    }

    // Update level number on top of the app
    this.updateLevelNumber = function(){
        this.getElement('level').innerHTML = this.app.level + 1;
    }

    // Show question text and 4 answer buttons
    this.showQuestion = function(question){
        this.getElement('questionText').innerHTML = question.question;
        this.getElement('answerButton0').innerHTML = question.answers[0];   
        this.getElement('answerButton1').innerHTML = question.answers[1];   
        this.getElement('answerButton2').innerHTML = question.answers[2];   
        this.getElement('answerButton3').innerHTML = question.answers[3];
    }

    // Listen click events
    this.listenEvents = function(){
        // Click start button
        this.getElement('startButton').addEventListener('click', function(){
            self.app.start();
        });

        // Click #image div
        this.getElement('image').addEventListener('click', function(){
            self.app.pickAndShowQuestion();
        });

        // Click restartGame button
        this.getElement('restartGame').addEventListener('click', function(){
            self.app.restart();
        });

        // Listen click event for 4 answer buttons
        this.getElement('answerButton0').addEventListener('click', function(){
            self.app.checkAnswer(0);
        });
        this.getElement('answerButton1').addEventListener('click', function(){
            self.app.checkAnswer(1);
        });
        this.getElement('answerButton2').addEventListener('click', function(){
            self.app.checkAnswer(2);
        });
        this.getElement('answerButton3').addEventListener('click', function(){
            self.app.checkAnswer(3);
        });
    }
}
```