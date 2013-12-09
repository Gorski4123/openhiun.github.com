---
layout: post
title:  "워드프레스 자신의 포스트명을 포스트의 고유주소로 사용하기"
date:   2012-12-07 01:10:45
categories: k
permalink: /using-post-name-as-a-permalink
---

자신이 블로깅을 하거나 일반 사이트를 워드프레스를 통해 제작, 운영한다면 고유주소는 선택이 아닌 필수다.
**참고로 고유주소는 영어로 Permalink  라고 한다.**
고유주소가 뭔가 하면 자신이 포스트를 쓰면 (뭐든 간에 웹페이지를 만들면) 워드프레스에선 기본으로 ``http://hiun.org/?p=123`` 이런꼴의 주소로 만들어진다.
숫자로 주소를 생성하는것은 알아보기 힘들뿐아니라 Google같은 검색엔진에서 이 주소에 어떤내용이 있는지 색인(indexing)하기도 어렵다 그러므로 ``http://hiun.org/permalinks/``
같이 포스트의 내용을 나타낼수 있는 주소로 변경하는것이 검색엔진최적화(SEO, Search Engine Optimization)와 컨텐츠관리측면에서 편리하다.
이것은 약간의 수동 설정이 필요하다.
**먼저 FTP로** ``.htaccess``**파일이 있는곳을 살핀다. 대부분의 경우** ``index.php``**파일과 같이있을것이다.**

##경우1. ``index.php``가  ``www``,  ``public_html``같은 최상위 디렉터리 바로 아래  있는경우

.메모장하나 열고 아래와 같은 코드를 복사해붙인다.

{% highlight apacheconf %}
RewriteEngine On
RewriteBase /
RewriteRule ^index\.php$ – [L]
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . /index.php [L]
{% endhighlight %}

그리고 이것을 아무이름으로 저장한다음 FTP로 ``index.php``가 있는 디렉토리에 업로드 하고 이름을 ``.htaccess`` 로 변경한다.

##경우2. ``INDEX.PHP``가  ``/WP`` 혹은 ``/WORDPRESS`` 폴더 안에 있는경우

설치폴더명이 ``/wp`` 일 경우 아래의 코드를 복사해서,
{% highlight apacheconf %}
RewriteEngine On
RewriteBase /
RewriteRule ^index\.php$ – [L]
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . wp/index.php [L]
{% endhighlight %}

설치폴더명이 ``/wordpress`` 일 경우 아래의 코드를 복사해서

{% highlight apacheconf %}
RewriteEngine On
RewriteBase /
RewriteRule ^index\.php$ – [L]
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . wordpress/index.php [L]
{% endhighlight %}
메모장에 붙인후 아무 이름으로 저장하가고 FTP로 ``index.php``가 있는 폴더에 넣은다음
이름을 ``.htaccess`` 로 바꾸면 된다.
 
… 한뒤에 설정-고유주소로가서 고유주소를 글 제목으로 변경하면 된다.
 
ps. 워낙 헷갈리는 글이라.. 자세히 쓰다보니 많이 길어졌네요 ㅋㅋ
ps2. 방금 생성한 ``.htaccess``를 제외한 다른 ``.htaccess``파일이 존재한다면 삭제해 주셔야 정상적으로 고유주소가 작동합니다.
