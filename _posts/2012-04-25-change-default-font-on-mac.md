---
layout: post
title:  "MAC OS X에서 기본글꼴을 원하는 글꼴로 변경하기"
date:   2012-04-25 02:46:45
categories: k
permalink: /change-default-font-on-mac
---

아시다시피 맥의 기본폰트(애플고딕)은 가독성이 많이 떨어집니다.

때문에 애플고딕을 맑근고딕 나눔고딕으로 많이들 바꾸시죠..

파일 바꿔치기등 여러가지 방법이 있습나다만, 가장 확실한 방법은 

터미널을 사용해서 깔끔하게 파일만 교체하는 방법인듯 합니다. 

저도 이 방법으로 지금까지 잘 사용하고 있습니다.

터미널을 켜시고

{% highlight bash %} 
sudo vi -e -c ":%s/<string>AppleGothic/<string>맑은 고딕 Bold/g" -c ":wq" 
/System/Library/Frameworks/ApplicationServices.framework/Versions/A/Frameworks/
CoreText.framework/Versions/A/Resources/DefaultFontFallbacks.plist
{% endhighlight %}



요 명령어를 고대로 붙어 넣으시면 됩니다. 

물론 나눔고딕등 다른글꼴로 변경하고 싶으시면

<div class="txc-textbox" style="border-top-style: solid; border-right-style: solid; border-bottom-style: solid; border-left-style: solid; border-top-width: 1px; border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-top-color: rgb(121, 165, 228); border-right-color: rgb(121, 165, 228); border-bottom-color: rgb(121, 165, 228); border-left-color: rgb(121, 165, 228); background-color: rgb(219, 232, 251); padding-top: 10px; padding-right: 10px; padding-bottom: 10px; padding-left: 10px; "><p>sudo vi -e -c ":%s/&lt;string&gt;AppleGothic/&lt;string&gt;<span class="s1"><b>맑은 고딕 Bold</b></span>/g" -c ":wq"</p><p><br></p><p>이 줄에서 &nbsp;--------------------------------&lt;string&gt;붙이고 폰트이름 적으시고 붙여서/g"&nbsp;-c":wq"</p><p><br></p><p>맑은 고딕 Bold를 지우고 다른 글꼴 이름을 넣으시면 됩니다.</p><p><br></p><p>한글이든 영어이든 글꼴 이름은 상관없습니다만,&nbsp;</p><p><br></p><p>이름과 띄어쓰기를 정확하게 해주셔야 됩니다.</p></div>

아 참, 바꾸시려는 글꼴은 미리 설치해 놓으셔야 합니다.

시스템파일 변경이니 패스워드를 요구한다면 쳐줍시다.. 없다면 그냥 엔터 쳐도 안보입니다. 

보안때문에.. 그러니 안보여도 그냥 칩니다. 그리고 엔터..

터미널에서 완료된후 재부팅을하면.. 눈이 시원해질겁니다. ㅋ

개인적으로 "맑은 고딕 Bold"체를 추천합니다. 가독성이 정말 좋습니다.ㅋ 

되셨으면 밑에 한줄 적어주세요~
