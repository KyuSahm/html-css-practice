# HTML and CSS
## 실습 환경 준비
1) Visual Studio Code설치
2) Visual Studio Code의 좌측에 위치한 "확장(Extension)" 메뉴에서 Live Studio 설치

## HTTP 주요 요소
- URI
- HTTP Method (POST, GET, PUT, DELETE etc)
- Request Parameter
- Response Body
- Request Header
- Response Header
- Status Code

## REST API
#### CRUD
- HTTP method의 POST, GET, PUT, DELETE에 대응. 이것은 강제 사항은 아니고, 약속에 가깝다.
- https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol

#### Google REST API Guideline
- https://cloud.google.com/apis/design

#### 카카오톡 REST API 규격
- https://developers.kakao.com/docs/latest/ko/message/rest-api



## HTTP Request 구조

#### Start line
 - HTTP Method: GET, POST, DELETE, OPTIONS 등
 - Request Target: URI
 - HTTP Version
#### Request Header : key-value 쌍으로 구성
 - Host: host url on target
 - User-Agent: 요청을 보내는 클라이언트의 정보(예를들어, 웹브라우저 정보)
 - Accept: 해당 요청이 받을 수 있는 응답(response) 타입
 - Connection: 해당 요청이 끝난 후, 클라이언트와 서버가 계속해서 네트워크 커넥션을 유지할지 끊을지를 지시하는 부분
 - Content-Type: 해당 요청이 보내는 메시지 body의 타입. 예를 들어, JSON을 보내면, application/json
 - Content-Length: 메시지 body의 길이
#### Request Body
- 해당 request의 실제 메시지 내용.

- Body가 없는 request도 많다. 특히, Get Request들은 대부분 body가 없음

- start line

  ```html
  http -v http://localhost:8000/User/login name='tsedsas' password=123123123 
  POST /payment-sync HTTP/1.1
  ```

- Request Header

  ```html
  - Accept: application/json
    Accept-Encoding: gzip, deflate
    Connection: keep-alive
    Content-Length: 83
    Content-Type: application/json
    Host: intropython.com
    User-Agent: HTTPie/0.9.3
  ```

- Request Body
  ```html    
  {
    "imp_uid": "imp_1234567890",
    "merchant_uid": "order_id_8237352",
    "status": "paid"
  }
  ```



## HTTP Response 구조
#### Status line
 - Response의 상태를 간략하게 나타내주는 부분
 - HTTP Version
 - Status code: 응답 상태를 나타내는 코드. 숫자로 되어 있는 코드(예: 200)
 - Status Text: 응답 상태를 간략하게 설명해주는 부분(예: "Not Found")

#### Response Header
 - key-value 쌍으로 구성
 - Request Header와 비슷하지만, 약간 다름
 - 예를 들어, User-Agent 대신에 Server헤더가 사용
#### Response Body
 - 해당 response의 실제 메시지 내용
 - Body가 없는 response도 존재한다. 데이터를 전송할 필요가 없을 경우, body가 비어 있게 됨.
 - Status line
 ```html
 HTTP/1.1 404 Not Found
 ```

- Response Header
```html
Connection: close
Content-Length: 1573
Content-Type: text/html; charset=UTF-8
Date: Mon, 20 Aug 2018 07:59:05 GMT
```

- Response Body
```html
<!DOCTYPE html>
<html lang=en>
  <meta charset=utf-8>
  <meta name=viewport content="initial-scale=1, minimum-scale=1, width=device-width">
  <title>Error 404 (Not Found)!!1</title>
  <style>
    *{margin:0;padding:0}html,code{font:15px/22px arial,sans-serif}html{background:#fff;color:#222;padding:15px}body{margin:7% auto 0;max-width:390px;min-height:180px;padding:30px 0 15px}* > body{background:url(//www.google.com/images/errors/robot.png) 100% 5px no-repeat;padding-right:205px}p{margin:11px 0 22px;overflow:hidden}ins{color:#777;text-decoration:none}a img{border:0}@media screen and (max-width:772px){body{background:none;margin-top:0;max-width:none;padding-right:0}}#logo{background:url(//www.google.com/images/branding/googlelogo/1x/googlelogo_color_150x54dp.png) no-repeat;margin-left:-5px}@media only screen and (min-resolution:192dpi){#logo{background:url(//www.google.com/images/branding/googlelogo/2x/googlelogo_color_150x54dp.png) no-repeat 0% 0%/100% 100%;-moz-border-image:url(//www.google.com/images/branding/googlelogo/2x/googlelogo_color_150x54dp.png) 0}}@media only screen and (-webkit-min-device-pixel-ratio:2){#logo{background:url(//www.google.com/images/branding/googlelogo/2x/googlelogo_color_150x54dp.png) no-repeat;-webkit-background-size:100% 100%}}#logo{display:inline-block;height:54px;width:150px}
  </style>
  <a href=//www.google.com/><span id=logo aria-label=Google></span></a>
  <p><b>404.</b> <ins>That’s an error.</ins>
  <p>The requested URL <code>/payment-sync</code> was not found on this server.  <ins>That’s all we know.</ins>
</html>
```

#### HTTP Status Code
- 200 OK
  가장 자주 보게 되는 status code.
  문제없이 다 잘 실행 되었을때 보내는 코드.
- 301 Moved Permanently
  해당 URI가 다른 주소로 바뀌었을때 보내는 코드.
  ```html
  HTTP/1.1 301 Moved Permanently  
  Location: http://www.example.org/index.asp
  ```

- 400 Bad Request
  해당 요청이 잘못된 요청일때 보내는 코드.
  주로 요청에 포함된 input 값들이 잘못된 값들이 보내졌을때 사용되는 코드.
  예를 들어, 전화번호를 보내야 되는데 text가 보내졌을때 등등.
- 401 Unauthorized
  유저가 해당 요청을 진행 할려면 먼저 로그인을 하거나 회원 가입을 하거나 등등이 필요하다는것을 나타내려 할때 쓰이는 코드.
- 403 Forbidden
  유저가 해당 요청에 대한 권한이 없다는 뜻.
  예를 들어, 오직 과금을 한 유저만 볼 수 있는 데이터를 요청 했을때 등.
- 404 Not Found
  요청된 uri가 존재 하지 않는다는 뜻.
```html
http -v google.com/no-such-uri
  
GET /no-such-uri HTTP/1.1
Accept: */*
Accept-Encoding: gzip, deflate
Connection: keep-alive
Host: google.com
User-Agent: HTTPie/0.9.3

HTTP/1.1 404 Not Found
Content-Length: 1572
Content-Type: text/html; charset=UTF-8
Date: Mon, 20 Aug 2018 08:46:48 GMT
Referrer-Policy: no-referrer
```
- 500 Internal Server Error 
 서버에서 에러가 났을때 사용되는 코드.
  API 개발을 하는 백앤드 개발자들이 싫어하는 코드.

