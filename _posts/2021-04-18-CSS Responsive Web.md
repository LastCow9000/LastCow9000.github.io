---
title: 'Responsive Web'
toc : true
toc_sticky: true
categories: [Frontend]
tags: [Web, CSS, Responsive Web]
---



## 반응형 웹(Responsive Web)

> 적응형 웹 vs 반응형 웹
>
> - 적응형 웹 : 접속 디바이스가 모바일 환경인지 PC 환경인지에 따라 다른 페이지를 보여줌
>
>    예시
>
>   - 모바일로 naver.com 접속 시 => m.naver.com
>   - pc로 접속 시 => naver.com
>
> 
>
> - 반응형 웹 : 동일한 웹페이지를 보여주지만 디바이스 화면 사이즈에 따라 다르게 보여줌



>480p 사이즈를 가진 이미지를 480p의 모니터에서 볼 때와 2k의 해상도를 가진 스마트폰에서 >볼 때를 가정하면 2k 해상도의 스마트폰에서 이미지가 매우 작게 보일 수 있음
>
>> - 이러한 문제점때문에 viewport가 생겨남







### viewport

---

웹 페이지의 표시 영역

- 스마트폰에서는 virtual viewport를 대부분 980px으로 설정함
- 이렇게 해도 스마트폰의 디스플레이 사이즈에 따라서 웹 페이지가 작게 보여 가독성이 떨어질 수 있음

> 이를 해결하기 위해 viewport meta tag를 사용

```html
<!--
아래와 같이 작성할 경우 480px에 맞게 웹페이지가 표시됨
해당 태그가 없을 경우 스마트폰의 default 설정인 980px에 맞게 웹페이지가 표시됨
-->
<meta name="viewport" content="width=480">

<!--
하지만 위와 같이 하드코딩할 경우 다양한 디스플레이 사이즈에 대응이 힘드므로 아래와 같이 사용하여 각 기기에 알맞는 너비값을 가져옴
-->
<mate name="viewport" content="device-width">
    
<!-- 보펴적으로 아래와 같이 사용 -->
<meta name="viewport" content="width=device-width, initial-scale=1.0" >
```

❗ device-width는 디스플레이 해상도의 너비가 아니고 [디스플레이 해상도 너비 / 픽셀 밀도] 로 계산됨





#### 주요 property

| property        | 설명                                       | 사용 예             |
| :-------------- | :----------------------------------------- | :------------------ |
| `width`         | viewport 너비[px] (default: 980px)         | width=device-width  |
| `height`        | viewport 높이[px]                          | width=device-height |
| `initial-scale` | viewport초기 배율(default: 1.0)            | initial-scale=1.0   |
| `user-scale`    | 확대 축소 가능 여부(default: yes)          | user-scale=no       |
| `maximum-scale` | viewport 최대 배율[0 ~ 10] (default: 5.0)  | maximum-scale=2.0   |
| `minimum-scale` | viewport 최소 배율[0 ~ 10] (default: 0.25) | minimum-scale=1.0   |







### 레이아웃과 미디어 쿼리

---

**레이아웃**

- 각 구성요소를 페이지 안에 효과적으로 배열하는 일을 의미함

- 시멘틱 태그를 사용하여 레이아웃을 잡는 것이 일반적임





**미디어 쿼리(`@media`)**

- 반응형 레이아웃에 사용되는 핵심 기술
- `@media`을 사용하여 미디어 별로 style을 지정하는 것을 의미



```css
@media (only|not) media-type and (property){}
```

- media-type : 보통 all 또는 screen
   - `all`
   - `print` (출력 미리보기 화면)
   - `screen` (브라우저 화면)
   - `speech` (음성)

- property

| property        | 설명                                                     |
| :-------------- | :------------------------------------------------------- |
| `width`         | viewport 너비[px]                                        |
| `height`        | viewport 높이[px]                                        |
| `device-width`  | 디바이스의 물리적 너비[px]                               |
| `device-height` | 디바이스의 물리적 높이[px]                               |
| `orientation`   | 디바이스 방향 (가로 방향: landscape, 세로방향: portrait) |

> 주로 `min-width`/`max-width`, `orientation`이 사용됨



- 논리 연산자를 사용하여 조건을 만들 수 있음
  - `and` : 모든 조건이 참일 때
  - `,` : 조건이 하나라도 참일 때
  - `not` : 조건이 거짓일 때
  - `only` : 생략하면 only가 default 미디어 쿼리를 지원하는 사용자만 미디어 쿼리 구문을 해석하라는 명령. 하지만 구형 브라우저 지원을 위해 선언하는 것이 좋음

  ```css
  /* 사용 예시 */
  
  /* 화면 너비가 768이상일 때 */
  @media (min-width: 768px){}
      
  /* 모든 화면에서 디바이스 방향이 가로가 아닐 때*/
  @media not all and (orientation: landscape){}
  
  /* 브라우저 화면이고 화면 너비가 1200이하일 때 */
  @media only screen and (max-width: 1200px){}
      
  /* 디바이스 방향이 세로이거나, 출력 화면이고 화면 너비가 1200이하일 때*/
  @media (orientation: portrait), print and (max-width: 1200px){}
  ```







### 미디어쿼리 적용한 반응형 웹 예시

```html
  <style>
    .header {
      background: salmon;
    }
    .nav {
      background: lightcoral;
    }
    .aside {
      background-color: cornflowerblue;
      float: right;
    }
    .section {
      background: lightblue;
    }
    .article {
      width: 45%;
      background-color: azure;
      float: left;
    }
    .footer {
      background: lightseagreen;
      clear: both;
    }
    @media only screen and (max-width: 768px) {
      .article {
        background: brown;
      }
      .aside {
        display: none;
      }
    }
  </style>
</head>
<body>
  <header class="header">header</header>
  <nav class="nav">nav</nav>
  <aside class="aside">aside</aside>
  <section class="section">
    <article class="article">article</article>
    <article class="article">article</article>
  </section>
  <footer class="footer">footer</footer>
</body>
```

> ![resposiveWeb](/assets/ImagesForPosts/2021-04-18-CSS Responsive Web/resposiveWeb.gif)

