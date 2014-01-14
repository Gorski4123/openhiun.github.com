---
layout: post
title:  "자바스크립트 뉴비의 NamerJS 개발기"
date:   2014-01-15 21:52:45
categories: k
permalink: /javascript
code-white: confirmed
image: http://farm8.staticflickr.com/7389/11947096744_8c429e1d40_o.jpg
---

**0. 문제**

살면서여러가지 서비스(springvil.com, vk-m.org, 1618vote.net 등등)을 개발봤지만 가장큰 문제는 **서비스의 이름**이었다. 서비스의 얼굴이자 철학의 깊음 담으면서도 가볍고 쉽게부를수 있는게 중요하기때문이다. 하지만 최근에 스타트업 네이밍에서 어려운점은 2가지가 있다.

- 대부분 도메인이 먹혀있어서 Apple과 같은 흔한 단어로는 사이트를 만들기 어렵다.

- 그럼 2가지 단어를 사용해야 되는데 괜찮은 조합은 이미 사용되고 있는것도 많다. (face+book, insta+gram 등등)

하지만 영어단어는 무수히 많기 때문에(라틴어 포함 ㅋ) 대부분의 스타트업들은 새로운 단어를 조합해서 만들어야 한다. 하지만 일일이 경우에 수에 대입해보면서 분노를 느꼈다. **왜 그런툴은 없는걸까??** 모든 서비스의 시작인 난 불편을 느꼈다. 그래 내가 만들어야겠다.

**1. 구상**

2가지 고려사항이 있다.

- 단어 사이를 띄어쓰기로 구분할것.(여러 단어 입력하는게 콤마도 귀찮다.)

- 비동기성(async)으로 바로 결과를 알수 있을것.

나는 OS와 웹브라우져를 제외한 네이티브 애플리케이션를 혐오하는 구글형(?!) 사람(참조 1)이기때문에 당연히 웹에서 돌아가는 툴을 만들려고 했고 단순툴을 만들기에는 Javascript(이하 자바스크립트)가 최고이자 유일한 대안이어서 선택하였다.

허나 컴퓨터 언어로 생각하지전에 사람의 기계어 나의 본능으로 생각해봤다. 단어 조합기는 a, b, c라는 단어로 aa, ab, ac, ba, bb, bc, ca, cb, cc라는 단어를 조합하는것이기때문에 기본적으로 아래와 같은 형태가 필요하다고 생각했다. 아래와 같아야 모든 경우의수를 뽑아낼수 있다. 

{% highlight python %}
#if input is 1 2 3
1     1
1     2
1     3

2     1
2     2
2     3

3     1
3     2
3     3
{% endhighlight %}

**2. 개발을 위한 개발**

웹개발을 2년남짓 해봤지만 자바스크립트는 CPP(Copy & Paste Programming)으로만 한터라 실력은 흠..이였다. 
그리고 내가 증오하는 비-해커적 인어인 자바의 스타일을 일부 물려받았다.예를 들어 HTM의 특정 DIV를 id로 선택할때 쓰이는 ``document.getElementbyId``는 비-해커적 언어의 상징? 이라 그리 좋아하진 않았다.

가장중요한것은 어떻게 하면 

{% highlight python %}
#if input is 1 2 3
1     1
1     2
1     3

2     1
2     2
2     3

3     1
3     2
3     3
{% endhighlight %}

와 같은 문자열을 출력할수 있냐는 것이다. 물론 입력이 3개만 들어오면 저대로 프레임을 만들고 인풋만 하주면 되지만 입력은 무한가지로 들어오고 출력역시 입력값의 제곱만큼 경우의 수가 나오기 때문에 스케일링이 가능한 방법을 찾아야했다.

**3. 진짜 개발**

-출력 알고리즘의 구현

바로 생각난것은 loop(이하 루프)이다. 어떤 값이나 피드가 무한히 나온다면 그것은 분형명루프를 사용한것이기 때문이다. 루프는 크게 2종류가 있다.

- for루프 - 괄호 안의 특정한 횟수만큼 루프안에 있는 코드를 반복한다. 대표적인 예로 자바스크립트의 for루프가 있다.

{% highlight javascript %}
for (var i=0; i<array.length; i++) {
// do some stuff
}
{% endhighlight %}

- while루프 - 특정작업이 끝날때까지 코드를 반복한다. 대표적인 예로 php에서 피드를 생성할때 MySQL에서 특정한 열만큼의 데이터를 불러와서 그 데이터가 소진될때까지 코드를 반복 실행해 반복적으로 피드등을 만들어 출력한다. 대표적인 예로 블로그의 인덱스 페이지나 페이스북의 뉴스피드가 있다.