## 경로
- 경로 표시법
/     // 루트 디렉토리
./    // 현재 디렉토리
../    // 상위 디렉토리
../../  // 2번 상위 디렉토리

- 경로 지정방법: 절대경로 or 상대경로
- 루트 디렉토리를 이용한 절대경로
- 각 HTML별로 상대경로 지정 : 유리. 폴더 구조를 바꿀 때 수정할 사항이 적어진다.

## html 파일 생성
1) VS Code에서 "!"를 입력하고 엔터치면, 기본적인 html template를 입력해 준다.

## html tags
#### tags 분류
- 블록 스타일 Tags
  블록 태그의 크기는 자신이 감싸는 콘텐츠와 상관없이 자신의 영역을 가지고 있음.
  기본적으로 window의 width를 다 채우는 형태로 작동하고, 줄바꿈이 일어난다.
  ```html
  섹션: <section><nav><aside><article>
  블록: <div><header><main><footer>
  제목: <h/><hgroup/>..  // 위 아래 Margin이 조금 존재. 
  목록: <ul/><ol/><dl/>.. // 왼쪽에 어느 정도의 Margin이 존재.
  문장: <p/>
  표: <table/>
  입력폼: <form/>
  ```

- 인라인 Tags
  줄바꿈이 없음. 자신이 감싸는 콘텐츠의 크기가 자신의 크기가 됨.
  ```html
  하이퍼 텍스트: <a/>
  글자체 Bold: <b/>
  밑줄: <u/>
  폰트: <font/> => css로 대체 가능
  스타일 지정: <span> => css로 대체 가능
  굵은 텍스트: <strong> => css로 대체 가능
  한줄바꿈: <br> <!-- 사용자가 Enter키를 친것은 한줄에서 나옴 -->
  현재 사용가능한 인라인 Tags: css로 대체가능한 꾸미는 Tag들은 사라지고 있다.
  <a>, <abbr>, <acronym>, <audio>, <br>, <bdi>, <bdo>, <big>, <br>, <button>, <canvas>, <cite>, <code>, <data>, <datalist>, <del>, <dfn>, <em>, <embed>, <i>, <iframe>, <img>, <input>, <ins>, <kbd>, <label>, <nao>, <mark>, <meter>, <noscript>, <object>, <output>, <picture>, <progress>, <q>, <ruby>, <s>, <samp>, <script>, <select>, <slot>, <small>, <span>, <strong>, <sub>, <sup>, <svg>, <template>, <textarea>, <time>, <u>, <tt>, <var>, <video>, <wbr>
  ```
- 영역 나누기
  위의 것들에 해당되지 않는 경우처럼 애매할 때
  기본적으로 window의 width를 다 채우는 형태로 작동하므로, 줄바꿈이 일어난다.
  ```html
  <div>
  ```

#### 제목 태그
- 제목을 글자크기에 따라서 아래와 같이 나뉨.
```html
<h1>, <h2>, <h3>, <h4>, <h5>, <h6>
```

#### 목록 태그
```html
 <ul></ul>: unordered list.
 <li></li>: 목록의 item, list item의 약자
 <ol></ol>: ordered list. 숫자가 라벨링됨.
 <dl></dl>: 설명과 관련된 list
 <dt></dt>: 용어의 정의
 <dd></dd>: 용어의 설명
```

```html 
<ul>
  <li>학습가이드</li>
  <li>강좌선택</li>
  <li>AnswerIs</li>
</ul>

<ol>
  <li>학습가이드</li>
  <li>강좌선택</li>
  <li>AnswerIs</li>
</ol>

<dl>
  <dt>어묵탕</dt>
  <dd>따뜻한 국물..</dd>
  <dt>떡복이</dt>
  <dd>맵고 쫄깃..</dd>        
</dl>
```
#### form에서 주로 사용하는 태그
```html
<fieldset>: 묶음 표시     
<legend>: 묶음의 표시글
<label>: 라벨
<input type="text"/>: input text
<input type="submit"/>: 제출 버튼
```
```html
<form>
    <fieldset>
        <legend>검색입력필드</legend>  
        <label>과정검색</label>
        <input type="text"/>
        <input type="submit" value="검색">
    </fieldset>
</form>
```
#### Table 그리기
```html
<table>: 테이블
<table border="1">: 테이블 경계선 굵기
<tr>: 테이블의 ROW
<td>: 테이블의 Column
```

#### HTML5 TAGs(Semantic Web)
- 섹션 Tag의 종류들
```html
<section>
<aside>
<nav> 
```
- ``<header>``
 웹 문서 맨 윗부분에 위치, 웹 사이트 이름, 글로벌 링크(로그인, 회원가입, 사이트맵, 언어 선택등 웹사이트 어느 곳에서든지 이용할 수 있는 링크)등으로 구성된 영역. 사이트 이름(로고), 내비게이션, 헤드라인, 검색 등으로 구성된다. 과거에는 <div id="header">와 같이 사용했었다. 문서나 각 section, article 의 헤더 부분에 사용가능하며, 그것들의 제목이나 간단한 소개 콘텐츠를 담을 수 있다. 브라우저가 헤더영역을 인식할 수 있게되면 스크린리더의 내비게이션과 검색엔진의 색인에 도움을 줄 수 있다.
```html
<header>
    <h1>LOGO</h1>
    <h2>검색</h2>
    <input type="text">
</header>
```
- ``<main>``
 HTML5 권고후보에 main요소가 추가. 문서내 main요소가 나오는 것은 1번만 허용. 콘텐츠모델은 Flow content. 단, main요소를 article, aside, footer, header, nav요소의 하위로 사용하지 않음. 섹션 콘텐츠가 아니기 때문에 아웃라인 생성하지 않음

- ``<aside>``
 섹션 Tag 중의 하나. 페이지 전체 내용과는 어느정도 관련성이 있지만 주요 내용과는 직접적인 연관성은 없는 분리된 내용을 담고 있다. 흔히 사이드바라고 부르는 영역으로 배너, 용어 설명, 관련 상품 등 본문 내용과 직접적인 관련성이 적거나 없는 내용으로 구성된다. aside 요소로 구성된 것을 검색엔진은 무시하고 본문 위주로 색인을 진행할 수 있고, 스크린리더 사용자는 해당 영역이 어떤 성격의 영역인지 신속하게 파악할 수 있으므로, 곧바로 다른 영역으로 이동할 수도 있다.

