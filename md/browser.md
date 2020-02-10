# 웹 사이트 분석

## 1. HTML안에 js, css의 위치는?

### js 
주로 문서 하단에 위치

script태그를 만나면 스크립트가 해석, 실행되는 동안 문서의 파싱은 중단된다. 

### css  
주로 문서 상단에 위치

DOM트리를 변경하지 않기 때문에 문서 파싱을 기다리거나 중단되지 않는다.

## css가 js보다 하단에 위치한다면?
스크립트가 문서를 파싱하는 동안 브라우저는 다른 작업을 수행하지 않기 때문에 스타일이 파싱되지 않는 상태가 된다.

스크립트 소스를 하단에 두면 HTML문서를 화면에 표시하는 속도가 빨라지고 사용자가 뷰를 보는데 필요한 문서를 해석한 상태이기 때문에 불편을 초래하지 않는다.

문서 `head`영역에 스크립트가 삽입되거나 외부 파일에 정의되어 있다면 `defer` `async`속성을 사용할 수 있다.

## 2. 화면을 표시하기 위해 어떤 파일들이 다운로드 되는가?

### Website는 어떻게 보여주게 될까?

웹 페이지가 렌더링되는 과정  


#### 1. 브라우저는 어떻게 문서를 표현할까?
먼서 브라우저는 서버에서 받아온 HTML 문서를 W3C (World Wide Web Consortium)에서 정한 명세를 따라 HTML을 해석합니다. 그리고 해석된 문서는 브라우저 렌더링 엔진에 따라서 브라우저에서 사용자가 볼 수 있도록 그리기 시작합니다. 하지만 브라우저 별로 화면에 그리는 방식은 다릅니다. 
> 대표적으로 Chrome과 Safari는 Webkit 엔진을 사용하며, 파이어폭스는 Gecko 엔진을 사용합니다.  

> 브라우저다 그리는 법은 달라도 비슷하게 보여줄 수 있는 까닭은 W3C에서 정한 웹 표준 명세가 있기 때문입니다. 때문에 파이어폭스/사파리/크롬/익스플로어가 비슷한 형태로 구현 가능합니다. 하지만 표준 명세이기 때문에 특정 기능의 경우 브라우저 별로 차이가 있을 수 있습니다.  


#### 2. 브라우저 구조를 알아보자.

<img width="400"  src="https://miro.medium.com/max/1000/0*N7nIqUv99_Z5iWKU.png">  

브라우저는 크게 화면을 조정하는 영역과 데이터를 조작하는 영역으로 구분할 수 있습니다.  

|목록|내용|
|:---|:---|
|사용자 인터페이스|사용자가 브라우저에서 직접 조작할 수 있는 영역입니다.(앞으로가기, 뒤로가기, 즐겨찾기 등)|
|브라우저 엔진|사용자 인터페이스가 렌더링 엔진에 쿼리를 전달할 수 있게 조작을 담당합니다.|
|렌더링 엔진|HTML과 CSS 문서를 파싱/해석하여 화면에 표현합니다.|
|Networking|http 요청을 할 수 있으며 네티워크를 호출할 수 있습니다.|
|javascript 해석기|javascript 코드를 해석하고 실행합니다.|
|UI Backend|select/input 등 기본적인 위젯을 그리는 인터페이스입니다. |
|자료 저장소|Cookie, Local storage 등 모든 자료를 저장하는 영역입니다.|  

먼저 브라우저는 서버로부터 `HTML 문서를 모두 다운로드` 받습니다. 다운로드가 완료되면 `렌더링 엔진이 HTML 문서를 파싱해 렌더링 트리를 생성`합니다. 렌더링 트리 생성이 완료되면 `UI Backend에서 각 노드를 확인`하며, `화면에 그리기 시작`합니다.  

> <img width="400" src="https://miro.medium.com/max/1248/0*RBH9pfLPYaIQEf9T.png">  
>
>
> 웹킷과 게코의 렌더링 방식은 크게 차이가 없습니다.  
> <img width="400" src="https://miro.medium.com/max/1248/0*cdKyPMWdOZ2g-AkV.jpg">  
>
> 게코에 콘텐츠 싱크는 과정이 있지만 DOM 요소를 생성함에 있어 웹킷과 큰 차이는 없습니다.  

