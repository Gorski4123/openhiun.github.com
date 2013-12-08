---
layout: post
title:  "워드프레스 홈페이지에서 어드민바 숨기기"
date:   2012-12-07 01:09:45
categories: k
permalink: /how-to-hide-adminbar-in-wordpress
---

기업용, 단체용 워드프레스 사이트는 정적인 페이지(Static Page)를 메인페이지로 사용는편이다.
그렇게 되면 맴버들에게나 방분자에게나 상단에 위치한 기본 워드프레스 어드민바는 거슬릴수밖에 없다.
그리고 어드민바는 사이트를 너무 개인 블로그틱하게 만들어 준다..
워드프레스를 기업용, 단체용 홈피로 사용하실 분들에게는 어드민바의 존재는 걸리는 사항이다.
다음의 코드를 테마함수파일 ``functions.php``에 붙이는것 하나로 깨끗하게 어드민바를 감출수있다.

{% highlight php %} 
<!--adminbar control-->
<?php
show_admin_bar( false ); ?>
{% endhighlight %}
 
개인적으로 최상단에 넣는것을 추천하며, 주석도 같이 넣어두는것이 좋다.
(나중에는 이 코드가 뭐하는 놈인가 헷갈린다;;)
봐서 아시겠지만 false 를 true 로 고치면 어드민바는 다시 나타난다.