- ``<footer>``
 웹 문서 맨 아래쪽에 있으며 저작권, 연락처등으로 구성된 영역. footer는 바닥 영역 또는 꼬리말을 지칭하는데, 저작권, 연락정보 등 본문과의 관련성은 있지만 본문에는 담기 어려운 내용을 담는다. 일반적으로 footer 영역은 한 문서 내에서 한 번만 제공되지만, section 요소나 article 요소 내에 있는 footer 요소는 해당 영역에 관한 꼬리말을 표시할 수 있다. 맨위로 가기 링크나 헤더의 메인 내비게이션도 반복 제공을 위해 푸터 영역에 둘 수 있다.

- ``<nav>``
 섹션 Tag 중의 하나. 섹션이지만 링크를 모아둠. 목적지로 이동할 수 있도록 링크를 별도로 모아둔 영역.	링크 중에서 중요도가 높은 링크를 체계적으로 구성해 놓은 것으로 단순 본문 링크와 메뉴(카테고리) 성격의 링크인지 확인이 가능. ul, li, a 요소들을 여전히 함께 사용해야 한다.	브라우저가 네비게이션 영역을 알 수 있게 되면 스크린리더의 내비게이션과 검색엔진의 색인에도 도움을 줄 수 있다.                
 ```html
<nav>
    <h1>메인 내비게이션</h1>
    <ul>
        <li>메뉴1</li>
        <li>메뉴2</li>
    </ul>
</nav>
 ```
- ``<section>``
 섹션 Tag 중의 하나. 섹션을 표시한다. 내용적 흐름과 구조를 만들기 위해 내용을 나누는 용도이다. 같은 성격의 내용, 즉 관련있는 내용을 section 요소로 묶어 표시한다. 뉴스와 광고 섹션 처럼 서로 다른 성격을 지닌 것들을 section 요소로 표시하면 영역 구분이 아주 명확해진다. 탭과 같은 상위 주제 아래에 하위 주제로 엮인 탭 방식의 구성일때 각각의 탭을 section 요소로 표시할 수 있다. 섹션은 독립적인 영역이라 섹션 내에도 헤더(header)와 푸터(footer)를 둘 수 있다. 이것은 섹션마다 나름의 제목 체계를 가질 수 있다는 것을 의미하며, 섹션마다 H1 요소를 가질 수 있게 되었다. 스크린리더 사용자는 섹션 단위로 이동할 수 있으므로 문서 내 내비게이션이 좀 더 수월해지고 검색엔진은 특정 섹션 중심으로 색인 활동을 할 수 있으므로 검색엔진의 효율성을 높일 수 있다. 단, section tag안에 ``<header><footer>`` tag를 가질 수 있다.
```html
<section>
    <article>
        <h1>제목</h1>
        <p>본문</p>
    </article>
</section>
```
- ``<article>``
독립적으로 구성된 글을 표시. 본문과 별개로 구성되어 다른 영역에 영향을 주거나 받지 않고 독립적으로 배포되거나 재사용할 수 있다. 게시판의 게시물, 블로그 포스트, 댓글, 위젯에 담긴 콘텐츠등이 article에 해당한다. 일반적인 상황에서는 section 요소가 article 요소를 포함한다. 하지만 독립적으로 구성된 내용이 몇 개의 섹션으로 구성된 경우라면 article 요소가 section 요소를 포함할 수도 있다. section 요소가 관련 있는 내용을 묶는 역할이라면 article 요소는 관련 있는 내용 중에서 독립적으로 구성된 글을 별도로 묶는 역할이다. article 영역 내에 헤더(header)와 푸터(footer)를 둘 수 있다. article 요소안에 article 요소가 들어갈 경우, 밖의 요소의 내용과 안쪽의 요소의 내용이 관련이 있는 내용이라는 것을 의미한다.
```html
<article>
    <header>
        <h1>HTML5 구조</h1>
        <p>Published On <time datetime="2013-01-22">2013년1월22일</time></p>
     </header>
     <p>본문 내용</p>
     <footer>Posted in unclepapa</footer>
     <article> <!-- 코멘트 시작 -->
         <header> 작성자:<a href="">나그네</a> at <time datetime="2013-01-22T08:45">2013년1월22일 08:45</time></header>
         <p>코멘트 내용</p>
     </article> <!-- 코멘트 끝 -->
</article>
```
## Web Developer
- Chrome 브라우저에 설치하는 웹앱
- "Google web store"검색 => chrome 웹 스토어

## CSS
- 스타일을 변경하기 위한 명령어 집합: "css_properties-1.png, css_properties-2.png" 파일 참조
- 스타일을 적용하지 않아도 기본문서의 Tag가 가지고 있는 스타일이 존재
- 개별 적용예 => "속성:값;" 형태로 적용. 예를들면, "color:blue;". 하나의 속성이라도 ";"로 끝내야 됨.
```html
 <h1 style="color:blue;font-size:5px;">메인메뉴</h1> => 제목의 색깔과 폰트 사이즈 지정
```
- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference: 정확한 CSS properties 설명

## 기본 선택자(Selector)
- 태그명, 아이디, 클래스명(그룹명)으로 적용가능
- 태그명으로 적용
```html
<h1 style="font-weight:bold; cold:blue;">제목1</h1>
<h1 style="font-weight:bold; cold:blue;">제목2</h1>
<h1 style="font-weight:bold; cold:blue;">제목3</h1>
```
#### Tag Name
- 반복적인 내용을 한번에 적용(HTML 문서내에 존재하는 h1 tag들에 모두 적용)
```html
<style>
    h1
    {
        font-weight:bold; cold:blue;
    }
</style>
```
#### Class Name
- 그룹명 앞에 태그명과 구분하기 위해 "."을 찍음.
```html
<style>
   .g1 {
         color:red;
         font-weight:bold;
        }
   ....
   <li><a href="" class="g1">학습가이드</a></li>
</style>
```
#### ID
- 한 HTML의 Element에는 ID가 중복되면 안됨
- 그룹명 앞에 태그명과 구분하기 위해 "#"을 찍음
- 아이디가 두단어 이상인 경우, "-"로 구분(id="main-menu")
- Element의 자식들이 존재하는 경우, 다같이 적용됨.
 ```html
<style>
    #name1 {
        color:blue;
        font-weight:bold;
    }
</style>
....
<li><a href="" id="name1">강좌선택</a></li>
<li><a href="" id="name2">AnswerIs</a></li><!-- id가 중복되면 안됨-->
 ```
