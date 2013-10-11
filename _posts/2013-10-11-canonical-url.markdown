---
layout: post
title:  "캐노니컬 주소"
date:   2013-10-11 20:29:56
categories:
permalink: /canonical-url
---

캐노니컬 주소는 구글과 마이크로소프트에서 표준으로 밀고있는 SEO최적화를 위한 링크이다.

예를들어 ASP를 서버측 언어로 사용하고 있는 마이크로소프트의 홈페이지를 보면 미국지역기준으로 
아래 URL모두 같은 페이지를 가리키는것이다.

{% highlight php %}
microsoft.com
www.microsoft.com
www.microsoft.com/en-us/default.aspx
www.microsoft.com/en-us/DeFaUlT.AsPx
{% endhighlight %}

다만 301 redirect등을 통해서 non-www를 www로 변경하고, default.aspx를 주소에 보이게 할지 여부는 서버에 달려있다.
문제는 검색엔진은 이것들이 같은건지 다른건지 일일이 301 redirect를 타고 들어가서 알아야 한다는 것이다.

이러한 프로세싱의 낭비를 줄이고 사용자 요구에 맞는 단일 URL정의하기위해 캐노니컬 주소가 만들어졌다. 
캐노니컬 주소는 다음과 같이 정의할수 있다.

{% highlight php %}
<link href='http://www.example.com/index.html' rel='canonical'/>
{% endhighlight %}

만약 non-www 주소를 원한다면 다음과 같겠다.
{% highlight php %}
<link href='http://example.com/index.html' rel='canonical'/>
{% endhighlight %}

캐노니컬 주소를 통해 자신의 URL방식을 정의하므로써 프로세싱의 낭비를 막음과 더불어 SEO역시 향상 가능할것같다.

아래는 공식 소개 비디오.

<iframe width="560" height="315" src="//www.youtube.com/embed/Cm9onOGTgeM" frameborder="0" allowfullscreen></iframe>
