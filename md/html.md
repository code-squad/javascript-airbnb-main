# HTML

## 배경지식
#HTML문서구조

daum.net 사이트에 접속해서 크롬 개발자 도구를 통해 HTML 소스 코드를 살펴보자!  

> **크롬 개발자 도구**
> 
> 공통: `오른쪽 마우스 -> 페이지 소스보기`  
> MAC OS: `option + cmd + i`  
> Window: `Ctrl + Shift + I` or `F12` 
 
### :book: :mag: 크롬 개발자 도구안을 살펴보자!! 


> 
> **네트워크**를 살펴보자! (참고)
> 
> ![](https://i.imgur.com/aftwcAw.png)  
> 
> 1, 2를 클릭하면 
> **Header, Preview, Response, Timing, Cookies**를 확인 가능하다.

> **`Header`**
> 
> ![](https://i.imgur.com/aHv8p4G.png)  
>![](https://i.imgur.com/NX7SiJJ.png)  

>
> **`Preview`**
>
> ![](https://i.imgur.com/Ie8RWyl.png)  
>

> **`Response`**
> 
> ![](https://i.imgur.com/PQRI9Fw.png)  
> .
> .
> style태그와 script태그(이미지 생략)
> .
> .
> ![](https://i.imgur.com/4eD15a3.png)  
>
>
> **`Timing`**
> 
> ![](https://i.imgur.com/ger2bza.png)  

> **`Cookies`**
> 
> ![](https://i.imgur.com/vxKG9tG.png)  


### element에서 태그들을 확인해보자!

HTML 코드를 들여다보면 다음과 같은 사실을 알 수 있다.  
- HTML 문서는 <html>이라는 태그로 시작하여 </html> 태그로 닫힌다.  
- HTML은 계층적이다.
  브라우저는 HTML 정보를 tree 구조로 보관하고 있다. (DOM Tree)
- HTML은 여러가지 태그를 사용하여 구조를 만든다.  
- body 태그는 화면에 보여지기 위한 정보이다.  

## HTML 기본 지식
- div(division) 태그만 사용해도 되는 가?
  의미없는 다른 태그를 감싸는 역할(그룹을 지어서 style을 반영하는 등에 필요)을 하기 위해서는 div만 쓸 수 있지만 의미에 맞는 태그들을 찾아서 사용하는 것이 중요하다.
  

  
- 화면의 배치(layouting)을 위한 태그가 있는가?
  아래 태그를 유심히 공부할 필요가 있다. Top-down 방식으로 HTML 구조를 만들 때 이를 이용한다.  
  
    > http://m.naver.com 에서 이 태그들이 실제 사용된 예를 들여다보자.  
  
  |태그| 사용 예|
  |:--:|:--|
  |header|  `<header>` 태그는 문서나 특정 섹션(section)의 헤더(header)를 정의할 때 사용합니다. 헤더(header)는 보통 도입부에 해당하는 콘텐츠나 네비게이션 링크의 집합 등과 같은 정보를 포함하게 됩니다.  `하나 이상의 제목 요소(h1 ~ h6)`, `로고(logo)나 아이콘(icon)`, `저자(author) 정보` |
  |section| `<section>` 태그는 HTML 문서에 포함된 독립적인 섹션(section)을 정의할 때 사용합니다. `<section>` 요소는 보통 제목 요소(h1~h6)를 자식 요소로 포함하고 있는 경우가 많습니다. |
  |nav| `<nav>` 태그는 다른 페이지 또는 현재 페이지의 다른 부분과 연결되는 네비게이션 링크(navigation links)들의 집합을 정의할 때 사용합니다. `<nav>` 요소를 사용하는 일반적인 예로는 메뉴, 목차, 인덱스 등이 있습니다. 글을 읽지 못하는 사용자를 위한 스크린 리더기와 같은 브라우저는 `<nav>` 요소를 사용하여 해당 콘텐츠의 초기 렌더링을 생략할지 여부를 결정합니다. |
  |footer|`<footer>` 태그는 문서나 특정 섹션(section)의 푸터(footer)를 정의할 때 사용합니다. 푸터(footer)는 보통 `<footer>` 요소가 포함되어 있는 문서나 섹션에 대한 아래와 같은 정보를 포함합니다. `저자(author) 정보`, `저작권 정보`, `연락처`, `사이트맵(sitemap)`, `페이지 맨 위로 되돌아갈 수 있는 Top 버튼`, `연관 페이지` 등.. 하나의 HTML 문서에는 여러 개의 `<footer>` 요소가 포함될 수 있습니다. |
  |aside| `<aside>` 태그는 페이지의 다른 콘텐츠들과 약간의 연관성을 가지고 있지만, 해당 콘텐츠들로부터 분리시킬 수 있는 콘텐츠로 구성된 페이지 영역을 정의할 때 사용합니다. |
  참고: http://tcpschool.com/html-tags/intro  

- 문서를 쓰듯이 의미에 맞는 태그(시멘틱 태그)를 찾아보자. (이미지, 제목, 문단, 표, 목록, 강조, 링크 등)
- HTML 태그에는 attribute를 추가할 수 있다. 아래 class, id, data, style 소겅들은 어떤 역할을 할까?
  |attribute|역할|
  |:--:|:--|
  |class||
  |id||
  |data||
  |style||

- HTML에서 주석은 어떻게 표현될까?


- 닫히지 않는 태그는 어떻게 브라우저에서 표현될까?

  |태그|내용|
  |:--:|:--|
  |br||
  |img||
  |meta||
  |link||
  |input||
  |hr||
  
  닫는 태그가거 없는 이유는?  
  태그 내부에 넣을 값이 없기 때문.
  
  **Self Closing**  
  어떤 문법에서는 닫는 태그가 없는 태그들을 닫는 태그와 규칙을 맞추기 위해 `<태그 />`처럼 사용하기도 합니다.   
  예) `<hr />` 처럼 작성하기도 한다.  
  [XHTML](https://ofcourse.kr/html-course/HTML5%EC%99%80-XHTML)에서는 이런 문법을 강제화 하였지만 HTML5에서는 닫아주지 않아도 된다.  
  
  참고: https://ofcourse.kr/html-course/%ED%83%9C%EA%B7%B8  


### CSS display의 block 속성 태그와 inline 속성 태그
- `block` 속성 태그는 그 크기를가지고 있어서 새로운 라인에서 시작한다.  
- `inline` 속성 태그는 화면 상에서 새로운 줄로 시작하지 않고 옆으로 배치된다.  
- `div`와 `span`이 대표적인 태그이다.  
- 이들을 사용해보면서 block과 inline 속성의 차이를 이해하자.  
  ``` html
  <div>나는 블록 속성을 가진 태그야!</div>
  ```
  ``` html
  <span>나는 인라인 속성을 가진 태그야!</span>
  ```
  
  화면에 어떻게 출력되는가?  
  사진을 첨부해보자!  
  
  inline을 쓰지않고 inline-block을 쓰는 이유는?  

### class와 id 구분해서 사용하기
HTML 태그에는 class와 id라는 속성을 사용할 수 있다.  

``` html
<div class="detail_item" id="left_item"> </div>
```

`class`는 css의 스타일을 만들고 이를 부르는 용도로 사용한다. `id`는 그 태그의 고유한 정보를 표현하는 것이다.   
`class`는 한 페이지에서 여러번 사용할 수 있는 반면, `id`는 한번만 사용하는 것이 좋다.  
`id`를 여러번 사용해도 페이지 렌더링을 하는데 문제가 발생하지는 않으나 유니크한 값으로 인식되서 페이지 내에 `id`로 지정한 노드를 찾으려고 할 때는 예상과 다른 결과를 얻을 수 있으니 주의해야 한다.  
보통 `id`는 레이아웃을 결정하는 바깥쪽 영역의 태그에 주로 부여한다.(이런 태그들은 페이지에서 unique 하다.)  
그 올바른 사용법을 좀 더 찾아보도록 하자.
```
저는 올바른 사용법을 적는 곳입니다.
```

학습 참고 사이트
1. https://www.edwith.org/htmlcss  
2. W3School.com 과 같은 사이트  