## 콤비네이션 연산자(Combinators)
#### 종류
- Descendant selectors: A B  => A selector 자손들 중에서 B selector를 찾아라!
- Child selector: A>B => A selector 자식들 중에서 B selector를 찾아라!
- Adjacent sibling selector: A+B => A selector 오른쪽 수평방향으로 바로 이웃한 것(바로 아래 동생) 중에서 B selector를 찾아라!
- General sibling selector: A~B => A selector 오른쪽 수평방향으로 이웃한 것들(동생들) 중에서 B selector를 찾아라!
- "main-menu" id를 가지는 엘리먼트의 자손들 중, h1 tag에 적용
```html
<style>
    #main-menu h1{
      font-size:30px;
    }
</style>
```
- "main-menu" id를 가지는 엘리먼트의 자식 엘리먼트들 중, h1 tag에 적용
```html
<style>
    #main-menu>h1{
      font-size:30px;
    }
</style>  
```
- "main-menu" id를 가지는 엘리먼트의 자식 엘리먼트들 중, h1 tag에 적용. 그리고, h1과 Adjacent sibling selector관계에 있는 ul tag에 적용
```html
<style>
    #main-menu>h1+ul{
      font-size:20px;
    }
</style>
```
- "main-menu" id를 가지는 엘리먼트의 자식 엘리먼트들 중, h1과 ul tag에 적용. "#main-menu>h1+ul"형식보다 좀 더 자연스러움.
```html
<style>
    #main-menu>h1{
      font-size:20px;
    }
    #main-menu>ul{
      font-size:20px;
    }
</style>
```
- "main-menu" id를 가지는 엘리먼트의 자손 엘리먼트들 중, "first"란 이름의 class를 가진 엘리먼트에 적용. 
```html
<style>
    #main-menu .first{            // "#main-menu *.first"를 의미함. 
      font-size:100px;
    }  
</style>
<h1 class="first">서두</h1>  // 적용 안됨
<nav id="main-menu">
    <h1>메인메뉴</h1>
    <ul>
        <li class="first"><a href="">학습가이드</a></li> // main-menu의 자식 엘리먼트이므로 적용됨.
        <li><a href="">강좌선택</a></li>
        <li><a href="">AnswerIs</a></li>
        <li><nav><h1>aaaa</h1></nav></li>
    </ul>
</nav>
```
- "main-menu" id를 가지는 엘리먼트의 <li> 자손 엘리먼트들 중, "first"란 이름의 class를 가진 엘리먼트에만 적용
```html
<style>
    #main-menu li.first{
        font-size:50px;
    }
</style>
<nav id="main-menu">
    <h1>메인메뉴</h1>
    <ul>
        <li class="first"><a href="">학습가이드</a></li>
        <li><a href="" class="first">강좌선택</a></li>
        <li><a href="">AnswerIs</a></li>
        <li><nav><h1>aaaa</h1></nav></li>
    </ul>
</nav>
```
- "main-menu" id를 가지는 엘리먼트의 <ul> 자식엘리먼트의 <li> 자식엘리먼트 중에 "first"란 이름의 class를 가진 엘리먼트에만 적용.
- 해당 엘리먼트의 하위엘리먼트들도 자동으로 동일한 스타일이 적용됨. 따라서, "학습가이드", "서브메뉴 1", "서브메뉴 2"에도 적용.
```html 
<style>
    #main-menu>ul>li.first{
        font-size:40px;
        font-weight:bold;
    }
</style>
<nav id="main-menu">
    <h1>메인메뉴</h1>
    <ul>
        <li class="first">
            <a href="">학습가이드</a>
            <ul>
                <li class="first">서브메뉴 1</li>
                <li>서브메뉴 2</li>
            </ul>
        </li>
        <li><a href="" class="first">강좌선택</a></li>
        <li><a href="">AnswerIs</a></li>
        <li><nav><h1>aaaa</h1></nav></li>
    </ul>
</nav>
```
- "main-menu" id를 가지는 엘리먼트의 <ul> 자식엘리먼트의 <li> 자식엘리먼트 중에 "first"란 이름의 class를 가진 엘리먼트에 바로 동생인 "aa"란 이름의 class를 가진 엘리먼트에만 적용. 
- 결국, "강좌선택"에는 적용되고, "AnswerIs"에는 적용 안됨.
```html
<style>
    #main-menu>ul>li.first+.aa{
        font-size:100px;
        color:red;
    }
</style>
<nav id="main-menu">
    <h1>메인메뉴</h1>
    <ul>
        <li class="first">
            <a href="">학습가이드</a>
            <ul>
                <li class="first">서브메뉴 1</li>
                <li>서브메뉴 2</li>
            </ul>
        </li>
        <li class="aa"><a href="">강좌선택</a></li>
        <li class="aa"><a href="">AnswerIs</a></li>
        <li><nav><h1>aaaa</h1></nav></li>
    </ul>
</nav>
```
- "main-menu" id를 가지는 엘리먼트의 <ul> 자식엘리먼트의 <li> 자식엘리먼트 중에 "first"란 이름의 class를 가진 엘리먼트들에 동생들 중 "bb"란 이름의 class를 가진 엘리먼트에 적용. 
- 결국, "aaaa"에 적용
```html
<style>
    #main-menu>ul>li.first~.bb{
        font-size:50px;
        color:blue;
    }
</style>
<nav id="main-menu">
    <h1>메인메뉴</h1>
    <ul>
        <li class="first">
            <a href="">학습가이드</a>
            <ul>
                <li class="first">서브메뉴 1</li>
                <li>서브메뉴 2</li>
            </ul>
        </li>
        <li class="aa"><a href="">강좌선택</a></li>
        <li class="aa"><a href="">AnswerIs</a></li>
        <li class="bb"><nav><h1>aaaa</h1></nav></li>
    </ul>
</nav>
```

#### CSS Style 적용 순서
- 콘텐츠 블록 스타일을 먼저 작업 후, 레이아웃 블록 스타일을 작업("css_style_apply_order.png" 참조)

## Selectors 정리
1) Basic Selectors
- Type Selector: 엘리먼트명
- Class Selector: .클래스명
- ID Selector: #ID명
- Universal Selector: *
- Attribute Selector: [속성=값]

2) Combinators
- Descendant Selector: A B
- Child Selector: A > B
- Adjacent Sibling Selector: A + B
- General Sibling Selector: A ~ B

