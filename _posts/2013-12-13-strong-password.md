---
layout: post
title:  "강력한 비밀번호 만들기에 대한 고찰"
date:   2013-12-13 08:51:55
categories: k
permalink: /strong-password
image: http://farm6.staticflickr.com/5493/11346327516_76ed85abd0_o.jpg
---

**비밀번호는 어떻게 저정될까?**

비밀번호는 Digital Age의 분신과도 같은 존재이다. 최소한 내가 입력한 Critical한 비밀번호가 어떻게 인증되고 저장되는지 
아는것은 코딩 교육이 일반화되는것처럼 필수적인 일이라고 생각한다.

강력한 비밀번호를 만들기에 앞서 우리가 설정한 비밀번호는 당최 어떻게 저장되는지 알아보자. 
대부분은 마이크로소프트 엑셀과 같은 표에 저장되는데, 
그것이 엑셀에서와 달리 수억줄로 확장될수있고 빠른속도로 <a href="http://php.net/" target"blank">PHP</a>와 같은 프로그래밍 언어의 함수를 사용해서 읽고 쓸수 있으면 
데이터베이스로 부른다. 전체적인 구조는 엑셀과 비슷하다.

<center>
<img src="http://farm3.staticflickr.com/2868/11345626924_6f7a637540_o.png" width="671">
실제 데이터 베이스에 비밀번호가 저장된 모습

source <a href="http://webscripts.softpedia.com/scriptScreenshots/Mysql-Ajax-Table-Editor-Screenshots-45296.html" target="blank">http://webscripts.softpedia.com/scriptScreenshots/Mysql-Ajax-Table-Editor-Screenshots-45296.html</a></center>


**비밀본호가 저장되는 과정**

**사실 사용자가 입력한 '12345678'나 'mypassword'과 같은 비밀번호는 별로 중요하지 않다.** 그리고 애당초 저장되지도 않는다. 
거의 모든 서비스의 비밀번호는 <a href="http://en.wikipedia.org/wiki/MD5" target"blank">md5</a>나 <a href="http://en.wikipedia.org/wiki/Bcrypt" target="blank">bcrypt</a>와 같은 문자를 암호화 하는 알고리즘에 의해, 암호화(해싱이라고 한다.)되어 저장된다.

예를들어 비밀번호 ``password``를 md5로 해싱하면 아래와같은 값이 나온다. 

{% highlight php %}
5f4dcc3b5aa765d61d8327deb882cf99
{% endhighlight %} 

많은 서비스에서 권유하는 방식인 특수문자를 붙혀셔 ``!password``를 해싱한다면? 아래와 같다.

{% highlight php %}
d9ce320e9607636e2dba50d23dc1704d
{% endhighlight %} 

조금더 복잡하게 ``!#pass?word^.^``를 해싱해보면 아래와 같다.

{% highlight php %}
ae0ceba47c33d0f5b3f444a0073da439
{% endhighlight %} 

md5를 포함단 거의 모른 암호화 알고리즘은 여러문자중 하나만 바뀌어도 암호화된 전체 값이 바뀌기때문에 안전하다.

또한 단방향성이기때문에 ``password`` 라는 문자를 해싱해서는 ``5f4dcc3b5aa765d61d8327deb882cf99`` 라는 문자를 얻을 수 있지만 얻어진 값을 다시한번를 해싱하면 ``696d29e0940a4957748fe3fc9efd22a3``라는 완전히 새로운 값이 
나온다 역으로 해싱하는것은 거의 불가능하다. 

그 이유는 각 문자가 가진 고유한 ASCII코드라는것을 이용하며 각 문자를 암호화하는것이 아닌 그 문자들의 ASCII코드의 물리적인 크기(bit)
를 해싱하기 때문이다. 예를 들자면 우리는 1 + 2 + 3이 6이라는것은 알지만 6자체가 
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

**왜냐하면 최종의 6은 그냥 6이기 때문이다.** 위값들은 모두 다합치면 결과가 6인 값들이다. 그러면 여기서 또하나의 문제가 생기는데,
다른 비밀번호가 내것과 해싱된값이 일치할수도 있다는 것이다. 여기까지는 나도 잘 모른다 (아시는 분들은 댓글좀) 하지만 추측으로는 
워낙 물리적인 문자열의 크기가 크기때문에 중간에 일적한 패턴의 랜덤한 요소를 넣는 방식으로 해결하지 않을까 싶다.

**현실적으로 안전한 비밀전호 만들기 그리고 더 현실적인 팁**

위에서 알아본 내용으로 괜시리 기억하기 어렵께 특수문자 넣는것은 헛짓이라는것을 알았다. 예전에는 사람들이 위키하게 md5에서 해싱된 값들을 모아서 <a href="http://www.md5rainbow.com/" target="blank">레인보우 테이</a>블이라는것을 만드는것이 성행했고, 그곳에서 해싱된 값을 넣고 실제 문자와 대조하는것을 찾곤 하였다. **이 경우에는 특수문자를 넣지 않은 비밀번호가 문제가 될수 있으나** 요즘은 비트코인 마이닝에 흔히 쓰이는 ATI GPU의 막강한 힘을 빌려서 하기때문에 아래와 같은 방법을 추천한다.

만약 ``google.com``에서 로그인 한다면 ``goopassword``이나 ``password#goo``등을 사용한다.
``facebook``이라면? ``facepassword``나 ``password#face``등이 될수 있겠다.

하지만 더욱 중요한것은 듣보잡 워드프레스, XE사이트, 그리고 개인이 만든 사이트에 가입할때는 Facebook이나 Google과 같은
사이트와 완전히 다른 비밀번호를 사용하는것이 좋다. 작정하고 아이디 털려는 사람은 Facebook이나 Google의 데이터베이스를 노리기보다 당신이 가입한 듣보잡, HTTPS도 작동 안되는 사이트를 노릴것이다. 해생에 관한 것보다 사실 이것이 가장 현실적인 방법이다. **믿을수 있는 사이트와 듣보잡 사이트를 분리하는것.. 제일 중요하다.**

**개발자에게**

해싱 알고리즘으로 제발 bcrypt를 사용해 주기 바란다. md5의 가장큰 단점은 GPU를 사용한 md5해싱이 1초에 몇억번도 가능하다는 것이다. 그에 반해 becypr는 <a href="http://en.wikipedia.org/wiki/Blowfish_(cipher)" target="blank" target="blank">blowfish</a>라는 기술을 사용해서 의도적으로 패스워드 해싱하는 시간을 
늘렸다. 이것이 한번해싱할때 1초씩만 되어도 모든 경우의수를 다 커버할려면 몇십-볓백년이 걸리기 마련이다. **그러니 새롭게
서비스를 만들 스타트업이 있다면 bcrypt를 사용해서 비밀번호를 안전하게 암호화하자!**

**bcrpyt에 관한 좋은글**

<a href="http://codahale.com/how-to-safely-store-a-password/" target="blank">codehale님의 bcrypt를 세상에 공론화 시킨 글</a>

<a href="http://www.openhiun.com/2013/08/bcrypt.html" target="blank">내가 쓴 PHP를 이용한 bcrypt 암호화 예제 글</a>

<a href="https://github.com/openhiun/php/blob/master/r.php" target="blank">PHP기반에서 bcrypt 비밀번호 암호화 예제 코드 @ Github</a>

오류가 있으면 지적부탁한다.
