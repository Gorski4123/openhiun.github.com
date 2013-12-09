---
layout: post
title:  "아파치 웹서버 무조건 WWW 붙힌 URL 로 이동 시키기"
date:   2012-12-07 01:10:45
categories: k
permalink: /redirect-www-url-on-apache
---

난 php / apache 환경에서 워드프레스를 사용중인데, (당연한 말인가 ;;)
다양한 사이트를 개발하면서 나온 문제가 바로 ``WWW.`` 이다.
``WWW``는 서브도메인으로 취급되기도 하고 그냥 붙는것인데 생략되기도 해서
조금 애매하다.. 나같은 초보자가 헷갈리기 쉬운 ㅎㅎ
문제는 ``WWW.``의 유무에 따라 로그인이 풀린다는것인데.
해결방법은 ``WWW.`` 있거나 없는것으로 URL은 강제로 리다이렉션 해주면된다.
(= 접근 가능한 URL을 하나로 통일하면 된다.)
자신의 웹서버 폴더에 있는 ``.htaccess`` 를 연뒤

{% highlight apacheconf %}
RewriteEngine On
RewriteCond %{HTTP_HOST} ^example.com
RewriteRule (.*) http://www.example.com/$1 [R=301,L]
{% endhighlight %}

를 갖다 붙인다. 해석을 하자면 ``example.com`` 이란 접근 URL을 닥치고 ``www.example.com`` 이란 것으로 바꿔버린다. 라는 설정이다.
물론 ``RewriteCond`` 에 ``www.example.com``  을 ``RewriteRule``에 그냥 ``example.com`` 을 넣으면 반대 상황이 될것 같으니,
www의 호불호에따라 하나로 통일하기만 하면 될것이다.
아파치 웹서버에서는 OS상관없이 다 되는것 같다!