## Attribute Selector(속성 선택자)
1) 관련 사이트 - https://developer.mozilla.org/en-US/docs/Web/CSS/Attribute_selectors
2) 문법 설명
[attr]
Represents elements with an attribute name of attr.
[attr=value]
Represents elements with an attribute name of attr whose value is exactly value.
[attr~=value]
Represents elements with an attribute name of attr whose value is a whitespace-separated list of words, one of which is exactly value.
[attr|=value]
Represents elements with an attribute name of attr whose value can be exactly value or can begin with value immediately followed by a hyphen, - (U+002D).
It is often used for language subcode matches.
[attr^=value]
Represents elements with an attribute name of attr whose value is prefixed (preceded) by value.
[attr$=value]
Represents elements with an attribute name of attr whose value is suffixed (followed) by value.
[attr*=value]
Represents elements with an attribute name of attr whose value contains at least one occurrence of value within the string.
[attr operator value i]
Adding an i (or I) before the closing bracket causes the value to be compared case-insensitively (for characters within the ASCII range).
[attr operator value s] 
Adding an s (or S) before the closing bracket causes the value to be compared case-sensitively (for characters within the ASCII range).
<style>
    /* All divs with a `lang` attribute are bold. */
    div[lang] {
        font-weight: bold;
    }

    /* All divs without a `lang` attribute are italicized. */
    div:not([lang]) {
        font-style: italic;
    }
    
    /* All divs in US English are blue. */
    div[lang~="en-us"] {
        color: blue;
    }
    
    /* All divs in Portuguese are green. */
    div[lang="pt"] {
        color: green;
    }
    
    /* All divs in Chinese are red, whether simplified (zh-CN) or traditional (zh-TW). */
    div[lang|="zh"] {
        color: red;
    }
    
    /* All divs with a Traditional Chinese `data-lang` are purple. */
    /* Note: You could also use hyphenated attributes without double quotes */
    div[data-lang="zh-TW"] {
        color: purple;
    }
</style>
<html>
    <div lang="en-us en-gb en-au en-nz">Hello World!</div>
    <div lang="pt">Olá Mundo!</div>
    <div lang="zh-CN">世界您好！</div>
    <div lang="zh-TW">世界您好！</div>
    <div data-lang="zh-TW">世界您好！</div>
</html>

<style>
    a {
        color: blue;
    }

    /* Internal links, beginning with "#" */
    a[href^="#"] {
        background-color: gold;
    }
    
    /* Links with "example" anywhere in the URL */
    a[href*="example"] {
        background-color: silver;
    }
    
    /* Links with "insensitive" anywhere in the URL, regardless of capitalization */
    a[href*="insensitive" i] {
        color: cyan;
    }
    
    /* Links with "cAsE" anywhere in the URL, with matching capitalization */
    a[href*="cAsE" s] {
        color: pink;
    }
    
    /* Links that end in ".org" */
    a[href$=".org"] {
        color: red;
    }
    
    /* Links that start with "https" and end in ".org" */
    a[href^="https"][href$=".org"] {
        color: green;
    }
</style>
<html>
    <ul>
        <li><a href="#internal">Internal link</a></li>
        <li><a href="http://example.com">Example link</a></li>
        <li><a href="#InSensitive">Insensitive internal link</a></li>
        <li><a href="http://example.org">Example org link</a></li>
        <li><a href="https://example.org">Example https org link</a></li>
    </ul>
</html>

3) 사용예
<style>
    #member-menu a[href]{
        font-size:30px;
        color:green;
    }
</style>
<nav id="member-menu">
    <h1>회원메뉴</h1>
    <ul>
        <li><a href="../index.html">HOME</a></li>
        <li><a href="../member/login.html">로그인</a></li>
        <li><a href="../member/signup-agree.html">회원가입</a></li>
        <li>회원탈퇴</li>
    </ul>
</nav>
=> "member-menu" id를 가지는 엘리먼트의 <a> Tag를 사용하는 자손엘리먼트 중, href 속성(attribute)를 가진 엘리먼트들에게만 적용
=> "HOME", "로그인", "회원가입"에는 적용되나, "회원탈퇴"에는 적용안됨.
<style>
    #member-menu a[href="../index.html"]{
        font-size:30px;
        color:red;
    }
</style>
<nav id="member-menu">
    <h1>회원메뉴</h1>
    <ul>
        <li><a href="../index.html">HOME</a></li>
        <li><a href="../member/login.html">로그인</a></li>
        <li><a href="../member/signup-agree.html">회원가입</a></li>
        <li>회원탈퇴</li>
    </ul>
</nav>
=> "member-menu" id를 가지는 엘리먼트의 <a> Tag를 사용하는 자손엘리먼트 중, href 속성(attribute)의 값이 "../index.html"인 엘리먼트들에게만 적용
=> "HOME"에만 적용

## Selector 예제들
1) "doc/Selector_example_*.png" 파일들을 참조

## Selector 우선순위
1) 아래와 같이 Selector들을 함께 사용해서 한 Element에서 충돌난다면? 
#h2 { color: green;}
h1 { color: orange;}
.h2 { color: red;}
=> 적용범위가 넓을수록, 우선 순위가 낮다.
   ID Selector > Class Selector > Type Selector
   "Selector_priority_1.png" 파일 참조

2) 동일한 연산 순위의 재정의
.h1 { color: green;}
.h1 { color: orange;}
.h1 { color: red;}
=> 차례대로 적용되기 때문에, 마지막 색깔이 적용된다.
   "Selector_priority_2.png" 파일 참조
=> 이런 경우가 있나?
   스타일 파일을 가져다 쓰고, 마음에 안드는 부분은 재정의해서 사용하면 된다.  

3) 복잡한 경우의 수
h1.h1 { color : green; }  <!-- 1번 -->
section > .h1 { color : orange; } <!-- 2번 -->
section > h1 { color : blueviolet; } <!-- 3번 -->
.h1 { color : red; } <!-- 4번 -->
=> 1번과 4번을 비교하면 1번이 적용범위가 작기 때문에, 우선 순위가 높음
=> Tag보다 combinator 연산자가 우선 순위가 높기 때문에, 1번과 2번을 비교하면 2번이 우선 순위가 높음
=> 2번과 3번을 비교하면, 2번이 적용 범위가 작기 때문에 우선 순위가 높음.
=> "Selector_priority_3.png" 파일 참조

h1[lang="ko"]{ color: blue;} <!-- 1번 -->
.h1 { color : red; } <!-- 2번 -->
h1 { color : gray; } <!-- 3번 -->
=> 속성을 사용한 것은 사용하지 않은 것보다 우선순위가 높아서 1번이 3번보다 높음
=> 속성을 사용한 것이 클래스보다 속성이 높아서 1번이 2번보다 높음
=> "Selector_priority_4.png" 파일 참조

