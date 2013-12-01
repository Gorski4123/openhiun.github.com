---
layout: post
title:  "PHP로 SNS만들기"
date:   2013-12-02 02:01:30
categories: k
permalink: /social-network-with-php
---

<center>
<a href="http://www.flickr.com/photos/openhiun/11155396466" title="the-social-network-logo by openhiun, on Flickr"><img src="http://farm4.staticflickr.com/3800/11155396466_fde1efe54a.jpg" width="500" height="194" alt="the-social-network-logo"></a>
</center>

한때 SNS가 많은 각광을 받았었다. 11년은 그 정점일것이다. 영화 소셜네트워크가 나오면서 페이스북과 트위터가 많은 인기를 얻었으니..
요즘에는 그때만 못하지만 난 여전히 SNS에 많은 가치를 두고 있다. 그 이유는 사람과 사람을 연결하는것 그것이 가장 가치있고 또한 재미있고 흥분되는 일인것 같다.
그런점에서 형태는 개방적, 폐쇠적으로 공간은 온라인, 오프라인, 온오프라인으로 많이 바뀌겠지만, 앞으로도 우리의 원초적 본능인 다른사람과 만나고 싶고
소통하고 싶다느것. 그것을 채워주기 위해 오랫동안 남아있을 카테고리인것 같다.

현실적으로 우리가 흔히 접할수 있는 언어인 'PHP로 SNS만들기'로 구글링을 하면 워드프레스를 이용한 방법말고는 나오지 않는다.
이 글에서는 1년전의 나처럼 막연하게 SNS를 만들고 싶은 마음을 가지고 있는 뉴비들을 대상으로 기본적인 기능 구현에대해 적어보려 한다.

**1.인프라**
상용 서비스든 베타 서비스든 '서비스'라는걸 가동시키기 위해서 장비와 전력등이 필요하다. 가장 쉬운 방법은 호스팅을 이용하는 것인데
나는 막 개발해보고픈 PHP입문자라면 아마존 웹 서비스에 가입해서 Elastic Beanstalk(이하 eb)을 사용해 볼것을 권한다.
PHP로 개발을 처음 하는 사람은 윈도우에서는 WAMP나 APM_SETUP등을 사용해서 쉽게 애플리케이션 구동환경을 만들겠지만
상용서비스시에는 비용문제등으로 리눅스 서버를 사용해야 하는데 이 경우 PHP와 MySQL그리고 그것을 뒷받침해주는 기타 패키지등을
설치해야한다. 지금 미친듯이 실현하고 싶은 아이디어가 있다면 나중으로 미루어도 된다. eb는 PHP와 MySQL같은 공통 요소를 최적화시켜 설치해놓은 서버이다.
eb를 선택한다음 당신이 할것은 PHP를 이용한 애플리케이션 개발 뿐이다.

**2.데이터베이스**
프로그래밍 언어로는 PHP를 사용할 것인데, PHP는 eb에 기본 설치되어 있다. 상용서비스 뿐만 아니라 초기서비스에서도 중요한것은
바로 **분이 시스템**이다. 대부분의 스타트업 서비스는 웹서버 + 애플리케이션 서버 - DB서버로 구성되어 있다. 웹서버와 애플리케이션 서버는 분리 통합이
비교적 문제가 아니나, 우리가 셀프 호스팅 할때처럼 데이터베이스를 같은 서버에 둘필요는 없다. 리소스 낭비이기 때문에, 그래서 아마존 웹 서비스의 RDS를 사용하면 된다. 간단하게.

**2-1.MySQL vs NoSQL(mongodb, HBase, Cassandra and Hadoop + etc)**
제발 MySQL로 가주기 바란다. 이제 시작한 서비스는 99%의 불확실성에 쌓여있다. 메시징은 HBase, 데이터분석은 Hadoop이 특화된 데이터베이스라고 하나
일반적으로 빠르게 시작해서 니즈를 검증하려면 시작하려면 그냥 MySQL로 가는것이 좋다. 빠른 시도가 실패의 비용을 줄이고, 개발의 복잡성도 줄이기 때문에 나는 처음에는 닥치고 MySQL을 사용하라고 권하고 싶다.

