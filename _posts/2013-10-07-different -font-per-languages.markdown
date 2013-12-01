---
layout: post
title:  "CSS 한영폰트 다르게 설정"
date:   2013-10-07 20:45:36
categories: k
pygments: true
permalink: /css-different-font-per-languages
---
항상 웹개발을 하다보면 한글서체(Google Fonts API가 제공하는 나눔고딕 이외에는 전무하지만..)가 마음에 들면 영문이 병신같고, 영문이라면 당연히 그 반대인 경우가 많다. 뭐.. 당연히 영문서체들은 한글을 지원을 안할것이다. 이점을 이용해서 웹에서 한영서체를 다르게 설정하는방법을 포스팅 해볼까한다.

얼마전 [Paul Irish][paulirish]의 [웹폰트 적용에 관한 방탄코딩 포스트][bulletproof]를 읽고 문득 이것에대한 영감이 들었다. 이미 알려져있고 사용되는 방법일수도 있지만 왠지 구글링해도 나는 찾지못했다. 찾은것은 [05년도 CSS2 표준화시절의 잡답 하나][cssdesignkr]이다.

무튼 본론으로 들어가서. 내 블로그 [openhiun.com][openhiun]의 폰트는 한글서체 ‘나눔고딕’과 영문서체 ‘Open Sans’로 이루어져 있다. 알파벳을 보면 알겠지만 나눔고딕의 스무쓰한 알파벳이 아님을 알수있다.

다음과 같이 적용하면 한영별로 다른 서체를 적용할수있다.

{% highlight html %}
<!DOCTYPE HTML>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html;charset=utf-8">
<title>Fancy Fonts</title>
<style>
@import url(http://fonts.googleapis.com/earlyaccess/nanumgothic.css);
@import url(http://fonts.googleapis.com/css?family=Open+Sans);
.font {
  font-family: 'Open Sans', 'Nanum Gothic', sans-serif;
 }
</style>
</head>
<body>
<div class="font">
나눔고딕 Nanum Gothic<br />
오픈산스 Open Sans<br />
구글 Google<be />
네이버 Naver<be />
<br />
</div>
</body>
</html>
{% endhighlight %}

[paulirish]: http://www.paulirish.com/
[bulletproof]: http://www.paulirish.com/2009/bulletproof-font-face-implementation-syntax/‎
[cssdesignkr]: http://cssdesign.kr/forum/viewtopic.php?id=136
[openhiun]: http://www.openhiun.com