## 스타일 링크하기
1) html에 직접 스타일을 지정하는 것보다는 외부 CSS파일을 만들고, 링크를 걸어서 여러 HTML에서 사용하도록 하는 방식이 효과적
=> "external_css_link_1.png" 파일 참조
2) Root에 CSS폴더를 생성하고, style.css 파일을 생성하여 아래의 내용을 작성.
<style>
...
</style>
3) html 파일에 <head>에 생성한 CSS파일을 상대경로를 통하여 명시
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <link href="../css/style.css" type="text/css" rel="stylesheet">    
</head>

## 스타일 리셋, 평준화, 현대화
1) reset.css
=> html이 기본적으로 사용하고 있는 스타일을 전부 없애고 싶어서 어떤 사용자가 만든 스타일시트 파일을 공유함.
2) normalize.css
   => html이 기본적으로 사용하고 있는 스타일을 승계받아서 사용하고,
   브라우저마다 차이가 나는 부분을 새로운 스타일로 재정의하여서 동일하게 맞춘 스타일 시트를 공유함.
3) reset.css 또는 normalize.css 중 어느 것을 사용하느냐?
=> 최근에는 대부분 리셋 후, 새로 정의해서 사용하는 방식을 채택
=> 구글 사이트등 여러 곳에서 reset.css를 제공
=> 남이 만든 것을 사용하지 않고, 우리는 reset하는 방법을 배울 것임.

4) 현대화 - 구버전의 브라우저 지원
=> HTML5를 지원하지 않는 예전 브라우저들에 대한 호환성제공
=> HTML5를 지원하지 않는 예전 브라우저들은 HTML5 Tag들(article, section, nav, video, audio etc)를 인식하지 못함.
=> "https://modernizr.com/"에서 "Add your detects"메뉴에서 특정 tag들을 브라우저에서 지원하는 체크하는 함수를 예제로 제공.
   특정 Tag를 클릭해서 "view examples"를 클릭하면 됨
예) "canvan" tag를 지원하는 지 체크하는 방법
.no-canvas .box { color: red; }
.canvas .box { color: green; }
JS
if (Modernizr.canvas) {
    // supported
} else {
    // not-supported
}

## 레이아웃 블록
1) 콘텐츠 블록 스타일 VS 레이아웃 블록 스타일
- "Contents_VS_Layout_Block_Style.png" 참조

2) 레이아웃 블록 스타일을 적용 후, 콘텐츠 블록 스타일을 적용
3) 레이아웃 배치 : 격자형은 단 방향을 중첩해서 만든다.
- 격자형은 단방향으로 나눌 수 있기 때문에, 수평(수직)을 먼저 나눈 후, 다시 수직(수평)으로 중첩해서 계속 나누어 가면 된다.
- "Layout_Block_Example_X.png"

## 제일 큰 방(Box) 꾸미기
1) 가장 큰 방을 수평 또는 수직으로 나눈다.
2) "Layout_Biggest_Box_X.png" 참조
3) header, visual, body, footer에 대한 ID 생성 후, 높이 지정
 => 높이를 지정하지 않으면, content들에 따라 달라짐.
    높이를 작게 지정하면, content가 겹쳐 보일 수 있음
    => Html 파일 영역 선택 후,  Ctrl + K + C 하면 주석처리됨.
    예) style.css 파일
    /* header Tag를 직접 사용하지 않음. section과 article Tag안에도 올 수 있기 때문.
    따라서, id를 사용 */
    #header {
    height: 70px;  /* 높이 지정, 지정하지 않으면, content들에 따라 달라짐 */
    background: yellow;
    }

#visual {
    height: 171px;
    background: green;
}

#body {
    height: 300px;
    background: red;
}

#footer {
    height: 100px;
    background: gray;
}

## reset 파일 생성
1) "제일 큰 방(Box) 꾸미기"을 해보면, 상하좌우 여백이 존재
=> HTML 기본 속성이 적용되기 때문
2) 실제 구성요소는 아래와 같이 구성
- content
- padding: 실제 content와 border 사이의 간격
- border
- margin: 창 전체와 border사이의 간격 => 상하좌우 여백이 존재하는 이유.
3) reset.css 파일을 추가 후, 아래 내용을 첨가
body {
    margin: 0px;
}
4) reset.css의 링크를 생성하는 두가지 방법
- 첫번째 방법: list.html파일에 아래의 내용을 추가
<link href="../css/reset.css" type="text/css" rel="stylesheet">
- 두번째 방법: 기존의 style.css 파일의 내용에 import함.     
@import url("reset.css");
- 두번째 방법이 로딩 속도가 느리다. 그러나, 관리하는 면에서는 두번째 방법이 좋다.

## 색상값
1) Color Keywords vs Hex vs Decimal
2) "Color_Value_Define.png" 참조
3) Color Keywords로 표현가능한 색깔은 256가지 정도이다.
4) Hex 표현
- 24bit로 표현
- 각 8bit는 R, G, B를 표현
- 대소문자 구별안함.
예)
#c0c0c0
#000000 => 검정색 
#ffffff => 흰색
#ff0000 => 빨간색  
5) Decimal 표현
- rgb(255, 0, 0);
- rgb(100%, 0%, 20%); // 퍼센트로도 표현가능
6) 투명도 조절(Transparent)
- 호환되지 않는 브라우저가 존재.
- 1에 가까울수록, 불투명해짐.
예)
rgba(255, 0, 0, 0.2);
#ff0000f0
7) Hue-saturation-lightness model(HSL)
hsl(30, 100%, 50%);
8) System Colors - 윈도우 OS의 테마 색깔을 사용 가능
- ActiveBorder: Active window border
- ActiveCaption: Active window caption. Should be used with CaptionText as foreground color.
- AppWorkspace: Background color of multiple document interface
- Background: Face background color of 3D elements that appear 3D due to one layer of surrounding border.
              Should be used with the ButtonText foreground.

## 두번째 방 설정하기(박스 정렬과 최소 높이)
1) 격자형은 단 방향을 중첩해서 만든다.
2) 화면을 세로로 세부분 나누면, 중간 부분에만 컨텐츠가 위치한다.
- "Layout_Second_Box.png" 참조
3) 부모의 속성값을 상속하기: "inherit"
   예) 부모의 높이 값을 상속
   #header {
    height: 70px;  /* 높이 지정, 지정하지 않으면, content들에 따라 달라짐 */
    background: #FFFF00f0;
   }
    #header>.content-box {
        height: inherit;
        background: red;
    }
   예) 부모의 높이을 100% 채움
   #header {
    height: 70px;  /* 높이 지정, 지정하지 않으면, content들에 따라 달라짐 */
    background: #FFFF00f0;
   }
    #header>.content-box {
        height: 100%;
        background: red;
    }
