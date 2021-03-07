---
title: "[node.js]MySQL과 연동하기"
excerpt: "node.js에서 mysql과 연동 테스트"

categories:
  - Blog
tags: 
  - [Blog, nodejs, study, mysql, db, database]
toc: true
toc_sticky: true
date: 2021-03-08
last_modified_at: 2021-03-08

---

<br>

# 1. mysql 데이터베이스 생성
-----


나는 이미 예전에 프로젝트에서 만들어둔 mysql db로 테스트했다. 아마존 RDS 서비스를 통해 만들어 둔 것인데, 유튜브에 동빈나님 강좌보고 따라했다. 아래 참조! 설명 너무 친절하고 좋음.

{% include video id="G6O-u6FkjpY?t=80" provider="youtube" %}


<br>

# 2. nodejs에서 db연동 테스트
-----

1. 터미널에서 ```npm install mysql```

2. mysql.js에서 아래와 같이 작성

```javascript
var mysql      = require('mysql');
var connection = mysql.createConnection({
  host     : '아마존 RDS 콘솔창에서 확인',
  user     : 'ID',
  password : 'PWD',
  database : 'DB명'
});

connection.connect();

connection.query('SELECT * FROM 테이블명', function(err, results, fields) {
  if (err) {
    console.log(err);
  }
  console.log(results);
});

connection.end();
```
<br>

# 3. 결과 확인
------
1. 터미널에서 ```node mysql.js```


짠&#9996;

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/210308_img.png){: .align-center}



