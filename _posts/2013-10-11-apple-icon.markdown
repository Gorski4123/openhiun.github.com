---
layout: post
title:  "애플 아이콘"
date:   2013-10-11 20:29:56
categories: k
permalink: /apple-icon
---

아이폰의 사파리에서 링크를 북마크하거나 홈화면 추가할경우 아이콘이 필요한데 최근 안드로이드까지 이러한 코드를 해석해서 북마크로 사용함으로써
웹 페이지의 아이콘 삽입은 모던웹사이트에는 필수적인 일이 되었다. 아이콘을 삽입하려면 아래의 코드처럼 애플에서 권장하는 다양한 해상도의 아이콘을 링크로 걸어주면 된다.

참고로 가장 마지막 아이콘의 크기는 57x57이다.

{% highlight html %}
<link rel="apple-touch-icon-precomposed" sizes="144x144" href="#">
<link rel="apple-touch-icon-precomposed" sizes="114x114" href="#">
<link rel="apple-touch-icon-precomposed" sizes="72x72" href="#">
<link rel="apple-touch-icon-precomposed" href="#">
{% endhighlight %}

또한 ``rel="apple-touch-icon-precomposed"``을 ``rel="apple-touch-icon"``으로 변경하면 애플 디바이스에서 아이콘의 기본 그라디언트가 적용된다.

참고로 나는 [Gravatar.com][gravatar]에서 이 블로그의 애플 아이콘을 호스팅하고 있는데, [URL을 통해서 사이즈별로 추출][asaph]할수도 있어서 참 편리하다.

[gravatar]: https://gravatar.com
[asaph]: http://asaph.org/gravatar/
