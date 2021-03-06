---
layout: post
title:  "AWS EC2에서 PHP세션 오류 해결하기"
date:   2013-12-11 11:19:55
categories: k
permalink: /php-session-on-ec2
image: http://farm8.staticflickr.com/7321/11316776485_6bc26ed304_o.jpg
---

한달전 <a href="http://www.springvil.com">Springvil</a>의 회원가입을 AWS EC2상에서 구현하면서든 가장 큰 문제가 
PHP세션이 도통 작동이 안된다는 것이다. 윈도우 머신의 WAMP와 카페24의 Shared 웹호스팅에서도 잘 작동하는데 
이상하게 AWS에서만 작동이 안되었다.

결국 외국의 한 블로그에서 권한문제때문에 세션 저장을 PHP가 하지 못한다는 인사이트를 받고 AWS에 맞게 시도해봤더니 해결됬다.
물론 나중에 사이트가 커지면 웹서버나 애플리케이션서버 자체에서 세션을 저장하지는 않지만 MVP를 만드는 우리와 같은 스타트업 들에게는 
성능보다 작동하는 제품이 우선이기때문에 자체적인 세션저장 역시 중요한편이다.

아래 명령어로 PHP의 설정파일인 ``php.ini``를 찾고 vim으로 열어보자.

{% highlight php %}
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

{% highlight php %}
$ mkdir /sessions
$ sudo chmod 777 -R /sessions
{% endhighlight %}

그리고 아래 명령어를 통해 PHP를 재시작하자.

{% highlight php %}
$ service php-fpm restart
//for php-fpm on ubuntu or centos with nginx
$ service php5-fpm restart
//for php on apache
$ apachectl restart
{% endhighlight %}

단순히 AWS만 해당되는 사항이 아니라 모든 클라우드 호스팅 그리고 개인 컴퓨터에서도 적용할수 있는 방법이다. **만약 이유없이 
PHP세션 변수가 패싱이 안된다면 가장먼저 권한을 의심해보자!**

**한가지 참고사항**

한가지 걸리는것은 내가 ``php.ini``설정을 바꿀 당시 너무 흥분되 있어서 기존에 ``php.ini``에 적혀있던 디렉토리를 확인하지도 
않고 지워버렸다. 만약 새로운 폴더를 만드는것이 불편하다면 기존디렉토리를 복사한후 ``chmod -R 777 /your/directory``를 통해 PHP에게 세션을 
쓸수있도록 하는 방법도 있다. 사실 이방법이 맞는 방법이지만, 난 디렉토리를 지워버려서 위와같이 새폴더를 만드는 방법으로 하였다.

**PHP세션 작동여부 간단히 테스트하기**

항상 <a href="http://www.w3schools.com/">w3school</a>같은대서 테스트 스크립트를 받아서 세션이나 서비스의 동작를 배우곤 했다. 근데 어떤 오류가 1달동안 안고쳐지면 어떤것이 그것의 완벽한 정의인지 블로그이름 맞다나 Defining Definition( 정의를 정의하는 )을 하는 작업이 필요하다. 간단하고 Robust한 테스트코드를 작성해 보겠다.

심플 그 자체의 HTML폼이다. 세션테스트는 HTML폼으로 'name'이라는 이름을 가진 데이터를 POST전송한뒤 세션을 생성해서 제3의 페이지로 다시 'name'을 출력할 생각이다. 즉 **1.html - 2.php - 3.php** 순으로 진행되고 만약 ``1.html``에서 입력한 값이 ``3.php``에서 출력다면 세션이 작동한다는 의미이다.

html폼에서 데이터를 보낸다.

{% highlight html %}
<!--file name : 1.html-->
<form action="result.php" method="post" enctype="multipart/form-data" id="questionnaire">
<input type="text" name="name" id="name" />   
<input type="Submit" value="Submit">
</form>
{% endhighlight %}

php에서 데이터를 받고 세션을 생성한뒤 세션변수에 저장한다.

{% highlight html+php %}
<!--file name : 2.php-->
<?php session_start();?>
<html>           
    <body>                   
        <?php 
        $_SESSION['name']=$_POST['name'];
        echo  $_SESSION['name']; 
        ?> 
        <br><br>
        <a href="3.php">move to 3.php</a>  
    </body>           
</html> 
{% endhighlight %}

세션변수 'name'에 저장된 값을 가져와서 출력한다.

{% highlight html+php %}
<!--file name : 3.php-->
<?php session_start();
?>
<html>
    <body>
        Hi, I am still <?php echo $_SESSION['name'];?>
    </body>
</html>
{% endhighlight %}

*Header Picture by <a href="http://www.flickr.com/photos/90237600@N00/2087764869">Flickr</a> with <a href="http://creativecommons.org/licenses/by-sa/2.0/">CC BY-SA 2.0 License</a>*
