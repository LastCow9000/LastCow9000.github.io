---
title: 'CSS(Cascading Style Sheets)크기 단위와 Selector'
toc : true
toc_sticky: true
categories: [Frontend]
tags: [Web, CSS, 단위, Selector]
---



# 0. CSS 적용 전

**normalize.css**

> 브라우저마다 각기 다른 default 스타일이 지정되어 있기 때문에 이를 초기화해서 다양한 브라우저에서도 동일한 스타일로 표시되도록 하는 설정

- 기본 스타일은 남겨두고 브라우저별로 다른 스타일만 reset

- cdn을 통해 링크 : https://cdnjs.com/libraries/normalize

- 주로 공백을 제거하여 용량이 작은 normalize.min.css를 사용

- 예전에는 아래와 같이 사용했었음

  ```css
  /* reset.css */
  <style>
      * {
         margin: 0;
         padding: 0;
         border: none;
      }
  </style>
  ```





# 1. CSS 크기 단위

- `px` : 픽셀(화소) 단위, 해상도에 따라 상대적인 크기를 가진다.
- `%` : 상대 단위, 지정 사이즈에 기반하여 상대적인 비율의 크기를 가진다.
- `em` : 배수 단위, 지정 사이즈에 기반하여 배수로 계산된 크기를 가진다.
  - 중첩된 자식 요소에 em을 지정하면 모든 자식 요소 사이즈에 영향을 끼칠 수 있으므로 주의!
- `rem` : root em, 최상위 요소(html) 사이즈(보통 font-default = 16px)를 기준으로 한다.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <style>
    /* span태그의 em class*/
    span.em {
      font-size: 2em;
    }
    /* span태그의 rem class*/
    span.rem {
      font-size: 2rem;
    }
  </style>
</head>
<body>
  기본<br>
  <span class="em">
    em1  <span class="em">em2(중첩)</span>
  </span><br>
  <span class="rem">
    rem1  <span class="rem">rem2(중첩)</span>
  </span>
<body>
</html>
```

>![image-20210216195402136](/assets/ImagesForPosts/2021-02-16-CSS(Cascading Style Sheets)/image-20210216195402136.png)



> **em1 size = 32px** 
>
> ![image-20210216195546213](/assets/ImagesForPosts/2021-02-16-CSS(Cascading Style Sheets)/image-20210216195546213.png)



> **em2 size = 64px**
>
> ![image-20210216195624794](/assets/ImagesForPosts/2021-02-16-CSS(Cascading Style Sheets)/image-20210216195624794.png)



> **rem1,2 size=32px**
>
> ![image-20210216195801372](/assets/ImagesForPosts/2021-02-16-CSS(Cascading Style Sheets)/image-20210216195801372.png)





# 2. Viewport 단위 (반응형)

> viewport : 브라우저에서 웹 페이지가 표시되는 영역
>
> 반응형 : 기기 사이즈(pc, tablet, smartphone.. ect)에 맞춰 자동으로 크기가 변하는 것 

- `vw` : viewport 너비의 1/100 (1%)
- `vh` : 높이의 1%
- `vmin` : viewport 너비 or 높이 중 작은 것의 1%
- `vmax`  : 너비 or 높이 중 큰 것의 1%

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <style>
   .boxmodel1 {
     width: 100vw;
     height: 40vh;
     background-color: aqua;
   }

   .boxmodel2 {
     width: 50vw;
     height: 60vh;
     background-color: chocolate;
   }
  </style>
</head>
<body>
  <div class="boxmodel1">boxmodel1</div>
  <div class="boxmodel2">boxmodel2</div>
</body>
</html>
```

> ![image-20210216201047422](/assets/ImagesForPosts/2021-02-16-CSS(Cascading Style Sheets)/image-20210216201047422.png)



# 3. CSS Selector

- 전체 selector
  - `*`  : html 문서 전체를 선택
- tag selector
  - 해당 태그만 선택
- class selector
  - `.`
- id selector
  - `#`

```css
<style>
    /* 전체 selector */
    * {
        color: green;
    }

    /*tag selector*/
    h1 {
        color: blue;
    }

    /*class selector*/
    .btn {
        color: red;
    }

    /*id selector*/
	#address {
    	color: orange;
	}
</style>
```



**속성 selector**

- [속성] : attr 속성을 가지는 모든 태그

  ```css
  <style>
  	[want-go]{
      	color: blue;
  	}
  </style>
  ```

  

