---
layout: post
title:  "블로그 유랑기 그리고 Static CMS의 미래 with Jekyll"
date:   2013-12-09 15:25:45
categories: k
permalink: /blog-traveling
image : http://e.fastcompany.net/multisite_files/fastcompany/imagecache/1280/poster/2013/12/3023173-poster-p-1-this-guy-made-his-own-ibeacon-for-70.jpg
---

10살 초반 네이버 블로그를 썼다.

16 티스토리를 썼다.

17살 워드프레스를 썼다.

18살 구글 블로거, 텀블러, <a href="http://postach.io/">Postach.io</a> (에버노트 기반 블로깅 플랫폼), 지킬을 
쓰고 나중에는 블로그는 직접 만들어 썼다(PHP-MySQL 기반.).

내가 원하는 블로그의 기능은 크게 아래와 같았다.

**-블로그 포스트 고유주소가 커스터마이징 가능할것.**

티스토리 : entry가 붙는다던가, 숫자가 분는건 싫다.
텀블러 : 큰 아키텍처를 지탱하기위해 stackoverflow처럼 중간에 랜덤 숫자 넣는건 증오한다.

**-무료일것. 그리고 무료로 도메인 연결 가능할것.**

wordpress.com 도메인 연결 유료이다. 
wordpress가 궁극의 블로깅 툴이긴 한데, 블로그하려고 LAMP호스팅하는건 별로다.

**-www가 없이 사이트를 요청할경우 www있는 도메인으로 rewriting가능할것**

물론 반대도 가능해야된다. 
티스토리 : 강제 rewriting기능이 없고 상담사도 모른다.
워드프레스 : 유료만 가능하고 셀프호스팅으로는 본전도 못뽑는다.
텀블러 : wwww 컨트롤이 안된다. 티스토리랑 마찬가지

**-HTML UI의 코드 한줄까지 커스터마이징 가능할것.**

티스토리: 모바일은 제어 불가, 자체 문법 배우는데 비용이 소요되어서 탈락.
워드프레스 : 너무 어렵기때문에 기회비용이 크다.

정리해보자. 마이너인 Postach.io는 여백상 제외한다.(inspired by Fermat)

<style type="text/css">
.tftable {font-size:12px;color:#333333;width:100%;border-width: 1px;border-color: #729ea5;border-collapse: collapse;}
.tftable th {font-size:12px;background-color:#acc8cc;border-width: 1px;padding: 8px;border-style: solid;border-color: #729ea5;text-align:center;}
.tftable tr {background-color:#ffffff; text-align: center;}
.tftable td {font-size:12px;border-width: 1px;padding: 8px;border-style: solid;border-color: #729ea5;}
</style>

<table class="tftable" border="1">
<tr><th>Concept</th><th>Naver Blog</th><th>Tistory</th><th>Wordpress</th><th>Blogger</th><th>Tumblr</th><th>Custom</th><th>Jekyll</th></tr>
<tr><td>커스텀 링크</td><td>x</td><td>o</td><td>o</td><td>o</td><td>x</td><td>o</td><td>o</td></tr>
<tr><td>고유 주소</td><td>x</td><td>x</td><td>o</td><td>x</td><td>x</td><td>o</td><td>o</td></tr>
<tr><td>무료</td><td>o</td><td>o</td><td>o</td><td>o</td><td>o</td><td>x</td><td>o</td></tr>
<tr><td>도메인 연결 무료</td><td>o</td><td>o</td><td>x</td><td>o</td><td>o</td><td>o</td><td>o</td></tr>
<tr><td>WWW Rewrite 여부</td><td>x</td><td>x</td><td>x</td><td>o</td><td>x</td><td>o</td><td>o</td></tr>
<tr><td>UI 커스터마이징</td><td>x</td><td>x</td><td>x</td><td>x</td><td>o</td><td>o</td><td>o</td></tr>
</table>

참고사항
      - wordpress 는 rewrite 가 되나 도메인이 유료이므로 포기
      - 구글 블로거, 티스토리, 워드프레스의 UI는 커스터마이징 가능하나 시간 비용이 너무 크므로 포기

궁극적으로 느낀 결론은 개발자라면 Gitdub에서 호스팅되는 지킬을 쓰면 좋고 일반인은 티스토리를 쓰면 좋겠다는 지극히 
주관적인 결론이 나왔다.

**Jekyll이란?**

Jekyll은 <a href="http://github.com">Github</a>의 CEO인 <a href="http://tom.preston-werner.com">Tom Preston-Werner</a>가 만든 Static 블로그 엔진이다.
Static 블로그 엔진은 기존 워드프레스처럼 PHP라는 서버측 언어를 이용해 데이터베이스에서 데이터를 뽑아와 완성된 HTML페이지를 만드는것이 아니라, 새로운 변경사항이 생기면 블로그 엔진이 변경사항이 적용해서 정적인 HTML파일을 모두 
업데이트한다. 

블로그처럼 데이터의 Write보다 Read가 많을경우 참으로 유리한 방법이다. PHP와 MySQL에 캐시를 달아도 태생적으로 가벼운
HMTL 블로그를 따라올수 없다. 

**좋은점, 약한점 그리고 미래**

태생적인 장점은 속도지만 HMTL파일 그자체이기 때문에 포스트별 인기도 측정이라던가 방문자추 추적같은것을 '자체적'으로
할수 없다. 여기서 자체적이란 말은 <a href="http://www.google.com/analytics">Google Analytics</a>같은 트레킹도구와 
그것들이 제공하는 API를 이용해서 Jekyll이 어느 포스타가 인기있는지 <a href="http://developmentseed.org/blog/google-analytics-jekyll-plugin/">플러그인</a>을 통해 판단하게 할수 있기 때문이다.

최근 미국 정부사이트인 <a href-"http://www.healthcare.gov/">www.healthcare.gov</a>역시 Static 블로그 엔진으로 돌아가고 있다. 갠적으로 지구 환경과 불피요한 프로세싱의 낭비를 줄이기 위해서라도 이런 툴은 좋은것 같다. 이런 대규모 서비스의 시도 결과가 기대된다.

기회가 된다면 <a href="http://developmentseed.org/blog/google-analytics-jekyll-plugin/">Jekyll과 Google Analytics를 결합하는 방법</a>에 대해서도 다뤄보고싶다. 아쉬운점은 Github의 Jekyll은 Safe모드로 동작해서 플러그인 사용이 안되는것 같다 ㅜㅜ