4) 블록의 너비 고정하기
- 윈도우 창을 줄여도 고정됨.
- width를 지정하지 않으면, 부모의 너비를 채움.
- 너비를 줄여서 부모 element를 채우지 못하면, 기본적으로 왼쪽으로 align됨.
  예) 왼쪽 정렬
    #header>.content-box {
        height: inherit;
        width: 960px;
        background: red;
    }
5) 블록의 오른쪽 정렬 방법
- "Layout_right_align.png" 참조
- "margin-left:auto;"을 명시하면, 오른쪽 정렬됨.
  예)
    #header>.content-box {
        height: inherit;
        width: 960px;
        margin-left:auto;
        background: red;
    }
6) 블록의 가운데 정렬 방법
- "Layout_center_align.png" 참조
- "margin-left:auto;"와 "margin-right:auto;"을 함께 명시하면, 가운데 정렬됨.
  예)
    #header>.content-box {
        height: inherit;
        width: 960px;
        margin-left:auto;
        margin-right:auto;
        background: red;
    }
## 세번째 방 설정하기
1) 중앙에 정렬된 두번째방을 좌우로 나누기. "Layout_Third_Box.png" 참조.
2) 시각적인 방을 만들 때는, <section>보다는 <div>를 이용
3) <section> 문서의 내용을 가지고 있는 영역. style과는 관련이 없다.
4) "<div id="body">"의 "<div class="content-box">"는 <aside>와 <main>을 그대로 사용해도 좋다.
5) 블록(Block) 형식의 기본 배치방식
- "Layout_Third_Box_1.png" 참조
- 블록들을 나열하면, 위에서부터 아래로 수직적으로 배치된다.
- 좌우로 배치하고자 할 때.
  ● float를 left로 변경하여 사용 => 과거에 사용하던 꼼수 방법
  ● 상위 Element에서 display를 flex로 지정 => 현재 방식
  예)"#body>.content-box"가 "#aside"와 "#main"의 상위 엘리먼트일 경우.
    #body>.content-box {
        display: flex;
    }
  
    #aside {
        height: inherit;
        width: 205px;        
        background: red;
    }

    #main {
        height: inherit;
        width: 755px;
        background: yellow;
    }
## 콘텐츠 블록과 절대좌표
1) CSS 2.0까지는 레이아웃 기법이 존재하지 않았으나, CSS 3.0부터 나오기 시작.
2) CSS 2.0까지는 컨텐츠(목록, 표, 제목, 문장, 폼, 기타(div))가 수직으로 쌓이는 방법밖에 존재 안함.
3) "Content_layout_01.png" 참조
4) Flex기법을 사용하면, 수평(오른쪽->왼쪽 또는 왼쪽->오른쪽) 배치도 가능.
   수직으로 아래에서 위로 쌓을 수 있다.
5) Grid기법을 사용하면, 컨텐츠들을 원하는 위치에 배치 가능.
=> 최신 기법. 지원하지 않는 브라우저가 있을 수 있음. 
6) 콘텐츠 블록의 일부분의 위치를 정하기.
=> "Content_layout_02.png" 참조
- Absolute 기법
- Relative 기법
- fixed 기법
- sticky 기법
7) <li> tag의 기본 Layout
- 높이는 컨텐츠 내용의 높이. 컨텐츠가 없으면, 0
- 너비는 화면을 다 채우는 너비(100%)
- 위치는 위의 tag아래에 위치
8) position의 속성의 기본값은 "static": Tag가 정해진 위치에 존재.
9) position의 속성을 "absolute"로 하면, 문서전체에서 정해주는 좌표의 위치에 존재.
   지정하면, 기본적으로 부모 Tag와의 관계가 사라지면서, 너비가 컨텐츠 크기만큼으로 줄어듬.
   다른 Tag들과 겹칠수도 있음. absolute가 명시된 Tag가 다른 tag보다 위에 Display됨.
   단, 부모 position속성을 relative로 변경하면 부모 tag내의 위치로 변경됨.   
   예1) 
   #s1 li:nth-child(2) {
    background: green;
    position: absolute;
    left: 100px;
    top: 100px;
   }

예2) 화면 크기에 상관없이 오른쪽 끝에 붙이고 싶은경우 => "right: 0px"을 명시
#s1 li:nth-child(2) {
    background: green;
    position: absolute;
    right: 0px;
    top: 30px;
}

예3) 화면 크기에 상관없이 아래쪽 끝에 붙이고 싶은경우 => "bottom: 0px"을 명시
#s1 li:nth-child(2) {
    background: green;
    position: absolute;
    right: 0px;
    bottom: 0px;
}

예4) 부모 Tag안에서 절대좌표를 사용하고 싶은 경우
=> 부모 Tag인 "ul"의 position 속성을 "relative"로 변경하면 됨.
=> 부모 Tag안의 위치에서 위치가 결정됨.
#s1 ul {
    background: yellow;
    height: 500px;
    position: relative;
}

#s1 li:nth-child(1) {
    background: red;
}

#s1 li:nth-child(2) {
    background: green;
    position: absolute;
    right: 0px;
    bottom: 0px;
}

#s1 li:nth-child(3) {
    background: blue;
}

## 콘텐츠 블록과 상대좌표(Relative 기법)
1) 원래 존재하는 위치에서 상대 좌표로 이동
2) 기존에 원래 존재하는 위치는 공백으로 남겨둠.
=> sibling tag들도 그대로 위치함.
예) 
@import url(css/reset.css);

#s1 ul {
    background: yellow;
    height: 500px;
    width: 500px;
}

#s1 li:nth-child(1) {
    background: red;
    position: relative;
    left: 50px;
    top: 30px;
}

-- 위치 변동 없음
#s1 li:nth-child(2) {
    background: green;
    
}
3) 부모를 relative해서 offset을 주면, 모든 child들도 함께 이동
@import url(css/reset.css);

#s1 ul {
    background: yellow;
    height: 500px;
    width: 500px;
    position: relative;
    left: 50px;
    right: 30px;
}

#s1 li:nth-child(1) {
    background: red;
    position: relative;
    left: 50px; -- 50px + 50px에 위치
    top: 30px;  -- 30px + 30px에 위치
}

## 콘텐츠 블록과 고정위치(fixed 기법)
1) 원래 존재하는 위치는 동생 sibling들이 채움
2) 해당 tag를 고정된 위치로 이동시킴.
3) absolute와의 차이점
- absolute: 브라우저 창이 스크롤되면, 해당 tag가 화면에서 사라짐. (문서기준 위치)
- fixed: 브라우저 창이 스크롤 되더라도 화면상의 정해진 위치에 표시됨. (브라우저 화면영역기준 위치)
         화면상의 퀵메뉴처럼 항상 보이게 할 때 사용.
     예)
     @import url(css/reset.css);

