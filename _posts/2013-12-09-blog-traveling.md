---
layout: post
title:  "블로그 유랑기 - 최종판"
date:   2013-12-09 15:25:45
categories: k
permalink: /blog-traveling
---

10살 초반 네이버 블로그를 썼다.
16 티스토리를 썼다.
17살 워드프레스를 썼다.
18살 구글 블로거, 텀블러, <a href="http://postach.io/">Postach.io</a> (에버노트 기반 블로깅 플랫폼), 지킬을 
쓰고 나중에는 블로그는 직접 만들어 썼다(PHP-MySQL 기반.).

내가 원하는 블로그의 기능은 크게 아래와 같았다.

**-블로그 포스트 고유주소가 커스터마이징 가능할것.**
(티스토리 : entry가 붙는다던가, 숫자가 분는건 싫다.
텀블러 : 큰 아키텍처를 지탱하기위해 stackoverflow처럼 중간에 랜덤 숫자 넣는건 증오한다.. )

**-무료일것. 그리고 무료로 도메인 연결 가능할것.**
(wordpress.com 도메인 연결 유료이다. wordpress가 궁극의 블로깅 툴이긴 한데, 블로그하려고 LAMP호스팅하는건 별로다.)

**-www가 없이 사이트를 요청할경우 www있는 도메인으로 rewriting가능할것**
(물론 반대도 가능해야된다. 
티스토리 : 강제 rewriting기능이 없고 상담사도 모른다.
워드프레스 : 유료만 가능하고 셀프호스팅으로는 본전도 못뽑는다.
텀블러 : wwww 컨트롤이 안된다. 티스토리랑 마찬가지)

**-HTML UI의 코드 한줄까지 커스터마이징 가능할것.**
(티스토리: 모바일은 제어 불가, 자체 문법 배우는데 비용이 소요되어서 탈락.
워드프레스 : 너무 어렵기때문에 기회비용이 크다.)

정리해보자. 마이너인 Postach.io와 CustomLAMP는 여백상 제외한다.(inspired by Permat)

<style type="text/css">
.tftable {font-size:12px;color:#333333;width:100%;border-width: 1px;border-color: #729ea5;border-collapse: collapse;}
.tftable th {font-size:12px;background-color:#acc8cc;border-width: 1px;padding: 8px;border-style: solid;border-color: #729ea5;text-align:left;}
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














한때 SNS가 많은 각광을 받았었다. 11년은 그 정점일것이다. 영화 소셜네트워크가 나오면서 페이스북과 트



궁극적으로 느낀 결론은 개발자라면 Gitdub에서 호스팅되는 지킬을 쓰면 좋고 일반인은 티스토리를 쓰면 좋겠다는 지극히 
주관적인 결론이 나왔다.