#### 3. DOM 트리를 구축하자.

HTML 문서를 받아오면, 렌더링 엔진이 HTML 파서를 이용해 파싱을 시작합니다. 그리고 파싱이 완료되면 문서 구조는 Parse Tree로 생성됩니다. 파싱하는 문서는 어휘 분석과 구문 분석으로 해석합니다. 어휘 분석은 자료의 유효한 토큰(의미없는 문자와 공백)을 분해하고, 구문 규칙으로 문서 구졸르 분석합니다. 어휘 분석으로 html 태그를 토큰으로 파싱합니다. 해당 과정을 통해 parser tree가 만들어집니다.  

<img src="https://miro.medium.com/max/202/0*sIyIJ8BcNNYpKMtl.png">  

parse tree를 기반으로 DOM 요소와 속성 노드를 가지는 DOM Tree를 생성합니다.  

``` html
<html>
<body>
    <p>Hello World</p>
    <div>
        <img />
    </div>
</body>
</html>
```

<img src="https://miro.medium.com/max/800/0*6bAj33VHxBWMxAZa.png">  

트리 생성이 끝나면 브라우저는 화면을 그리기 시작하며, 문서는 ready 상태가 되고 load 이벤트가 발생됩니다. DOM 로드가 완료되면 javascript를 다운로드하기 시작하며 javascript도 파싱합니다. 하지만 CSS 파서는 DOM Tree에 영향을 주지 않기 때문에 문서를 파싱하는 동시에 파싱을 진행합니다.  


<img src="https://miro.medium.com/max/1000/0*1biOcX1NF80wt4-f.png">  


#### 4. 렌더 트리를 만들어보자.
DOM Tree가 구축이 되어가는 동안 브라우저는 DOM Tree를 기반으로 렌더 트리를 생성합니다. 문서를 시각적인 구성 요소로 만들어주는 역할을 합니다. 하지만 1:!로 대응되지는 않습니다. 대표적인 예로 `<head>`나 `display: none; hidden`은 렌더 트리에 포함되지 않습니다.  

<img src="https://miro.medium.com/max/1462/0*IiYSaLxVgjuornbD.png">  

스타일은 브라우저에서 제공하는 기본 스타일 시트를 따라갑니다. 적용된 스타일 속성에 따라 렌터 트리를 구축합니다.  