#s1 ul {
    background: yellow;
}

#s1 li:nth-child(1) {
    background: red;
}

#s1 li:nth-child(2) {
    background: green;
    position: fixed;
    width: 100%;
    bottom: 0px;    
}

#s1 li:nth-child(3) {
    background: blue;
}
4) 부모의 position을 "relative"로 하고, height를 명시해도, 해당 Tag의 위치가 변하지 않음
=> 화면을 기준으로 하기 때문. 아래 예제에서 "#s1 li:nth-child(2)"의 위치는 변화 없음.
예)
@import url(css/reset.css);

#s1 ul {
    background: yellow;
    height: 300px;
    position: relative;
}

#s1 li:nth-child(1) {
    background: red;
}

#s1 li:nth-child(2) {
    background: green;
    position: fixed;
    width: 100%;
    bottom: 0px;    
}

#s1 li:nth-child(3) {
    background: blue;
}

## 콘텐츠 블록과 붙임위치(sticky 기법)
- 최근에 등장한 기법. 모바일에서 사용하던 기법이 CSS에 추가됨
- 주석처리: Ctrol + k후, c버튼
#### 사용자가 header를 화면 위쪽에 고정하기를 원하는 경우
- 아래와 같이 fixed기법을 사용하면, header가 동생 sibling를 가리는 문제가 발생
- 아래의 예에서는 "포지션: absolute"란 글자가 안 보임.(50px에 포함되는 tag들)
- css
```css
#header {
    height: 50px;
    background: beige;
    position: fixed;
    width: 100%;
    top: 0px
}
```
- Html
```html
<header id="header">
    <h1>뉴렉처</h1>
</header>
<section id="s1">
    <h1>포지션: absolute</h1>
    <ul>
        <li>1</li>
        <li>2</li>
        <li>3</li>
    </ul>
</section>
```
- 아래와 같이 header의 position을 "sticky"로 하면 해결됨.
- 주의할 사항으로, "top" 속성을 꼭 명시해줘야 동작함.
```css
  #header {
    height: 50px;
    background: beige;
    position: sticky;
    width: 100%;
    top: 0px
  }
```

## Flex Display 학습내용
#### Flex Terminology
- flex container
- flex item
#### Flexibility
- flex
- flex-grow
- flex-shrink
- flex-basis
#### Flex lightness
- flex-wrap
- flex-Flow
#### Orientation & Ordering
- flex-direction
- order
#### Alignment
- justify-content
- align-items
- align-self

## Flex 레이아웃과 용어
#### 기존 방식
- CSS2의 레이아웃을 위한 Display 방식: "layout_css_2.png" 참조
- 컨텐츠 블록들에 대해 수직적인 배치만을 허용: "layout_contents_block_old.png" 참조
#### 최근 방식
- 최근에는 컨텐츠 블록들에 대해 수평적인 배치도 가능 : Flex
- "layout_contents_block_new.png" 참조
#### Flex 컨테이너와 용어
- "flex_container_term.png" 참조
- flex container
- main size, cross size, main start, main end, cross start, cross end, main axis, cross axis
- flex item 
- main axis: 사용자가 기준으로 삼는 축(수평 또는 수직)
- cross axis: main axis에 90도되는 축
#### Flex 방향 설정하기
- "flex_direction_set.png" 참조
- row: 수평 방향으로 왼쪽에서 오른쪽으로
- row-reverse: 수평 방향으로 오른쪽에서 왼쪽으로
- column: 수직 방향으로 위에서 아래로
- column-reverse: 수직 방향으로 아래에서 위로
- flex-wrap: nowrap | wrap | wrap-reverse. "flex_direction_wrap.png" 참조
#### Flex 정렬 옵션
- "flex_align_option.png" 참조
- 수평축 정렬 옵션(main-axis): "flex_main_axis_align.png" 참조
  ```html
  justify-content: flex-start | flex-end | center | space-between | space-around
  ```
- 수직축 정렬 옵션(cross-axis): "flex_cross_axis_align.png" 참조
  ```html
  align-items: stretch | flex-start | center | space-between | space-around
  ```
## Flexibility 

#### flex 레이아웃 설정하기

- inline-flex(display): flex안에 들어가는 tag들이 inline tag들인 경우
- flex(display): flex안에 들어가는 tag들이 block tag들인 경우
- inline-flex와 flex간의 차이가 거의 없음

#### flex-grow

#### flex-shrink

#### flex-basis

## Flex Lines 

#### flex-direction

- ``<ul>``  Tag에 ``display: flex;``를 명시하면, 기본적으로 자식 tag들이 수평으로 표시
- flex가 적용되면, 너비를 다 채우던 ``<li>`` Tag가 content의 내용에 따라서 너비와 높이가 결정
- 수직과 수평의 방향 선택은 ``flex-direction`` 속성을 이용
  - ``flex-direction: row;`` :  수평방향으로 Tag들을 표시함
  - ``flex-direction: row-reverse;`` :  오른쪽에서 왼쪽 수평방향으로 Tag들을 표시함
  - ``flex-direction: column;`` :  수직방향으로 Tag들을 표시함
  - ``flex-direction: column-reverse;`` :  아래에서 위로 수직방향으로 Tag들을 표시함

#### flex-basis

- 축방향(row, column)으로의 크기(너비 또는 높이)를 ``flex-basis: 100px;`` 정해줄 수 있음
- 축방향과 관련없이 높이와 너비를 지정하고 싶으면, ``width: 100px;``와 ``height: 100px;``를 사용

- html

```html
<body>
    <section class="s1">
        <h1>flex box</h1>
        <ul>
            <li>1</li>
            <li>2</li>
            <li>3</li>
            <li>4</li>
            <li>5</li>
        </ul>
    </section>
</body>    
</html>
```

- CSS

```css
@import url(css/reset.css);
.s1 ul {
    display: flex;
    flex-direction: row; /* 자손들이 수평방향으로 display 됨. */
    background: gray;
}

.s1 li:nth-child(1) {
    background: red;
    flex-basis: 100px;   /* 축 방향으로 100px을 지정 */
}

.s1 li:nth-child(2) {
    background: green;
}

.s1 li:nth-child(3) {
    background: blue;
}

.s1 li:nth-child(4) {
    background: yellow;
}

.s1 li:nth-child(5) {
    background: lightblue;
}
```



#### flex-wrap

#### flex-flow