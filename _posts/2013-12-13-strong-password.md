---
layout: post
title:  "강력한 비밀번호 만들기에대한 고찰"
date:   2013-12-13 08:51:55
categories: k
permalink: /strong-password
image: http://farm8.staticflickr.com/7321/11316776485_6bc26ed304_o.jpg
---

##비밀번호는 어떻게 저정될까?

강력한 비밀번호를 만들기에 앞서 우리가 설정한 비밀번호는 당최 어떻게 저장되는지 알아보자. 
대부분은 마이크로소프트 엑셀과 같은 표에 저장되는데, 
그것이 엑셀에서와 달리 수억줄로 확장될수있고 빠른속도로 PHP와 같은 서버측애플리케이션이 공개된 함수를 사용해서 읽을수 있으면 
데이터베이스로 부른다. 구조는 엑셀과 비슷하다.

<center>
<img src="http://farm3.staticflickr.com/2868/11345626924_6f7a637540_o.png">
실제 데이터 베이스에 비밀번호가 저장된 모습
source <a href="http://webscripts.softpedia.com/scriptScreenshots/Mysql-Ajax-Table-Editor-Screenshots-45296.html">http://webscripts.softpedia.com/scriptScreenshots/Mysql-Ajax-Table-Editor-Screenshots-45296.html</a></center>


##비밀본호가 저장되는 과정

**사실 사용자가 입력한 ``Password``나 ``12345678``과 같은 비밀번호는 별로 중요하지 않다.** 그리고 애당초 저장되지도 않는다. 
거의 모든 서비스의 비밀번호는 ``MD5``나 ``bcrypt``와 같은 문자를 암호화 하는 알고리즘에 의해, 암호화(해싱이라고 한다.)되어 저장된다.

예를들어 비밀번호 ``password``를 md5로 해싱하면 아래와같은 값이 나온다. 

{% highlight php %}
password => 5f4dcc3b5aa765d61d8327deb882cf99
{% endhighlight %} 

회원정보 제대로 털어준 SK컴즈에서 권유하는 방식인 특수문자를 붙힌다면? 아래와 같다.

{% highlight php %}
!password => d9ce320e9607636e2dba50d23dc1704d
{% endhighlight %} 

{% highlight php %}
!#pass?word^.^ => ae0ceba47c33d0f5b3f444a0073da439
{% endhighlight %} 

``md5``를 포함단 거의 모른 암호화 알고리즘은 여러문자중 하나만 바뀌어도 암호화된 전체 값이 바뀌기때문에 안전하다. 
그리고 단방향성이기때문에 ``password`` 라는 문자를 해싱해서는 ``5f4dcc3b5aa765d61d8327deb882cf99`` 라는 문자를 얻을수 있지만 
``5f4dcc3b5aa765d61d8327deb882cf99``를 해싱하면 ``696d29e0940a4957748fe3fc9efd22a3``라는 완전히 새로운 값이 
나온다 역으로 해싱하는것은 불가능하다. 

그 이유는 각 문자가 가진 고유한 ASCII코드라는것을 이용하며 각 문자를 암호화하는것이 아닌 그 문자들의 ASCII코드의 물리적인 크기(bit)
를 해싱하기 때문이다. 예를 들자면 우리는 ``1 + 2 + 3``이 ``6``이라는것은 알지만 ``6``자체가 
아래의 값들중 어떤것으로 이우어진지는 모른다. 

{% highlight php %}
1 + 1 + 1 + 1 + 1 + 1
2 + 2 + 2
3 + 3
3 + 2 + 1
2 + 3 + 1
3 + 1 + 1 + 1
2 + 1 + 1 + 1 + 1 + 1
{% endhighlight %} 

왜냐하면 최종의 ``6``은 그냥 ``6이기 때문이다.`` 아래값들은 모두 다합치면 결과가 6인 값들이다. 그러면 여기서 또하나의 문제가 생기는데,
다른 비밀번호가 내것과 해싱된값이 일치할수도 있다는 것이다. 여기까지는 나도 잘 모른다 (아시는 분들은 댓글좀) 하지만 추측으로는 
워낙 물리적인 문자열의 크기가 크기때문에 중간에 일적한 패턴의 랜덤한 요소를 넣는 방식으로 해결하지 않을까 싶다.
