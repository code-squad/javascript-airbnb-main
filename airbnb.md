# 웹사이트 분석

## 임의의 웹사이트를 선정한다.
- www.naver.com

## HTML안에 js,css의 위치는 어디에 위치했는가? 왜 그랬을까?
- css는 head 태그 안에 위치한다.
- js는 head 태그 및 body 태그 안에 위치한다. head 태그 속에서는 css 파일 뒤에 나타난다. body 태그 속에서는 body의 끝 부분에 위치한다.

**head에 삽입되는 경우**
- html태그가 읽히기전에 수행되어야하는 `<script>`태그들은 윗부분에 위치시켜야 한다. 또한 jQuery같이 여러 페이지에서 같이 동작해야 하는 것들도 `<head>`태그에 놓는게 좋다. 
[참고 자료](https://jundol.kr/8)
- 문서를 초기화하거나 설정하는 가벼운 스크립트들 
[참고 자료](https://webdir.tistory.com/514)
- HTML head 태그 속 자바스크립트 파일이 항상 오류를 일으키지 않는다. jQuery를 사용할 때, 보통 document ready 함수에 모든 코드를 넣는다. 
```=javascript
$("document").ready(function(){
// your code here
});
```
- 이 함수는 document가 준비되기 전까지 어떠한 코드도 실행하지 않는다. 이 방식은 전술한 에러를 방지할 수 있지만, HTML 로딩 시간을 느리게 만들 수 있다. 결국, 모든 HTML 뒤에 자바스크립트 파일을 놓는 게, 가장 좋은 방법이다. 
[참고 자료](https://faqs.skillcrush.com/article/176-where-should-js-script-tags-be-linked-in-html-documents)

**body에 삽입되는 경우**
- HTML은 위에서 부터 아래로 로딩(loading) 되기 때문에, 만약, 자바스크립트 파일이 head 부분에 있다면, HTML이 로딩되기 전 모든 자바스크립트 파일이 로딩된다. 이는 문제를 일으킬 수 있다. 
    1. 만약 자바스크립트 파일에서 HTML 요소를 접근하는 부분이 있다면, 접근할 HTML 요소가 없어서 자바스크립튼 코드가 유효하지 않게 보일 수 있고, 에러를 얻을 수 있다.
    2. 만약 자바스크립트가 길다면, 페이지가 늦게 로딩되는 모습을 눈으로 직접 볼 수 있다.  
- 만약 자바스크립트 링크를 HTML body의 마지막 부분에 놓는다면, HTML에게, 자바스크립트 파일이 로딩되기 전, 로딩할 수 있는 시간을 줄 수 있다. 이는 자바스크립트 파일이 HTML 보다 미리 로딩되어서 생기는 에러를 막을 수 있고, 웹페이지 반응 시간을 빠르게 할 수 있다. 
[참고 자료](https://faqs.skillcrush.com/article/176-where-should-js-script-tags-be-linked-in-html-documents)

## 화면을 표시하기 위해 어떤 파일들이 다운로드 되는가?
- html파일, css파일, js파일, 화면을 구성하기 위해 필요한 여러 요소들(png, jpeg, jpg등)

## 특정 자원의 Request Headers 와 Response Headers의 내용을 분석.(네트워크 탭 활용)

## 화면에 보여지기 시작하는 시간은 언제인가?
- 73.61ms </br>
![](https://i.imgur.com/dbOaerN.png)
[참고 자료](https://developers.google.com/web/tools/chrome-devtools/network/reference#timing-explanation)

## DOMContentLoaded라는 이벤트는 언제 발생하는가? load랑은 어떤 차이점이 있는가?

- DOMContentLoaded : HTML 이 모두 로드되고, DOM 트리가 완성되었지만, 외부 리소스(img etc) 가 아직 로드되어지지 않았을 때
- load : 브라우저에 모든 리소스(img, style, script, etc) 가 로드되었을 때
[참고 자료](https://mygumi.tistory.com/281)

- DOMContentLoaded 이벤트는 초기 HTML 문서를 완전히 불러오고 분석했을 때 발생합니다. 스타일 시트, 이미지, 하위 프레임의 로딩은 기다리지 않는다.
- DOMContentLoaded의 원본 대상은 다 불러온 Document입니다. 이 이벤트를 이벤트 캡쳐 혹은 이벤트 버블링 단계에서, Window Interface를 이용하여 Listen할 수 있다. 
- Load는 완전히 페이지가 로딩됐는지 여부를 감지하는 이벤트이다. DOMContentLoaded를 활용하는 코드가 더 적절한 곳에, Load를 쓰는 실수를 많이들 한다. 
[참고 자료](https://developer.mozilla.org/ko/docs/Web/Events/DOMContentLoaded)

## HTML 파일 응답 받은 이후부터, 모니터화면에 보이기까지의 과정을 설명하고, 이를 암기한다.
1. HTML 마크업을 처리하고 DOM 트리를 빌드한다.
2. CSS 마크업을 처리하고 CSSOM 트리를 빌드한다.
3. DOM 및 CSSOM을 결합하여 렌더링 트리를 형성한다.
4. 렌더링 트리에서 레이아웃을 실행하여 각 노드의 기하학적 형태를 계산한다.
5. 개별 노드를 화면에 페인트한다.

[참고 자료](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-tree-construction?hl=ko)

* DOM이란?
    - DOM (Document Object Model) 은 HTML 또는 XML document와 상호작용하고 표현하는 API이다. DOM은 browser에서 로드되며, 노드 트리(각 노드는 document의 부분을 나타냅니다)로 표현하는 document 모델이다(예, element, 문자열, 또는 코멘트).
    - DOM은 document의 모든 노드에 접근하고 상호작용할 수 있도록 브라우저에서 코드를 실행할 수 있게 해주는 이유로, Web에서 가장 많이 사용되는 API 중 하나이다. 노드들은 생성, 이동 및 변경될 수 있다. 이벤트 리스너를 노드에 추가해 주어진 이벤트가 발생할 때 트리거되게 할 수 있이다.
    - DOM은 기본적으로 정의되어 있지 않다—이는 브라우저가 JavaScript 구현을 시작했을 때 나타난다. 이 레거시 DOM을 DOM 0 이라고도 한다. 오늘날, WHATWG에서 DOM 리빙 표준을 관리한다.
[참고 자료](https://developer.mozilla.org/ko/docs/Glossary/DOM)

## 더 알아보기
[참고 자료](https://stackoverflow.com/questions/9979172/difference-between-node-object-and-element-object)

## 질문사항
- html 파일 속 css 파일은 다른 위치에 있다. 그런데 왜 구글 개발자 도구를 열어 preview를 보면, style이 입혀져 있을까?