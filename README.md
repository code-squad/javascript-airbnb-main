# [미션] 웹사이트 분석

## 웹사이트 : [네이버](https://www.naver.com), [다음](https://www.daum.net/)

## 💻 브라우저의 동작방식

1. HTML을 한 줄씩 읽는다.
2. HTML을 파싱한다.
3. `DOM 트리`를 만든다.
4. `DOM 트리`와 `CSS`의 `CSSOM 트리`를 결합해 `Render 트리`를 만든다.
5. 브라우저에 `Display` 된다.

![Browser Rendering](https://i.imgur.com/qxnL2Kj.png)

> HTML을 파싱하고,`DOM 트리`를 만들기 전에 스크립트가 실행되면, 화면에 표시되는 시간이 지연되거나 존재하지 않는 DOM 조작을 하려고 해서 에러가 발생할 수 있다. 그래서 **보통 JavaScript파일은 `Body`에서 HTML파일이 끝나는 지점에 삽입**한다.

## 1️⃣ HTML안에 js,css의 위치는 어디에 위치했는가? 왜 그랬을까?

### Header

- `CSS`
- `Javascript`

### body 마지막

- `Javascript`

## ➡️ 그렇다면 Header에 Javascript가 오는 이유는 무엇일까?

- 가독성과 실행순서, 의존성들을 확인하기 수월하기 때문이다.
- 그래서 Header에는 문서를 초기화하거나 설정하는 가벼운 스크립트들이 자주 사용된다.

## 2️⃣ 화면을 표시하기 위해 어떤 파일들이 다운로드 되는가?

![source](https://i.imgur.com/M27jOkA.png)

### `XHR` : XMLHttpRequest

- 전체 페이지의 새로고침없이도 URL 로부터 데이터를 받아올 수 있는 서버와 상호작용하는 객체

### `WS` : Windows Script

- JScript 및 VBScript 루틴을 통합할 수 있고, XML 요소를 포함할 수 있는 Windows용 실행 스크립트

### `Manifest`

- 컴퓨팅에서 집합의 일부 또는 논리정연한 단위인 파일들의 그룹을 위한 메타데이터를 포함하는 파일

### 많이 다운받는 파일

- `css` 파일
- `js` 파일
- `img` 파일
- `webfont` 파일

## 3️⃣ 특정 자원의 Request Headers 와 Response Headers의 내용을 분석.(네트워크 탭 활용)

### _GET Resource : main_v200116.css 파일_

### `General header` : 요청과 응답 모두에 적용되지만 바디에서 최종적으로 전송되는 데이터와는 관련이 없는 헤더.

![General](https://i.imgur.com/RQtDo6M.png)

웹브라우저(클라이언트)가 서버에게 리퀘스트 URL로 식별된 리소스를 가져올 수 있도록 요구함 `GET`, 그리고 성공적으로 가져와 `200`을 Status Code로 가지고 있음

|      표현       |                                                       뜻                                                        |
| :-------------: | :-------------------------------------------------------------------------------------------------------------: |
|   Request URL   |                                    데이터를 받아오기 위해 요청을 보내는 주소                                    |
| Request Method  |                                      Request Header에 붙여야 하는 명령어.                                       |
|   Status Code   |                                        Response Header에 붙는 상태 코드                                         |
| Remote Address  | TCP/IP 접속에서 생성되는 접속자의 IP 주소 값.<br>원격의 Proxy 서버를 이용하는 경우 Proxy 서버의 IP로 바뀌게 됨. |
|   Remote Host   |                             클라이언트가 사용중인 IP 주소의 `Reverse DNS lookup` 값                             |
| Referrer Policy |                   요청에 포함되어야하는 Referer 정보 (Referer 헤더를 통해 전송)의 양을 제어함                   |

#### Referrer Policy - origin

> same-origin, cross-origin 요청 모두 수행할때 ASCII직렬화 정보를 보낸다.

![example of origin](https://i.imgur.com/j332dFi.png)

#### Request header

> 페치될 리소스나 클라이언트 자체에 대한 자세한 정보를 포함하는 헤더.

![Request Headers](https://i.imgur.com/C06dAir.png)

#### Response header

> 위치 또는 서버 자체에 대한 정보(이름, 버전 등)와 같이 응답에 대한 부가적인 정보를 갖는 헤더.

![Response Headers](https://i.imgur.com/pEbw8sW.png)

#### Entity header

> 컨텐츠 길이나 MIME 타입과 같이 엔티티 바디에 대한 자세한 정보를 포함하는 헤더.

## 화면에 보여지기 시작하는 시간은 언제인가?

![](https://i.imgur.com/ZcavRJN.png)
_Lighthouse - 사이트 로드 시간 측정해 주는 확장 프로그램_

![Lighthouse](https://i.imgur.com/tkhdGMw.png)

### LightHouse

![Google Developer tools - Performance](https://i.imgur.com/CzaVBAz.png)
_Google Developer tools - Performance_
\_\_

`First Paint` entry contains a DOMHighResTimeStamp reporting the time when the browser first rendered after navigation. This excludes the default background paint, but includes non-default background paint and the enclosing box of an iframe. This is the first key moment developers care about in page load – when the browser has started to render the page.

`First Contentful Paint` entry contains a DOMHighResTimeStamp reporting the time when the browser first rendered any text, image (including background images), non-white canvas or SVG. This excludes any content of iframes, but includes text with pending webfonts. This is the first time users could start consuming page content.

처음으로 텍스트나 이미지가 paint된 시간 : `0.9s`

## DOMContentLoaded라는 이벤트는 언제 발생하는가? load랑은 어떤 차이점이 있는가?

### DOMContentLoaded

HTML 이 모두 로드되고, DOM 트리가 완성되었지만, `외부 리소스(img etc)`가 아직 로드되어지지 않았을 때

### load

브라우저에 `모든 리소스(img, style, script, etc)`가 로드되었을 때

> DOMContentLoaded 가 load 보다 빨리 발생

## HTML 파일 응답 받은 이후부터, 모니터화면에 보이기까지의 과정을 설명하고, 이를 암기한다.

브라우저의 동작방식

## 참고

- [자바스크립트 삽입방식과 위치](https://webdir.tistory.com/514)
- [MDN](https://developer.mozilla.org/ko/docs/Web/API/XMLHttpRequest)
- [WEBDIR](https://webdir.tistory.com/514)
- [DOMContentLoaded, load, unload](https://mygumi.tistory.com/281)
- [MDN HTTP 헤더](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers)
- [W3C - Referrer Policy](https://www.w3.org/TR/referrer-policy/)
- [Lighthouse - FCP](https://web.dev/first-contentful-paint/?utm_source=lighthouse&utm_medium=lr)
- [Google Developers](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-tree-construction?hl=ko)
