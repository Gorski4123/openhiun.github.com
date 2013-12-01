---
layout: post
title:  "SNS 만들기 그리고 Django 낙서장"
date:   2013-09-22 18:16:16
categories: k
---

1년전 고2여름에 나는 IT기술을 통해서 해결하고 싶은 문제를 발견하고 그 문제를 해결하기 위해서 소셜 네트워깅 서비스를 만들고 싶었다. 그때는 내가 만든 서비스가 런칭만하면 페이스북처럼 될것 같은, 그런 느낌으로 개발을 했다. 내가 제일 처음 택한 것은 워드프레스를 이용해서 SNS를 만드는 것이다. 쉬운데다가 [Social Experience Lab][sel]같은 선례도 있었기 때문이다. 그러나 PHP라는 언어와 블로깅 엔진인 워드프레스의 기술적인 한계 때문에(아직 경험해 보지는 않았지만) 항상 유리천장이 있는것 같은 느낌이 들었다. 

앱스토어가 4주년을 맞이한 작년 가을 무렵 나의 아이폰 앱스토어의 소셜 네트워킹 카테고리에는 복사한듯한 깔끔하고 스타트업적인 디지인을 가진 다양한 버티컬 또는 가끔씩 호리즌탈한 소셜 네트워킹 서비스가 넘쳐나고 있었다. 대체 그것들은 어떻게 대량생산된것 처럼 모두 다 잘 동작할까? 라는 의문이 들었다. 대체 이러한 서비스들은 어떤 기술로 만들어질까? (그때 내가 스택오버플로우를 알았고 영어 구글링을 했다면 10초만에 나올 답이었다;;) 너무 궁금하였다. 누구도 알려주지 않았고 알 수 있는 곳도 없었다. 그러던 중 [생활코딩 페이스북 그룹에 막연하게 질문을 올렸다.][codingeverybody] 그렇게 해서 알게된것이 WAS(Web Application Framework)였고 Django, Ruby on Rails, Flask가 그러한 것이었다.

WAS를 구글링을 해보니 대표적인 WAS인 Django를 이용한 핀터레스트와 인스타그램의 신화적인 - [엔지니어 4명이서 4000만명이 사용하는 서비스를 만든 인스타그램의 이야기][instagram]와, 1900년대 이후 인구 증가속도만큼 2년동안 기하급수적인 사용자수 증가를 이겨낸 [핀터레스트의 이야기][pinterest]를 접했다.<br /><br />
<center>
<세계인구증가율과 핀터레스트 검색빈도 그래프>
![세계인구 증가율](/images/population.png "세계인구 증가율")
<script type="text/javascript" src="//www.google.com/trends/embed.js?hl=en-US&q=pinterest&cmpt=q&content=1&cid=TIMESERIES_GRAPH_0&export=5&w=500&h=330"></script>
</center>
[인스타그램의  기술 블로그][instagram-tech]를 보면 그들이 오픈소스 소프트웨어를 어떻게 잘 활용해서 최소의 인력으로 서비스를 운영했는지 알수있다. 내가 하려는것과 그것에 기반이 되는기술이 개발되어있다는것이 신기했다. **이렇게 모든것이 나를 위해 준비되어 있는데, 하라고 손짓을 하는데 안 할 이유가 무었인가?** 그래서 Django를 사용해서 내가 구상하고 있었던 Springvil이란 서비스를 만들어 보기로 했다. 제목을 낙서장이라고 지은것은 아직 강좌할 실력이 안되어 그날 배운것을 정리하는 용도로 쓸 생각이기 때문이다.

마지막으로 유튜브에 Mike Hibbert라는 사람이 [Django강좌][mikehibbert]를 하는데, 영어가 들린다면 들어볼만하다. 낙서장도 그의 강좌를 토대로 만들어질것임을 밝힌다.<br /><br />

**0.시작**

모든 서비스의 기본은 무엇을까? 극도로 추상화시켜보자면 그것은 **데이터를 입출력하는 일**이라고 생각한다. 사용자가 입력한데이터를 저장하고 변경하고 삭제하는것이 프로그래밍에서 궁극적으로 파이썬 -> C -> 어셈블리어 -> 기계어 순으로 처리되는것처럼 기계어 수준의 매우 단순하지만 저그의 라바같은 무엇이든 할수있는 가장 작은 단위의 일 일것이다. 

Django(이하 장고)는 파이썬이라는 언어로 만들어진 Web Application Framework(WAS)이다. 빠르고 쉬운 웹개발이라는 표현으로 설명을 해서 웹개발용으로만 사용되는 줄 알았는데 카카오톡과 같은 대부분의 모바일앱도 JSON이라는 방식으로 웹을 통해 데이터를 주고 받으니 **모바일앱이든 웹서비스든 궁극적으로는 WAS를 통해 데이터 입출력, 즉 서비스가 이루어진다.**<br /><br />

**1.설치**

