---
layout: post
title:  "HTML에서 jQuery를 아용한 글접기"
date:   2014-01-05 21:52:45
categories: k
permalink: /jquery-text-toggle
---

많이 쓰이는 자바스크립트 기술중에 글 접기가 있다. 딱딱한 플레인 자바스크립트 대신에 jQuery를 이용해서 부드럽게 접을수 있다.

**데모**

<iframe width="100%" height="720" src="http://jsfiddle.net/openhiun/tB6S9/embedded/result,js,html,css/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

**코드**

{% highlight html %}
<!--한글주석은 증오하지만 어쩔수 없이..-->
<!--jQuery를 불러옵니다. jQuery는 간단한 코드로 심오한 자바스크립트 기능을 사용할수 있는 자바스크립트 라이브러리입니다.-->
<script="http://code.jquery.com/jquery-1.10.2.min.js">

<!--감출 내용은 content라는 CSS클래스에 들어갑니다. 감출내용이니까 기본적으로 CSS에서 표시하지 않도록 설정해줍니다.-->
<style>
.content {
    display: none;
}
</style>

<!--jQuery내용입니다. 'container라는 클래스를 click할 경우 바로 다음에 나오는 content라는 클래스를 slideToggle하라.'라는 내용입니다. 결국 CSS를 통해 content는 display할수 없지만 jQuery가 인위적으로 그 내용을 끄집어 내어서 글 접기가 가능해지는 겁니다.-->
<script>
$(".container").click(function() {
    $(this).find('.content').slideToggle();
});
</script>

<!--위에서 설명한것과 같은 HTML내용입니다. 한번 보시면 이해가 될겁니다.-->
<div class="container">
    <b>Toggle</b>    
<div class="content">
  Lorem ipsum dolor sit amet, consectetur adipiscing elit.Lorem ipsum dolor sit amet, consectetur adipiscing elit.Lorem ipsum dolor sit amet, consectetur adipiscing elit.Lorem ipsum dolor sit amet, consectetur adipiscing elit.  
</div></div>

<div class="container">
  <b>Toggle</b> 
<div class="content">
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur sit amet ipsum eget nulla dictum porttitor. Suspendisse in orci a leo adipiscing blandit sit amet in diam. Duis a nisi in nisl semper condimentum ac ut augue. Nam aliquet orci lectus. Donec venenatis orci nisl, ut venenatis sem pellentesque sit amet.
    <img src="https://www.google.com/images/srpr/logo11w.png" width="480"/>
</div></div>
{% endhighlight %}