{% highlight php %}
<?php
while ($feed_query_array = mysqli_fetch_array($feed_query_result)) {
$feed_user = $feed_query_array['UserId'];
$feed_group = $feed_query_array['GroupId'];
$feed_text = $feed_query_array['FeedText'];
$feed_photo = $feed_query_array['FeedPhoto'];
$feed_date = $feed_query_array['CreationDate'];

?>
{% endhighlight %}

그리고 이경우에는 for를 사용한 다중루프가 생각이 났다. 위의 숫자더미에서 111으로 시작되는 행을 a 123으로 시작되는 행을 b라고 해보자.

-a는 배열에 담긴 입력값의 총 길이를 잰후(`array.length`) 그 값을 순차적으로 1씩 증가시키면서(`i++`) 한번 증가시마다 값들을 3번 출력하면 되겠다!(다중 `for`문 - i)

-b는 a의 코드를 a안에 한번더 집어넣음으로써(이것이 b이다) a가 한번 루프를 돌때마다 b의 루프가 전체 실행이 되도록 하면 되겠다!

push를 사용해서 한번씩 루프를 돌때마다 값을 result에 저장하고 루프가 완료되면 innerHTML을 통해 result라는 HTML div에 삽입한다. 그리고 배열 데이터의 구분을 comma대신에 그냥 빈 스페이스로 변경한다.

결과적으로 나온 자바스크립트 코드는 다음과 같다.

{% highlight javascript %}
$(document).ready(function(){
$("textarea").keyup(function(){
var textarea = document.getElementsByTagName("textarea")[0].value;
var array = new Array();
array = textarea.split(" ");

//variable for store loop result
var result = [];

// loop for combinating text
for (var i=0; i<array.length; i++) {
for (var j=0; j<array.length; j++) {
result.push(array[i] + array[j] + "&nbsp;&nbsp;&nbsp;");
}
}

$("#result").hide().html(result).fadeIn('fast');
document.getElementById('result').innerHTML = result.join(" ");
});
});

{% endhighlight %}

- 비동기성 출력

서비스의 작동방식은 크게 동기성과 비동기성으로 나뉜다.

- 비동기성은 aSync라고도 불리며 a는 Asynchronous의 첫글자이다. 지메일이나 페이스북처럼 웹 페이지가 새로고침 없이 컨텐츠만 업데이트되는것을 비동기성 출력(웹에서는 Ajax(Asynchronous Javascript and XML) 라고 한다.)의 전형적인 예이다.

- 동기성은 사용자의 지시로 어떤 명령이 수행되면 그 동안 사용자의 웹 페이지는 새로코침이나 로딩중 상태에 머물러 있으며 처리가 끝난후 결과값은 새로고침된 페이지에 출력되는것을 말한다. (많은 사람들이 동기성 출력이 좋은것인줄 알고 있지만 사실 비동기성 출력이 더욱 진보되고 사용자를 위한 기술이다.)

단어 조합기에서도 비동기성출력이 적용되면 사용자가 새로운 단어를 하나더 입력하거나 지우면 즉시 그 사항이 적용되어 예전 조합값들이 없어지고 새로운 조합값들로 HTML의 div안의 컨텐츠가 재작성된다.

Ajax의 경우 데이터가 지속적으로 새로고침 되면서 웹 페이지가 궁극적으로 반응형으로 보이는것이다. 동영상이 수많은 사진을 빠른 속도로 보여주는것을 생각한다면 **비동기성이 빠르고 부분적인 동기성의 데이터로 진행**된다는것을 알면 이해가 편할듯 싶다.



-어떻게 하면 데이터의 변경 사항을 알수 있을까? onchange VS onkeyup

우리가 지금 비동기성의 장점을 나열하고 있는 이유는 단 하나, **사용자가 입력한 값의 변경사항을 알아내서 변경사항이 있을때마다 루프를 실행하기 위해서 이다.**

자바스크립트에서 사용자의 데이터 입력을 감지하는 방법은 여러가지가 있지만 크게 onchange와 onkeyup이 있다. 편의를 위해 여기서는 jQuery 프레임 워크의 같은 기능을 하는 함수인 change와 keyup을 사용하였다.

change라는 속성이 폼에 적용하면 **폼에 적힌 글이 변경되었을때** 자바스크립트를 실행하는것이다. 그리고 또 변경되면 또 실행한다.

keyup이라는 속성은 폼여부에 상관없이 키보드의 키가 눌러지면 자바스크립트 코드를 실행한다. 키보드가 눌러지면 또 실행한다.

어떤것을 선택해야 할까??

change에서는 폼 데이터가 변경되었다는 기준이 폼에 데이터를 쓰고 다른곳을 클릭했을때 change된것으로 보고있다. 그 말은 사용자가 폼에 데이터를 입력하는중 혹은 몇개만 입력한 상태에서는 그 변경사항이 적용된것을 볼수 없다는 이야기이다. 반면 keyup은 키보드키가 눌릴때마가 코드를 실행하기 때문에 완벽한 비동기성 앱을 만들수 있다. 

다시한번 코드를 살펴보면 모든 루프와 코드 자체가 textarea폼에서 카보드가 눌렸을때(keyup)실행되고 또 실행됨을 알 수있다.

{% highlight javascript %}
$(document).ready(function(){
$("textarea").keyup(function(){

// do some stuff

});
});

{% endhighlight %}

지금까지 자바스크립트 기반 단어 조합기인 namer에 대해서 간단히 제작과정을 적어봤다. 살면서 처음으로 해본 수학적 프로그래밍이었고 큰 인사이트를 밭은 코딩이였다. namer는 [openhiun.com/namer](http://www.openhiun.com/namer)에서 사용할수 있으며 [Github(http://github.com/openhiun/namer)에 소스코드가 공개되어 누구나 더 나은 새로운버전의 namer를 만들고 배포할수 있다.
