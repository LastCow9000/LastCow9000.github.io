---
title: 'HTML(Hypertext Markup Language)'
toc : true
toc_sticky: true
categories: [Frontend]
tags: [Html, Web]
---



> 시작하기전에

html과 css를 공부할 때 좋은 레퍼런스 사이트 : [MDN Web Docs (mozilla.org)](https://developer.mozilla.org/ko/)



## 1. HTML5 Boilerplate



**DOCTYPE : 문서형식 선언**

```html
<!DOCTYPE html>
```

최상단에 위치하는 HTML 문서임을 알려주는 태그

---



**HTML : 휴먼랭귀지**

```html
<html lang="en"></html>
```

HTML 문서의 시작을 알리고 문서의 언어를 설정한다.(en, ko)

---



**head : 문서 전체를 대표하거나 문서 전체에 필요한 데이터를 넣음**

```html
<head>
    <title>문서 제목</title>
    <meta/>
</head>
```

- head 태그 안에서 사용되는 태그

  - title : html 문서의 제목을 나타낸다.

  - meta : html 문서를 대표하는 정보를 표기한다.

    > 검색 시 나타나는 대략적인 정보
    >
  > ![image-20210216150552289](/assets/ImagesForPosts/html/image-20210216150552289.png)
  

---



**meta : SEO(검색엔진최적화)와 연관되어 있다.**

```html
<meta charset="utf-8">
<meta http-equiv="X-UA-Compatible" content="ie=edge">
<meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
<meta name="description" content="비스포크 페스티벌. 갖고 싶던 나만의 비스포크!">
<meta name="keywords" content="삼성, samsung">
<meta name="author" content="Lee재용">
```

> - charset : 문자 인코딩 설정
>- http-equiv : 호환성(**크로스 브라우징**)을 위함. IE가 작동해야될 렌더링 엔진을 선택>(`IE=edge` 는 항상 최신의 표준엔진을 사용)
> - name : 메타 정보 이름
> - viewport : 웹브라우저의 현재 창에서 문서를 볼 수 있는 화면
>  - width=device-width : 너비 = 기기의 화면 사이즈
>   - user-scalable=no : 웹페이지 확대 허용 = 아니오
>    - initial-scale=1.0 : 페이지 로딩 시 확대비율
>    - maximum-scale=1.0 : 최대 확대 비율
>    - minimum-scale=1.0 : 최소 확대 비율
>  - description : html 문서가 포함하는 콘텐츠의 내용 간략히 설명
>  - keywords : 검색 엔진이 참고할 검색 키워드
>  - author : 저자명



- 크로스 브라우징이란? : 다양한 웹브라우저상에서 동일한 사용자 경험을 위한 기술

---



**link : html 문서에 필요한 외부 데이터(css, icon 등)를 가져올 때 사용**

```html
<link rel="stylesheet" href="css/style.css">
<link rel="icon" href="favicon.png">
```

---



**script : javascript 코드를 문서 내에서 작성하거나 외부의 js파일을 가져올 때 사용**

```html
<script type="text/javascript">
	let a = 10;
</script>

<script src="js/main.js"></script>
```

페이지의 빠른 로딩을 위해 주로 <body> 마지막에 삽입(또는 <head>에 defer 옵션주고 삽입)

---





## 2. body : 문서의 내용



**h1~6, p**

```html
<h1>제목</h1> : 제목 태그
<h5>제목</h5>

<p>문단</p> : 문단 태그
```

>  제목 태그의 경우, 웹 브라우저 호환성을 위해 태그에 표현 서식이 들어 있는 경우는 모두 삭제하고 별도로 css style을 적용함

---



**div : division, 레이아웃을 나눌 때 사용**

```html
<div class="구역1">
	<div class="구역2">
        lorem
    </div>
</div>
```

---



**ol, ul, li : 리스트 태그**

```html
<!-- ordered list : 순서 있는 목록 -->
<ol>
    <li>사과</li>
    <li>바나나</li>
    <li>딸기</li>
</ol>

<!-- unordered list : 순서 없는 목록 -->
<ol>
    <li>사과</li>
    <li>바나나</li>
    <li>딸기</li>
</ol>
```

> ![image-20210216150734467](/assets/ImagesForPosts/html/image-20210216150734467.png)

---



**a : 하이퍼링크 태그**

```html
<a href="google.com" target="_self">google로 가기</a>
```

> `href` : 링크 url, url말고 전화번호와 이메일도 가능하다.
>
> - tel:number
> - mailto:address
>
> ```html
> <a href="tel:010-1111-2222">전화하기</a>
> <a href="mailto:email_sys@gmail.com">메일보내기</a>
> ```
>
> 
>
> `target` : 링크로 이동 방법
>
> - _self : 현재 브라우저에서 열기
> - _blank : 새로운 브라우저(새탭, 새창)에서 열기

---



**img**

```html
<img src="iu.jpg" alt="이지금">
```

> `src` : 이미지 파일 경로
>
> `alt` : 이미지 대체 텍스트 -> **웹 접근성**을 높이기 위해 사용하는 것이 좋다.

- 웹 접근성이란? : 시각 장애인을 위한 이미지 태그에 alt 속성 넣기, 청각 장애인을 위한 영상에 자막 넣기, 키보드로 웹페이지 인터페이스 접근 가능한 기능 등 환경적 제한이 있는 사용자(고령자 or 장애인)를 고려하여 웹페이짖를 제작하는 것.

---



**table**

```html
<table border="1">
    <thead>
        <th>
            제목 1열
        </th>
        <th>
            제목 2열
        </th>
    </thead>
    <tbody>
        <tr>
            <td>내용 1행1열</td>
            <td>내용 1행2열</td>
        </tr>
        <tr>
            <td>내용 2행1열</td>
            <td>내용 2행2열</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td>마지막행 1열</td>
            <td>마지막행 2열</td>
        </tr>
    </tfoot>
</table>
```

> ![image-20210216151847386](/assets/ImagesForPosts/html/image-20210216151847386.png)
>
> - `colspan`
>
> ```html
> <table border="1">
> <tr>
>  <td colspan="2">1행1열+2열</td>
> </tr>
> <tr>
>  <td>2행1열</td>
>  <td>2행2열</td>
> </tr>
> </table>
> ```
>
> ![image-20210216152618228](/assets/ImagesForPosts/html/image-20210216152618228.png)
>
> - rowspan
>
> ```html
> <table border="1">
>   <tr>
>     <td>1행1열</td>
>     <td rowspan="2">1+2행2열</td>
>   </tr>
>   <tr>
>     <td>2행1열</td>
>   </tr>
>   <tr>
>     <td>3행1열</td>
>     <td>3행2열</td>
>   </tr>
> </table>
> ```
>
> ![image-20210216152825820](/assets/ImagesForPosts/html/image-20210216152825820.png)

---



**form : 사용자 입력을 받음**

 ```html
<form action="register.do" method="post">
    아이디 : <input type="text" name="id">
	<button type="submit" name="btnSub">전송</button>
</form>
 ```

> ![image-20210216153935916](/assets/ImagesForPosts/html/image-20210216153935916.png)
>
> - `action` : 데이터를 보낼 url
> - `method` : http get방식, post방식
> - `target` : 링크로 이동 방법
>
>   - _self : 현재 브라우저에서 열기
>   - _blank : 새로운 브라우저(새탭, 새창)에서 열기

---



**form > input**

 ```html
이름<input type="text" autofocus autocomplete="on"><br>
체크박스<input type="checkbox"><br>
라디오버튼<input type="radio"><br>
비밀번호<input type="password"><br>
이메일<input type="email"><br>
색선택<input type="color"><br>
 ```

> ![image-20210216155411138](/assets/ImagesForPosts/html/image-20210216155411138.png)
>
> - 주로 사용하는 것들 : text, button, checkbox, radio, password, email, color ...ect
> - text의 주요 옵션들
>   - autofocus : 페이지 로딩 시 해당 입력창에 커서가 자동으로 놓임
>   - autocomplete : 자동완성기능, on/off
>   - maxlength : 입력값 최대 길이, 숫자
>   - minlength : 입력값 최소 길이, 숫자

---





## 3. Semantic Web

웹페이지 각 요소에 의미를 부여해서 단순 키워드 중심 검색을 넘어, '의미' 와 '관련성'을 기반으로 보다 진보된 검색 or 서비스가 가능토록 하는 시도

> `SEO`(검색엔진 최적화: Search Engine Optimization)같은 마케팅 도구를 사용하여 검색엔진이 본인의 웹사이트를 검색하기 알맞은 구조로 웹사이트를 조정하기도 하는데, 이것은 기본적으로 검색엔진이 웹사이트 정보를 어떻게 수집하는지 아는 것으로 부터 시작된다.
>
> 검색엔진은 로봇(Robot)이라는 프로그램을 이용해 매일 전세계의 웹사이트 정보를 수집한다.(이것을 `크롤링`이라 하며 검색엔진의 크롤러가 이를 수행한다.) 그리고 검색 사이트 이용자가 검색할 만한 키워드를 미리 예상하여 검색 키워드에 대응하는 `인덱스(색인)`을 만들어 둔다.(이것을 `인덱싱`이라 하며 검색엔진의 인덱서가 이를 수행한다.)
>
> 인덱스를 생성할 때 사용되는 정보는 검색 로봇이 수집한 정보인데 결국 웹사이트의 HTML 코드이다. 즉, 검색 엔진은 HTML 코드 만으로 그 의미를 인지하여야 하는데 이때 `시맨틱 요소`(Semantic element)를 해석하게 된다.
>
> [`출처`](https://poiemaweb.com/html5-semantic-web)

 

**주요 태그**

| 시맨틱 태그 | 설명                                             |
| :---------- | ------------------------------------------------ |
| header      | 헤더를 의미                                      |
| nav         | 내비게이션을 의미                                |
| aside       | 옆에 위치하는 부분을 의미                        |
| section     | 본문의 여러 내용(article)을 포함하는 부분을 의미 |
| article     | 본문의 주 내용이 들어가는 부분을 의미            |
| footer      | 하단부를 의미                                    |

![image-20210216161929261](/assets/ImagesForPosts/html/image-20210216161929261.png)

​					**잘 사용하면 검색엔진등이 각 부분에 대해 잘 이해 가능하다(SEO)**

```html
<body>
  <header></header>
  <nav></nav>
  <section>
    <article></article>
    <article></article>
  </section>
  <section>
    <article></article>
  </section>
  <aside></aside>
  <footer></footer>
</body>
```