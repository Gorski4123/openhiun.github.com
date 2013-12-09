---
layout: post
title:  "워드프레스 홈페이지를 자신의 URL메인페이지로 변경하기"
date:   2012-12-07 01:10:45
categories: k
permalink: /set-wordpress-mainpage-without-subdirectory
---

처음에 워드프레스를 설치하시는 분들중 많이 하시는 질문이.
FTP의 ``WWW``폴더나 ``public_html`` 폴더안에 워드프레스를 설치후 워드프레스가 자신의 도메인의 메인 페이지가 아닌
``yourdomain.com/wp``, ``yourdomain.com/wordpress`` 에 위치해 있다는 것입니다.
이것은 다른플러그인과 겹침을 방지하는 절차로써 간단하게 통해 워드프레스를 자신의 메인페이지로 만들수 있습니다.
1.설정(settings) – 일반(general)에 들어간뒤 사이트 주소(site url)에서 ``/wp /wordpress`` 를지우고 ``yourdomain.com`` 형태로 만듭니다.
2.FileZilla와 같은 FTP로 접속해서 ``/wp`` 혹은 ``/wordpress`` 폴더안에있는 ``index.php``를 다운받고 지웁니다.
3.메모장으로 다운받은 ``index.php`` 를 열면

{% highlight php %} 
<?php
/**
* Front to the WordPress application. This file doesn’t do anything, but loads
* wp-blog-header.php which does and tells WordPress to load the theme.
*
* @package WordPress
*/
/**
* Tells WordPress to load the WordPress theme and output it.
*
* @var bool
*/
define(‘WP_USE_THEMES’, true);
/** Loads the WordPress Environment and Template */
require(‘./wp-blog-header.php’);
{% endhighlight %}

이렇게 되어있을텐데요.
맨 마지막줄
``require(‘./wp-blog-header.php’);``
이것을 아까 바꾼 폴더 이름인 /wp를 하나 추가하여
``require(‘./wp/wp-blog-header.php’);``
이렇게 바꿉니다.
(워드프레스 코어가 ``/wp``가 아닌 ``/wordpress``에 설치되어 있는경우  ``require(‘./wordpress/wp-blog-header.php’);`` 바꾸시면 됩니다.)
4.저장하시고 FTP프로그램으로 Root디렉토리 (www, public_html같은 최상위 디렉토리)
에 올립니다.
그뒤 자신의 홈페이지 yourdomain.com 으로 접속하시면 위드프레스가 딱! 나오는것 보실겁니다.
