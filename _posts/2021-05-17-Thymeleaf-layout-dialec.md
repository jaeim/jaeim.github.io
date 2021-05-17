---
title: "[Spring-boot/Thymeleaf]thymeleaf-layout-dialect 라이브러리 사용법"
excerpt: "spring-boot에서 view 쉽게 구현하기"

categories:
  - Blog
tags: 
  - [Blog, Spring-boot, thymeleaf, spring, thymeleaf-layout-dialect]
toc: true
toc_sticky: true
date: 2021-05-17
last_modified_at: 2021-05-17

---

<br>

 __학교 게시판에 올린 글을 그대로 작성하는 거라 존댓말이다..^^__ 

 이 글은 아래 두 블로그를 참고하여 작성되었습니다.

 - <https://moonsiri.tistory.com/69>
 - <https://www.hanumoka.net/2020/05/21/springBoot-20200521-springboot-thymeleaf-layout-dialect/>
 

<br>

보통 웹페이지를 만들때 header, content, footer로 나누어 코드를 작성하고 대다수의 경우 header와 footer는 고정한 뒤 
content의 내용만 바뀌게 됩니다. 
(학교 스마트 클래스의 화면도 상단 학교 로고(header)와 하단의 footer는 그대로이고 그 안의 내용물만 바뀌는 것 처럼요.)

thymeleaf-layout-dialect 라이브러리는 타임리프에서 이러한 기능을 도와주는 역할을 합니다.


# 1. pom.xml에서  thymeleaf-layout-dialect 관련 디펜던시를 추가


(https://ultraq.github.io/thymeleaf-layout-dialect/getting-started/ <-- 해당 링크에서는 별도의 bean 설정도 필요하다고 나와있는데
제 프로젝트에서는 별도의 bean 설정시 오히려 오류가 나서.. 제가 잘 작동했던 방식으로 작성하겠습니다.)


```xml
<dependency>
   <groupId>nz.net.ultraq.thymeleaf</groupId>
   <artifactId>thymeleaf-layout-dialect</artifactId>
</dependency>
```

<br>

# 2. build.gradle -> dependencies에 아래 코드를 추가

```xml
implementation 'nz.net.ultraq.thymeleaf:thymeleaf-layout-dialect'
```

<br>

# 3. 스프링 부트 프로젝트의 src/main/resources/templates 아래 fragment 폴더와 layout를 생성

<br>

# 4. fragment폴더 아래 head.html과 footer.html을 생성

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/2021-05-17 21;25;26.PNG){: .align-center}

<br>

**<fragment/footer.html>**
```html
<!DOCTYPE html> 
<html xmlns:th="http://www.thymeleaf.org"> 
 <head th:fragment="headFragment"> 
 <!-- 공통 css, js 추가 -->
 <link rel="stylesheet" href="css/commons.css" />
 <script type="text/javascript" src="js/commons.js"></script> 
</head>
```

**<fragment/footer.html>**
```html
<!DOCTYPE html> 
<html xmlns:th="http://www.thymeleaf.org"> 
<footer th:fragment="footerFragment"> 
  this area is footer 
</footer>
```

<br>

# 5. layout폴더 아래 basic_layout.html을 생성

```html
<!DOCTYPE html> 
<html xmlns:th="http://www.thymeleaf.org" xmlns:layout="http://www.ultraq.net.nz/thymeleaf/layout"
  th:lang="ko"> 

<!-- [head] 영역 시작 --> 
<head> 
          <th:block th:insert="layout/head :: headFragment"></th:block> 
</head> 
<!-- [head] 영역 끝 --> 

<!-- [body] 영역 시작 --> 
<body>  

        <!-- [content] 영역 시작 --> 
        <div layout:fragment="custom-content"></div>
         <!-- [content] 영역 끝 --> 


         <!-- [footer] 영역 시작 --> 
         <footer th:replace="layout/footer :: footerFragment"></footer> 
         <!-- [footer] 영역 끝 --> 
</body> 
<!-- [body] 영역 끝 --> 
</html>
```
<br>

# 6. 위에서 만든 basic_layout.html을 적용할 content.html을 생성

```html
<!DOCTYPE html> <html xmlns:th="http://www.thymeleaf.org" 
xmlns:layout="http://www.ultraq.net.nz/thymeleaf/layout" 
layout:decorate="~{layout/basic_layout}">  
<!-- layout/basic_layout.html을 사용하겠다는 뜻 입니다. --> 
<head> 
<!-- 개별적으로 <head >에 추가하고 싶은 css, js 가 있다면 이 안에 넣어주면 됩니다. --> 
<!-- thymeleaf layout dialect가 content페이지의 head태그를 layout의 head태그에 자동으로 추가해준다. -->
       <title>content1</title>
       <link rel="stylesheet" href="css/content1.css" /> 
       <script type="text/javascript" src="js/content1.js"></script>
 </head> 




 <!-- 페이지의 실제 content 내용 -->
 <div layout:fragment="custom-content"> 
           이 부분을 원하는 대로 꾸며주면 됩니다. 
 </div> 
</html>
```

<br>

# 7. cotent.html 소스코드 확인

이제 controller를 통해 content.html을 실행하여 소스코드 보기를 눌러보면 head.html과 footer.html이 적용되어 아래와 같이 출력됩니다.

```html
<!DOCTYPE html> 
<html xmlns:th="http://www.thymeleaf.org" xmlns:layout="http://www.ultraq.net.nz/thymeleaf/layout" 
th:lang="ko"> 


<!-- [head] 영역 시작 --> 
<head> 
<!-- 공통 css, js 추가 --> 
    <link rel="stylesheet" href="css/commons.css" /> 
    <script type="text/javascript" src="js/commons.js"></script>
 <!-- 개별적으로 <head >에 추가하고 싶은 css, js 가 있다면 이 안에 넣어주면 됩니다. --> 
<!-- thymeleaf layout dialect가 content페이지의 head태그를 layout의 head태그에 자동으로 추가해준다. -->
    <title>content1</title> 
    <link rel="stylesheet" href="css/content1.css" />
    <script type="text/javascript" src="js/content1.js"></script> 
</head> 
<!-- [head] 영역 끝 -->


 <!-- [body] 영역 시작 --> 
<body>
     <!-- [content] 영역 시작 --> 
     <div> 이 부분을 원하는 대로 꾸며주면 됩니다. </div>
     <!-- [content] 영역 끝 --> 


     <!-- [footer] 영역 시작 --> 
     <footer> this area is footer </footer>
     <!-- [footer] 영역 끝 --> 
</body> 
<!-- [body] 영역 끝 --> 
</html>
```
<br>

위에 첨부한 블로그의 글을 제가 이해하기 쉬운 방식으로 편집하여 재작성하였습니다. 이해가 되셨으면 좋겠습니다.

 위에서 작성한대로 head.html이나 footer.html, 추가로 header.html 등을 원하는대로 작성하고, 이를 basic_layout.html에 넣어준 뒤
여러분이 원하시는 대로 바뀔 내용인 content.html을 웹페이지의 용도에 맞게 변경하여 사용하시면 될 것 같습니다.

thymeleaf-layout-dialect을 사용하면 새로운 웹페이지를 만들때마다 header나 footer, head를 일일히 다시 작성할 필요가 
전혀 없고, content 부분만 작성해주기만 하면 되는 것이 큰 장점인 것 같습니다.


