---
layout: post
title:  "Clien for Chrome"
categories: k
permalink: /clien-for-chrome
image: http://farm4.staticflickr.com/3714/11656957215_6d926afb6f_o.jpg
---

<script src="/js/expando.js"></script>

<script>
$(document).ready(function(){
  $("#hide").click(function(){
    $("p").hide();
  });
  $("#show").click(function(){
    $("p").show();
  });
});
</script>

<style type="text/css">
 .button {
  position: relative;
  display: inline-block;
  vertical-align: top;
  height: 36px;
  line-height: 35px;
  padding: 0 20px;
  font-size: 13px;
  color: white;
  text-align: center;
  text-decoration: none;
  text-shadow: 0 -1px rgba(0, 0, 0, 0.4);
  background-clip: padding-box;
  border: 1px solid;
  border-radius: 2px;
  cursor: pointer;
  -webkit-box-shadow: inset 0 1px rgba(255, 255, 255, 0.1), inset 0 0 0 1px rgba(255, 255, 255, 0.08), 0 1px 2px rgba(0, 0, 0, 0.25);
  box-shadow: inset 0 1px rgba(255, 255, 255, 0.1), inset 0 0 0 1px rgba(255, 255, 255, 0.08), 0 1px 2px rgba(0, 0, 0, 0.25);
}

.button:before {
  content: '';
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  pointer-events: none;
  background-image: -webkit-radial-gradient(center top, farthest-corner, rgba(255, 255, 255, 0.08), rgba(255, 255, 255, 0));
  background-image: -moz-radial-gradient(center top, farthest-corner, rgba(255, 255, 255, 0.08), rgba(255, 255, 255, 0));
  background-image: -o-radial-gradient(center top, farthest-corner, rgba(255, 255, 255, 0.08), rgba(255, 255, 255, 0));
  background-image: radial-gradient(center top, farthest-corner, rgba(255, 255, 255, 0.08), rgba(255, 255, 255, 0));
}

.button:hover:before {
  background-image: -webkit-radial-gradient(farthest-corner, rgba(255, 255, 255, 0.18), rgba(255, 255, 255, 0.03));
  background-image: -moz-radial-gradient(farthest-corner, rgba(255, 255, 255, 0.18), rgba(255, 255, 255, 0.03));
  background-image: -o-radial-gradient(farthest-corner, rgba(255, 255, 255, 0.18), rgba(255, 255, 255, 0.03));
  background-image: radial-gradient(farthest-corner, rgba(255, 255, 255, 0.18), rgba(255, 255, 255, 0.03));
}

.button:active {
  -webkit-box-shadow: inset 0 1px 2px rgba(0, 0, 0, 0.2);
  box-shadow: inset 0 1px 2px rgba(0, 0, 0, 0.2);
}

.button:active:before {
  content: none;
}


.button-darkblue {
  background: #3b5ca0;
  border-color: #2d477b #2d477b #263c68;
  background-image: -webkit-linear-gradient(top, #4369b6, #3b5ca0 66%, #365391);
  background-image: -moz-linear-gradient(top, #4369b6, #3b5ca0 66%, #365391);
  background-image: -o-linear-gradient(top, #4369b6, #3b5ca0 66%, #365391);
  background-image: linear-gradient(to bottom, #4369b6, #3b5ca0 66%, #365391);
}

.button-text a         { color: white !important; }
.button-text a:hover   { color: white !important; }
.button-text a:visited { color: white !important; }
.button-text a:visited:hover { color: white !important; }

.button-darkblue:active {
  background: #3b5ca0;
  border-color: #263c68 #2d477b #2d477b;
}

img {
position: relative;
z-index: 1;
}

img.expando{ /*sample CSS for expando images. Not required but recommended*/
border: none;
vertical-align: top; /*top aligns image, so mouse has less of a change of moving out of image while image is expanding*/
position: relative;
z-index: 2;
}

</style>

<img class="expando" src="http://farm6.staticflickr.com/5480/11655234213_cb4d539d9d_o.png" width="640">

<b>Clien for Chrome</b>

<b>클리앙을 간단히 크롬 익스텐션으로 볼수있는 프로그램입니다.</b>

아래와 같은 경우에 사용하시면 좋습니다.

- mega.co.nz에서 탈옥툴 다운받으면서 잠깐 클리앙을 확인하고 싶을때.
- 느린 웹페이지 로딩때문에 잠깐 클리앙을 확인하고 싶을때.
- 심심해서 잠깐 클리앙을 확인하고 싶을때.

많은 이용 부탁드립니다. 

돈이 없어서 구글 웹 스토어 등록은 못하고 있습니다($5 소요). 반응이 좋으면 시도해볼 예정입니다.

피드백은 댓글이나 이메일( openhiun@gmail.com )로 부탁드립니다.

<b>다운로드</b>

<center><div class="button-text"><a href="https://mega.co.nz/#!Yx8UmSSJ!XYsEvGjy4HcPWgqSQ0r3_wkvSTg77l97VvRdDX0uL78" class="button button-darkblue" target="blank">Download Clien for Chrome - 40KB</a></div></center>

<b>설치방법</b>

`.crx`확장자의 크롬 익스텐션 파일을 다운로드한뒤 <a href="chrome://extensions/">chrome://extensions/</a>에 가셔서 파일을 창으로 드래그 하시면 됩니다. (보안 정책 때문에 다운받은 파일을 그냥 누르면은 안되네요 ㅠㅠ)

<img class="expando" src="http://farm6.staticflickr.com/5538/11657036283_160a2b3e0f_o.png" width="640">

드래그 후에 아래와 같은 팝업에서 'Add'를 눌러주면 끝!입니다.

<img class="expando" src="http://farm8.staticflickr.com/7329/11657138114_f5af28744a_o.png" width="640">