- [속성=값] : attr 속성이 해당값을 갖는 모든 태그, 대소문자 구분x

  ```html
    <style>
      [want-go] {
        color: crimson;
      }
    </style>
  </head>
  <body>
    <h5 want-go="yes">야너두?</h5>
    <h4 want-go="what">야너두?</h4>
    <h6 want-go="no">야너두?</h6>
    <h4 want-go="yes">야너두?</h4>
  </body>
  ```

  > ![image-20210216204816412](/assets/ImagesForPosts/2021-02-16-CSS(Cascading Style Sheets)/image-20210216204816412.png)

  

  ```html
    <style>
      [want-go] {
        color: crimson;
      }
      [want-go="no"] {
      color: rosybrown
      }
      [want-go="yes"] {
      color: yellowgreen
      }
    </style>
  </head>
  <body>
    <h5 want-go="yes">야너두?</h5>
    <h4 want-go="what">야너두?</h4>
    <h6 want-go="no">야너두?</h6>
    <h4 want-go="yes">야너두?</h4>
  </body>
  ```

  > ![image-20210216205016328](/assets/ImagesForPosts/2021-02-16-CSS(Cascading Style Sheets)/image-20210216205016328.png)



- [속성~=값] : attr 속성이 (공백으로 분리된) 해당값을 단어로 포함하는 모든 태그, 대소문자 구분x

  ```html
    <style>
      [want-go] {
        color: crimson;
      }
      [want-go~="yes"] {
      color: yellowgreen
      }
    </style>
  </head>
  <body>
    <h5 want-go="yesim">야너두?</h5>
    <h4 want-go="whatyes">야너두?</h4>
    <h6 want-go="no yes">야너두?</h6>
    <h4 want-go="yes im">야너두?</h4>
  ```

  > ![image-20210216205354997](/assets/ImagesForPosts/2021-02-16-CSS(Cascading Style Sheets)/image-20210216205354997.png)



- [속성|=값] : attr 속성이 `"값"` or `"값"으로 시작하면서 -(하이픈)문자가 곧바로 뒤따라 붙는` 모든 요소, 대소문자 구분x

  ```html
    <style>
      [want-go] {
        color: crimson;
      }
      [want-go|="yes"] {
      color: yellowgreen
      }
    </style>
  </head>
  <body>
    <h5 want-go="yes im">야너두?</h5>
    <h4 want-go="what-yes">야너두?</h4>
    <h6 want-go="yes">야너두?</h6>
    <h4 want-go="yes-im">야너두?</h4>
  </body>
  ```

  > ![image-20210216205821875](/assets/ImagesForPosts/2021-02-16-CSS(Cascading Style Sheets)/image-20210216205821875.png)



- [속성^=값] : attr속성이 `값`으로 시작하는 모든 태그, 대소문자 구분O

  ```html
    <style>
      [want-go] {
        color: crimson;
      }
      [want-go^="yes"] {
      color: yellowgreen
      }
    </style>
  </head>
  <body>
    <h5 want-go="yes im">야너두?</h5>
    <h4 want-go="what-yes">야너두?</h4>
    <h6 want-go="yes">야너두?</h6>
    <h4 want-go="yes-im">야너두?</h4>
  </body>
  ```

  >![image-20210216210536421](/assets/ImagesForPosts/2021-02-16-CSS(Cascading Style Sheets)/image-20210216210536421.png)

  

- [속성$=값] : attr속성이 `값`으로 끝나는 모든 태그, 대소문자 구분O

  ```html
    <style>
      [want-go] {
        color: crimson;
      }
       /* h4태그중 want-go 속성이 소문자 "yes"로 끝나는 태그 */
      h4[want-go$="yes"] {
      color: yellowgreen
      }
    </style>
  </head>
  <body>
    <h5 want-go="yes im">야너두?</h5>
    <h4 want-go="what-yes">야너두?</h4>
    <h6 want-go="yes">야너두?</h6>
    <h4 want-go="yes-im">야너두?</h4>
    <h4 want-go="whatyes">야너두?</h4>
    <h4 want-go="yes-im">야너두?</h4>
    <h4 want-go="what Yes">야너두?</h4> <!-- 대문자라x -->
    <h5 want-go="what yes">야너두?</h5>
  </body>
  ```

  > ![image-20210216211032341](/assets/ImagesForPosts/2021-02-16-CSS(Cascading Style Sheets)/image-20210216211032341.png)



- [속성*=값] : attr속성이 `"값"`을 포함하는 모든 태그, 대소문자 구분O

  ```html
    <style>
      [want-go] {
        color: crimson;
      }
      h4[want-go*="yes"] {
      color: yellowgreen
      }
    </style>
  </head>
  <body>
    <h5 want-go="yes im">야너두?</h5>
    <h4 want-go="what-yes">야너두?</h4>
    <h6 want-go="yes">야너두?</h6>
    <h4 want-go="yes-im">야너두?</h4>
    <h4 want-go="whatyes">야너두?</h4>
    <h4 want-go="yes-im">야너두?</h4>
    <h4 want-go="what Yes">야너두?</h4>
    <h5 want-go="what yes">야너두?</h5>
  </body>
  ```

  > ![image-20210216211201818](/assets/ImagesForPosts/2021-02-16-CSS(Cascading Style Sheets)/image-20210216211201818.png)



- 2부터정리