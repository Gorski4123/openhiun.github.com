---
layout: post
title:  "AWS EC2에서 PHP세션 오류 해결하기"
date:   2013-12-11 11:19:55
categories: k
permalink: /php-session-on-ec2
image: http://farm8.staticflickr.com/7321/11316776485_6bc26ed304_o.jpg
---

한달전 <a href="http://www.springvil.com">Springvil의 회원가입을 AWS EC2상에서 구현하면서든 가장큰 문제가 
PHP세션이 도통 작동이 안된다는 것이다. 윈도우 머신의 WAMP와 카페24의 Shared 웹호스팅에서도 잘 작동하는데 
이상하게 AWS에서만 작동이 안되었다.

결국 외국의 한 블로그에서 권한문제때문에 세션 저장을 PHP가 하지 못한다는 인사이트를 받고 AWS에 맞게 시도해봤더니 해결됬다.
물론 나중에 사이트가 커지면 웹서버나 애플리케이션서버 자체에서 세션을 저장하지는 않지만 MVP를 만드는 우리와 같은 스타트업 들에게는 
성능보다 작동하는 제품이 우선이기때문에 자체적인 세션저장도 해볼만 한편이다.

아래 명령어로 PHP의 설정파일인 ``php.ini``를 찾고 vim으로 열어보자

{% highlight bash %}
$ find / -name php.ini
/etc/php.ini
$ vim /etc/php.ini
{% endhighlight %}

아래와 같은 코드를 세션이 있는 section에서 찾아보자. vim으로는 ``/session.save_path`` 명령어를 내리면 된다. 대강 1277번째 줄에 있는듯 하다.

{% highlight ini %}
session.save_path = "/your/session/path"
{% endhighlight %}

만약 세션을 ``/session``이라는 폴더에 저장하고 싶다면 아래처럼 변경해주자

{% highlight ini %}
session.save_path = "/sessions"
{% endhighlight %}

그리고 아까 입력한 폴더를 실제 생성하고 777권한을 줘서 PHP가 세션정보를 wtite할수 있게 하자.

{% highlight bssh %}
$ mkdir /sessions
$ sudo chmod 777 -R /sessions
{% endhighlight %}

그리고 아래 명령어를 통해 PHP를 재시작하자.

Finally restart PHP-FPM for apply setting with following commends.
{% highlight bash %}
$ service php-fpm restart
//for php-fpm on ubuntu or centos with nginx
$ service php5-fpm restart
//for php on apache
$ apachectl restart
{% endhighlight %}

단순히 AWS만 해당되는 사항이 아니라 모든 클라우드 호스팅 그리고 개인 컴퓨터에서도 적용할수 있는 방법이다. **만약 이유없이 
PHP세션 변수가 패싱이 안된다면 가장먼저 권한을 의심해보자!**
1

**참고사항**
한가지 걸리는것은 내가 ``php.ini``설정을 바꿀 당시 너무 흥분되 있어서 기존에 ``php.ini``에 적혀있던 디렉토리를 확인하지도 
않고 지워버렸다. 만약 새로운 폴더를 만드는것이 불편하다면 기존디렉토리를 복사한후 ``chmod -R 777 /your/directory``를 통해 PHP에게 세션을 
쓸수있도록 하는 방법도 있다. 사실 이방법이 맞는 방법이지만, 난 디렉토리를 지워버려서 위와같이 새폴더를 만드는 방법으로 하였다.

*Header Picture by <a href="http://www.flickr.com/photos/90237600@N00/2087764869">Flickr</a> with <a href="http://creativecommons.org/licenses/by-sa/2.0/">CC BY-SA 2.0 License</a>*