**3회원가입**
간단한 과정을 설명하자면 
1. 사용자가 폼에서 입력한 이름, 성, 이메일, 비밀번호를 post방식으로 전송한다.
2. 처리하는 PHP스크립트에서 PHP의`isset`과 `!empty`함수를 사용해 post방식으로 전송된 값이 설정되 있는지, 비어있지 않은지 
검사한다. (이때는 다중 if if if를 사용해서 하나하나 값을 검사하면 될것 같다.)
3.값이 유효하다면 비밀번호를 bcrypt등으로 암호화해서 다른 정보화 같이 MySQL에 넣고 이메일을 가져와서 로그인을 시도한다.
4.로그인 방법은 이메일과 암호화된 비밀번호를 mysql에서 쿼리문으로 `SELECT`하고 `mysqli_num_query`로 이메일과 비밀번호가
매칭되는 값이 있는지 확인한다.
5.만약 1이 나온다면 `session_start();`함수를 통해 세션을 발급하고 `header`함수로 실제 퍼스널라이징된 SNS페이지로 이동시킨다.

(BTW나는 여기까지 파는대 2달 걸렸다.)

**4.피드 만들기**
항상 궁금했다. 어떻게 페이스북은 같은 피드를 아니, 거의 모든 서비스가 어떻게 UI와 피드를 만드는지. 답은 간단했다. 
우리가 프로그래밍 시간에 배운 `while`문을 PHP에서 MySQL에서 데이터를 가져올때 사용하는 `mysqli_fetch_array`와 함께 사용해서 **일치하는 열의 데터를 모두 가져온뒤, 한열씩 조건에 맞게 반복``while``하면 된다.** 이런식으로 블로그 글,
트위터와 페이스북 피드도 작동한다. 물론 추가되는 조건이나 알고리즘은 다르지만, 근본은 같다.

예를 들어보자. 나는 이름과 시간 그리고 텍스트가 있는 피드를 가져올것이다. 아래와 같은 PHP코드로 말이다.

{% highlight html %}
$feed_query = mysqli_query($conn, "SELECT * FROM blog ORDER BY time DESC");
  while($feed_array = mysqli_fetch_array($feed_query)) {
    $firstname = $feed_array['firstname'];
    $lastname = $feed_array['lastname'];
    $time = $feed_array['time'];
    $text = $feed_array['text'];
    echo <<<POST
    "<h3>" . $firstname . "&nbsp;" . $lastname . "</h3><br />"
    "<h5>" . $time . "</h5><br />"
    "<h4>" . $text . "</h4><br />"
    <hr>
POST;
  }
{% endhighlight %}

매우 간단하다. ``feed_query``변수로 쿼리문을 통해 데이터를 불러오고, ``mysqli_fetch_array``함수를 ``while``함수 안에 
넣어서 쿼리를 통해 가져온 모든 결과값을 반복해서 출력한다. ``mysqli_fetch_array``는 가져온 값을 배열에 넣는 함수인데 
아래처럼 각각 피드 내용의 변수를 만들어서 배열에 있는 데이터를 입력하고 ``echo <<<POST``와 ``POST;``사이에 넣어서 
출력한다. ``echo``는 PHP에서 HTML을 출력할수 있게 만들어 주는 내장함수이다.


그루폰과 핀터레스트가 워드프레스와 수제 pdf쿠폰, 핀터레스트가 PHP기반으로 시작됬다는


참고로 나는 [Gravatar.com][gravatar]에서 이 블로그의 애플 아이콘을 호스팅하고 있는데, [URL을 통해서 사이즈별로 추출][asaph]할수도 있어서 참 편리하다.

[gravatar]: https://gravatar.com
[asaph]: http://asaph.org/gravatar/
