---
layout: post
title:  "티스토리 스킨 웹브라우져로 추출하는 방법"
date:   2013-02-13 21:57:45
categories: k
permalink: /export-tistory-skin-with-web-browser
---

<div class="txc-textbox" style="border: 1px solid rgb(159, 211, 49); background-color: rgb(231, 253, 181); padding: 10px;"><p><b>티스토리측에서&nbsp;스킨 버전및 배포를 관리하지 않고 개인들이 배포관리를 하고있어서 아쉬움이 들었다.</b></p><p>초야에 파묻힌 아름다운 스킨들을 사람들이 활용하지 못하고, 공개용 스킨인데도 불구하고 배포가 열려있지않아서 접근및 사용이 제한되는 경우를 봐왔다.<br></p><p><br></p><p>아래는 웹브라우져만으로&nbsp;티스토리 블로그의 스킨을 추출하는 방법이다.</p><p>(무료 스킨중&nbsp;배포중단등의 이유로 구할수 없을경우에만&nbsp;사용할것을 권한다. )</p></div>

1.나의 블로그에서 사용하고있는 화이트스킨을 추출해 보겠다.

<img src="http://cfile24.uf.tistory.com/image/18153638511B89922E1D7C" width="672">

2.블로그에 접속후 소스보기를 누른다.

<img src="http://cfile22.uf.tistory.com/image/235BA03A511B89CE05CCF5" width="672">

3.컨트롤 + F로 ``style.css``를 찾고 연다. ( 대부분 상단에 존재한다. )

<img src="http://cfile10.uf.tistory.com/image/01294437511B8A2623FDA0" width="672">

4.스킨 파일중 하나인 ``style.css`` ( 스타일시트 ) 를 볼수있다.
   컨트롤 + S 로 저장한다.

5.``style.css`` 주소를 보면 이 경우는 

{% highlight php %}
http://ts.daumcdn.net/custom/blog/92/920609/skin/style.css?_T_=1360689470
{% endhighlight %}

값이라는것을 알수있다. 그럼 skin.html 은 

{% highlight php %}
http://ts.daumcdn.net/custom/blog/92/920609/skin/skin.html
{% endhighlight %}

위의 주소임을 확인할수있다.

바로 들어가면 

<img src="http://cfile28.uf.tistory.com/image/17282434511B8B9A103538" width="672">

이런식으로 나온다. 역시 소스보기를 하면

<img src="http://cfile10.uf.tistory.com/image/201BFD35511B8BF1017F14" width="672">

이런식으로 나오는데 이것은 ``style.css`` 처럼 그냥 저장하지말고 전체선택후 메모장등 텍스트에디터로 저장하는것이 좋다. (그냥하면 깨진다.)
만약 스킨중 그림이 혹은 아이콘등이 있다면 이 화면에서 ``.png`` ``.jpg`` 로 검색하여 같이 추출할수 있다. 자바스크립트파일역시 추출가능하다.

6.마지막으로 ``index.xml`` 역시 같은 방법으로 저장한다.

<img src="http://cfile23.uf.tistory.com/image/181C7543511B8C8C31F1DA" width="672">


컨트롤 + S로 저장한다. 

7. Preview 이미지는 ``index.xml`` 을 지우고 ``/images/preview.png`` 등으로 들어가보면 있다.

8. 저장한 ``skin.html``, ``style.css``, ``index.xml``과 스킨별 이미지를 업로드후 이름을 정하고 저장한다. 블로그로 가서 에러가 날경우 ( 코드가 보인다든지.. ) HTML/CSS 수정에 들어가서 소스보기창에 나온 ``skin.html``을 전체선택해서 그대로 붙이면 해결된다.

<div class="txc-textbox" style="border: 1px solid rgb(243, 197, 52); background-color: rgb(254, 254, 184); padding: 10px;"><p>9. 이글은 쓸만한 무료스킨이 배포문제로 사라저가는것이 안타까워서 써보았다. 유료스킨과 저작물에는 사용하지 않기를 바란다.<br></p></div>