개발 과정은 우분투 12.04 LTS에서 진행한다. 리눅스 서버개발에는 같은 리눅스를 쓰는게 편하다. ㅋㅋ

우리는 파이썬 패키지와 모듈을 버전별로 독립적으로 실행하기 위해 `virtualenv`라는 관리툴을 사용할것이고 장고는 그 위해서 돌아갈 것이다.(이렇게 패키지와 모듈을 독립적으로 사용하는것을 샌드박스 모드라고 한다.) 그리고 파이썬 소프트웨어 재단에서 관리하는 공식 패키지 저장소인 PyPi(Python Package Index)에서 패키지 설치를 위해 `easy_install`을 사용할것이다. 

**1-1**<br />
`easy_install`은 `python-setuptools`의 패키지이므로 `python-setuptools`를 설치한다.
<pre>
sudo apt-get install python-setuptools
</pre><br />

**1-2**<br />
`python-setuptools`를 설치했다면 이제 `easy_install`를 사용해 `virtualenv`를 설치하자.

<pre>
sudo easy_install virtualenv
</pre><br />

**1-3**<br />
이제 `virtualenv`를 통해 샌드박스 폴더를 만들자.  `--no-site-package`옵션은 기존에 설치된 패키지가 샌드박스 폴더에 영향을 미치지 않게 만들기 위한 명령어이다. 한마디로 깨끗하게 시작한다는것이다.

<pre>
virtualenv --no-site-package django
</pre><br />
<pre>
The --no-site-packages flag is deprecated; it is now the default behavior.
New python executable in django/bin/python
Installing distribute...............done.
Installing pip...............done.
</pre><br />

**1-4**<br />
이제 `virtualenv`를 활성화시키자.

<pre>
source django/bin/activate
</pre><br />

**1-5**<br />
활성화 시킨다면 터미널이 `(django)user@computer`처럼 변하면서 당신이 `virtualenv`에 있다는것을 확신시켜준다. `virtualenv`에서 작업한다면 무조건 실행해야되는 커맨드이다.

`cd django`명령어를 통해 방금 만든 django폴더에 들어가면 `bin`, `include`, `lib`, `local`폴더가 있는데 여기다가 장고를 설치하자. 아래 명령어를 보면 `sudo`가 없다. 우리는 `virtualenv`안에서는 `root`이기때문에 `sudo`가 필요없는 것이다. 마지막으로 django를 설치할 차례이다.

<pre>
easy_install django
</pre><br />
<pre>
Downloading https://pypi.python.org/packages/source/D/Django/Django-1.5.4.tar.gz
…
…
…
Finished processing dependencies for django
</pre><br />

**1-6**<br />
`bin`폴더안을 보면 `django-admin.py`라는 파이썬 파일이 있는데 이 파일이 장고 프로젝트를 생성할수 있게 해준다. 아래 명령어를 실행해서 `django_test`라는 프로젝트를 만들자

<pre>
django-admin.py startproject django_test
</pre><br />

**1-7**<br />
`cd django_test`를 통해 폴더로 들어가면 프로젝트 폴더인 `django_test`와 `manage.py`라는 파일이 있다. `manage.py`는 말그대로 웹서버와 시스템 컨트롤에 사용되는 파이썬 스크립트이다. 그럼 이 파일을 이용해서 첫번째 장고 서버를 켜보자!

<pre>
python manage.py runserver
</pre><br /> 
<pre>
(django)openhiun@openhiun:~/Desktop/django/django_test$ python manage.py runserver
Validating models...

0 errors found
September 22, 2013 - 14:36:10
Django version 1.5.4, using settings 'django_test.settings'
Development server is running at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
</pre><br />
 `http://localhost:8000`으로 접속하면 결과를 확인할수 있을것이다. 이제 모든걸 다 마쳤다. `ctrl-c`를 통해 서버를 죽이고 아래 명령어를 통해 `virtualenv`에서 나가자.<br />
{% highlight php %}
deactivate
{% endhighlight %}

[sel]: http://www.socialexperiencelab.com
[codingeverybody]: https://www.facebook.com/groups/codingeverybody/permalink/576755052365035/
[instagram]:       http://charsyam.wordpress.com/2011/12/17/%EB%B0%9C-%EB%B2%88%EC%97%AD-%EC%88%98%EB%B0%B1%EB%8C%80%EC%9D%98-%EC%9E%A5%EB%B9%84%EC%99%80-%EC%88%98%EC%8B%AD%EA%B0%80%EC%A7%80%EC%9D%98-%EA%B8%B0%EC%88%A0-instagram%EC%9D%98-%ED%9E%98/
[pinterest]: http://blog.naver.com/parkjy76/30167859682
[instagram-tech]: http://instagram-engineering.tumblr.com/post/13649370142/what-powers-instagram-hundreds-of-instances-dozens-of
[mikehibbert]: http://www.youtube.com/channel/UCFW_fvwCoF44MGWk74U_rFg
