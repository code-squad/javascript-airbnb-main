# javascript-airbnb-main

### [미션] 웹사이트 분석
- 임의의 웹사이트를 선정한다.
- HTML안에 js,css의 위치는 어디에 위치했는가? 왜 그랬을까?
- 화면을 표시하기 위해 어떤 파일들이 다운로드 되는가?
- 특정 자원의 Request Headers 와 Response Headers의 내용을 분석.(네트워크 탭 활용)
- 화면에 보여지기 시작하는 시간은 언제인가?
- DOMContentLoaded라는 이벤트는 언제 발생하는가? load랑은 어떤 차이점이 있는가?
- HTML 파일 응답 받은 이후부터, 모니터화면에 보이기까지의 과정을 설명하고, 이를 암기한다.

https://gist.github.com/baekCode/00c7584b528c79641b7af71504c68f41

### [미션] airbnb - html 구현
index.html 
https://baekcode.github.io/codesquad-FE/day1/index.html

### [미션] airbnb - css 구현
index2.html 
https://baekcode.github.io/codesquad-FE/day1/index2.html

#### DOCTYPE 정의 및 선언(DTD)
HTML 문서에서 제일먼저 선언되어야 하며, **선언된 페이지의 HTML 버전이 무엇인지 웹브라우저에게 알려주는 역활**을 한다.
문서의 유형, 선언에 따라 문서내 요소와 속성을 처리하는 기준

- HTML5 : HTML5의 형태의 DOCTYPE선언 방식 <!DOCTYPE html>
- XHTML : XHTML 1.0 Strict / 1.0 Transitional / 1.0 Frameset
- HTML : 4.01 Strict / 4.01 Transitional / 4.01 Frameset

Strict : 엄격 모드, 웹표준을 엄격하게 지키는 버전
Transitional : 웹페이지와 호환성을 위해 쓰임
HTML5는 SGML을 기반으로 하기때문에 DTD를 참조할 필요가 없다.

```
HTML 5 
<!DOCTYPE html>


HTML 4.01 Strict (엄격모드)
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">


HTML 4.01 Transitional (호환모드)
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">


HTML 4.01 Frameset 
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN" "http://www.w3.org/TR/html4/frameset.dtd">


XHTML 1.0 Strict (엄격모드)
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">


XHTML 1.0 Transitional (호환모드)
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

국내에서 가장 많이 사용하는 DOCTYPE. 하위 브라우저 호환성 때문.


XHTML 1.0 Frameset
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Frameset//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-frameset.dtd">


XHTML 1.1
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">


```