> [Website는 어떻게 보여주게 될까?](https://medium.com/@pks2974/website%EB%8A%94-%EC%96%B4%EB%96%BB%EA%B2%8C-%EB%B3%B4%EC%97%AC%EC%A3%BC%EA%B2%8C-%EB%90%A0%EA%B9%8C-f1193c844480)

### 웹 브라우저의 HTML문서 렌더링 과정

#### 1. 불러오기
로더(Loader)가 서버로부터 전달 받는 리소스 스트립을 읽는 과정.  
읽으면서 어떤 파일인지, 데이터인지 파일을 다운로드 할 것인지 등을 결정한다.  

#### 2. 파싱(Phasing)
웹 엔진이 가지고 있는 `HTML/XML 파서가 문서를 파싱해서 DOM Tree`를 만든다.  

#### 3. 렌더링 트리 만들기
`DOM Tree`는 내용을 저장하는 트리로 javascript에서 접근하는 `DOM 객체`를 쓸 때 이용하는 것이고 별도로 그리기 위한 트리가 만들어져야 하는데 그것이 `렌더링 트리`다.  
(그릴 때 필요없는 haed, title, body 태그 등이 없음 + `display: none;`처럼 DOM에는 있지만 화면에서는 걸러내야할 것들을 걸러낸다.)  

#### 4. CSS 결정
CSS는 선택자에 따라서 적용되는 태그가 다르기 때문에 모든 CSS style을 분석해 태그에 스타일 규칙이 적용되게 결정한다.  

#### 5. 레이아웃
렌더링 트리에서 위치가 크기를 가지고 있지 않기 때문에 객체들에게 위치와 크기를 정해주는 과정을 레이아웃이라고 함.

#### 6. 그리기
렌더링 트리를 탐색하면서 그리기.  




[웹 브라우저에서 HTML문서 렌더링 과정(동작 순서)](https://jeong-pro.tistory.com/90)  






## 3. 특정 자원의 Request Headers 와 Response Headers의 내용을 분석.(네트워크 탭 활용)


## Request Headers
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
- 클라이언트 자신이 원하는 미디어 타입 및 우선순위를 알린다.
>Ex) Accept: \*/* (어떤 미디어 타입도 가능하다)
Ex) Accept: image/* (모든 이미지 유형이 가능하다)


Accept-Encoding: gzip, deflate, br
- 클라이언트 자신이 원하는 문자 인코딩 방식

Accept-Language: ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7
- 클라이언트 자신이 원하는 가능한 언어

Cache-Control: max-age=0
- max-age로 캐시 유효시간을 줄 수 있다. 
- 초 단위이며 위 캐시 유효시간은 0초이다.

Connection: keep-alive

Cookie: webid=50e7d70025de11ea99aa000af759d7a0; 
dtck_first=20200203; dtck_refresh=0; dtck_media=-1; dtck_blog=-1; dtck_channel=-1; dtck_photo_slide=-1; dtmulti=-1; webid_sync=1580726539077; TIARA=AdlyuJQdSYtZc5Qc_VmFK4_9HssEnjIimlMEMW7zm7tDmud7LimOtCcbT_Rabd_q33-pu5Q1RsL6s.UB-dQCKQ00
- 서버에 의해 Set-Cookie로 클라이언트에게 설정된 쿠키 정보

Host: www.daum.net
- 요청하는 호스트에 대한 호스트명 및 포트번호(필수)
- 전체 URL지정이 필요하다
- 이에 따라 동일 IP 주소를 갖는 단일 서버에 여러 사이트를 구축할 수 있다.

Referer: https://search.naver.com/search.naver?ie=UTF-8&query=%EB%8B%A4%EC%9D%8C&sm=chr_hty
- 바로 직전에 머물었던 웹 링크 주소

Sec-Fetch-Mode: navigate

Sec-Fetch-Site: cross-site

Sec-Fetch-User: ?1

Upgrade-Insecure-Requests: 1

User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.130 Safari/537.36
- 클라이언트 소프트웨어(브라우저, OS)명칭 및 버전 정보

## Response Headers
Cache-Control: no-cache, no-store, must-revalidate
- no-cache : 모든 캐시를 쓰기 전에 서버에 해당 캐시를 사용해도 되는지 확인한다.
- no-store : 아무것도 캐싱하지 않는다.
- must-revalidate : 만료된 캐시만 서버에 확인을 받도록 한다.
Connection: close

Content-Encoding: gzip
- 컨텐츠 압축된 방식
- 압축해서 보내면 브라우저가 알아서 해제해서 사용한다.
- 컨텐츠 용량이 줄어들기 때문에 압축을 권장한다.(요청 응답 속도 빨라진다, 데이터 소모량이 준다)

Content-Language: ko-KR
- 사용자의 언어

Content-Length: 47911
- 요청과 응답 메세지의 본문 크기를 바이트 단위로 표시해 준다. 메시지 크기에 따라 자동으로 만들어 진다.

Content-Type: text/html;charset=UTF-8
- 컨텐츠의 타입과 문자열 인코딩을 명시할 수 있다.
- Accept헤더, Accept-Charset 헤더와 대응된다.

Date: Mon, 03 Feb 2020 08:20:53 GMT
- HTTP 메시지가 만들어진 시각.

Expires: Sat, 01, Jan 1970 22:00:00 GMT
- 리소스가 지정된 일시까지 캐시로써 유효함을 나타낸다.
- 즉 응답 컨텐츠가 언제 만료되는지 나타낸다.
P3P: CP="ALL DSP COR MON LAW IVDi HIS IVAi DELi SAMi OUR LEG PHY UNI ONL DEM STA INT NAV PUR FIN OTC GOV"

Pragma: no-cache
- 모든 캐시를 쓰기 전에 서버에 해당 캐시를 사용해도 되는지 확인한다.

Vary: Accept-Encoding

X-Frame-Options: SAMEORIGIN

X-UA-Compatible: IE=10

X-UA-Device-Type: pc




## 4. 화면에 보여지기 시작하는 시간은 언제인가?

![](https://i.imgur.com/IVGGsbN.png)  


요즘 일반적인 스크린에서는 1초에 60번(60fps)의 그림을 그린다고 합니다. 이 때문에 브라우저가 60fps를 유지해야 웹 페이지가 버벅거림 없이 매끄럽게 보일 수 있고, 60fps를 유지하기 위해서는 최적화(Optimization)가 필요합니다. 이러한 최적화를 하기 위해 먼저 브라우저가 어떤 과정을 거쳐 화면에 나타나는지부터 알아보려고 합니다.  

브라우저가 하나의 화면을 나타내는 과정을 중요 렌더링 경로(Critical Rendering Path)라고 부릅니다.  
우리가 일상적으로 주소창에 url을 입력하고 엔터키를 누르면 브라우저는 해당 서버에 요청을 보내게 됩니다. 서버에서는 요청을 받고 응답으로 HTML 데이터를 보냅니다. 이 HTML 데이터를 실제 우리가 보는 화면으로 그리기까지의 과정이 바로 중요 렌더링 경로이며 이 과정의 각 단계가 최대한 효율적으로 이루어지도록 만드는 것을 최적화라고 부릅니다.  

![](https://i.imgur.com/mH9LkeH.png)  
  
중요 렌더링 경로의 과정에는 총 7가지의 과정이 있습니다.  

> 1. 서버에 응답으로 받은 HTML데이터를 파싱한다.
> 2. HTML을 파싱한 결과로 DOM Tree를 만든다. 
> 3. 파싱하는 중 CSS 파일 링크를 만나면 CSS 파일을 요청해서 받아온다.
> 4. CSS 파일을 읽어서 CSSOM(CSS Object Model)을 만든다.  
> 5. DOM Tree와 CSSOM이 모두 만들어지면 이 둘을 사용해 Render Tree를 만든다. 
> 6. Render Tree에 있는 각각의 노드들이 화면의 어디에 어떻게 위치할지를 계산하는 Layout 과정을 거쳐서 
> 7. 화면에 실제 픽셀을 Paint한다.


[브라우저에서 웹 페이지가 나타나는 과정](https://bearjin90.tistory.com/19)  



### comment
7번에서 픽셀이 Paint된 페이지 = 화면에 보이기 시작하는 시간이 되는 것 같다.





## 5. DOMContentLoaded라는 이벤트는 언제 발생하는가? load랑은 어떤 차이점이 있는가?

### DOMContentLoaded Event
DOMContentLoaded Event는 초기 HTML 도큐먼트가 로드되고 파스되면 스타일 시트, 이미지 및 다른 프레임이 로딩되기전에 실행됩니다. 이벤트의 진짜 타켓은 로드가 완료된 이벤트입니다. 이벤트는 Window 인터페이스에서 이벤트를 수진하여 캡처하고 버블링할 수 있습니다.  

동기식 javascript는 DOM을 파서하는 것을 정지합니다. 만약 유저가 페이지를 요청했을 때, DOM이 최대한 빠르게 파서되기를 원한다면 javascript를 비동기식으로 변환하거나 스타일시트를 수정하면 됩니다. 보통 스타일 시트는 병렬로 로드가 되면서 DOM 파싱 속도를 저하하고 주요 HTML 도큐먼트 트래픽을 스틸합니다.

HTML이 모두 로드되고 DOM트리가 완성되었지만 외부 리소스(img, style, script, etc )들은 아직 로드 되어지지 않을 때입니다.

DOM이 준비된 상태이기 때문에 DOM노드를 제어할 수 있습니다.

IE8이하에서 실행 되려면 추가코드가 필요합니다.

중복되더라도 차례대로 실행됩니다.

```js
window.addEventListener('DOMContentLoaded', function(){ //실행될 코드 })
```

### load Event
load Event는 스타일시트 이미지와 같이 의존성이 있는 리소스가 준비되면 실행됩니다. 이것은 DOMContentLoaded와 정 반대입니다.(브라우저에 모든 리소스들이 로드되었을 때)

image 사이즈와 같은 것들을 얻을 수 있습니다.

중복될 경우 마지막 선언이 실행됩니다.

```js
document.getElementById("myFrame").onload \= function() { //실행될 코드 }

window.addEventListener('load', function(){ //실행될 코드 });
```

#### 브라우저 로드 순서
DOMContentLoaded -> load

#### 대부분 load 보다 ready 또는 DOMContentLoaded 를 사용하는 이유는 무엇인가?

load는 모든 리소스를 로드해야 하기 때문에 DOMContentLoaded가 먼저 

발생된 후 발생합
니다. 대부분 모든 리소스를 기다릴 필요가 없는 경우가 많기에 빠른 실행을 위해서 입니다.


[DOMContentLoaded 와 Load 이벤트의 차이는 무엇인가요?](https://yngmanie.space/posts/dom-event)  


## 6. HTML 파일 응답 받은 이후부터, 모니터화면에 보이기까지의 과정을 설명하고, 이를 암기한다.

4번 문제와 동일.. 암기하기!!  


---
__+__ 추가(Lia가 잘 모르는 것~!)  
 
## DOM?

문서 객체 모델(The Document Object Model, 이하 DOM)은 HTML, XML 문서의 프로그래밍 언어가 interface 이다. DOM은 문서의 구조화된 표현(structured repersentation)을 제공하며 프로그래밍 언어가 DOM 구조에 접근할 수 있는 방법을 제공하여 그들이 문서 구조, 스타일, 내용 등을 변경할 수 있게 돕는다. DOM은 구조화된 nodes와 property와 method를 갖고 있는 objects로 문서를 표현한다. 이들은 웹 페이지를 스크립트 또는 프로그래밍 언어들에서 사용될 수 있게 연결시켜주는 역할을 한다.  


웹 페이지는 일종의 문서(document)다. 이 문서는 웹 브라우저를 통해 그 내용이 해석되어 웹 브라우저 화면에 나타나거나 HTML 소스 자체로 나타나기도 한다. 동일한 문서를 사용하여 이처럼 다른 형태로 나타날 수 있다는 점에 주목할 필요가 있다. DOM은 동일한 문서를 표현하고, 저장하고, 조작하는 방법을 제공한다. DOM은 웹 페이지의 객체 지향 표현이며, 자바스크립트와 같은 스트립팅 언어를 이용해 DOM을 수정할 수 있다.  

### DOM과 javascript

DOM은 프로그래밍 언어는 아니지만 DOM이 없다면 자바스크립트 언어는 웹 페이지 또는 XML 페이지 및 요소들과 관련된 모델이나 개념들에 대한 정보를 갖지 못하게 된다. 문서의 모든 element - 전체 문서, 헤드, 문서안의 table, table header, table cell 안의 text - 는 문서를 위한 document object model의 한 부분이다. 때문에 이러한 요소들은 DOM과 자바스크립틔와 같은 스크립팅 언어를 통해 접근하고 조작할 수 있는 것이다.  

초창기에는 자바스크립트와 DOM이 밀접하게 연결되어 있었지만, 나중에는 각각 분리되어 발전해왔다. 페이지 콘텐츠(the page content)는 DOM에 저장되고 자바스크립트를 통해 접근하거나 조작할 수 있다.  




[MDN: DOM이란?](https://developer.mozilla.org/ko/docs/Web/API/Document_Object_Model/%EC%86%8C%EA%B0%9C)  
