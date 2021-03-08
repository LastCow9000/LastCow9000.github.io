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

##### 전체 selector

- `*`  : html 문서 전체를 선택

##### tag selector

- 해당 태그만 선택

##### class selector

- `.`

##### id selector

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



##### 속성 selector

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



##### CSS Selector 조합

- 클래스, 아이디, 태그 selector를 조합해서 복합적으로 사용 가능

  ```html
    <style>
      /* 특정 클래스의 아이디 태그를 선택시 아래와 같이 select한다 */
      h1.last.cow#meh {
        color: red;
      }
    </style>
  </head>
  <body>
    <h1 class="last cow" id="meh">hahaha</h1>
  </body>
  ```



##### 복합 Selector

- 후손 선택자 (Descendant Selector) : `space bar`

  - 부모 tag 안에 있는 모든 하위 tag : 하위 요소, 후손 요소

  - 부모 tag 안에 있는 **모든 tag 중에 특정 tag**를 선택

    ```html
      <style>
        h1 {
          color: red;
        }
        div span {
          color: blue;
        }
      </style>
    </head>
    <body>
      <div>
        <h1>hahaha</h1>
        <p>영어가 안되면 야너두스쿨</p>
        <p><span>서경석</span>야 너두?</p>
      </div>
    </body>
    ```

    > ![image-20210220031803525](/assets/ImagesForPosts/2021-02-16-CSS(Cascading Style Sheets)크기 단위와 Selector/image-20210220031803525.png)

  

- 자식 선택자 (Child Selector) : `>`

  - 부모 tag 안에 있는 **바로 다음 레벨의 tag 중에 특정 tag**를 선택

  ```html
    <style>
      h1 {
        color: red;
      }
      div > p {
        color: blue;
      }
    </style>
  </head>
  <body>
    <div>
      <h1>hahaha</h1>
      <h2> <!-- div 바로 다음이 아니라 h2 다음 레벨이라 적용x -->
        <p>영어가 안되면 야너두스쿨</p>
      </h2>
      <p><span>서경석</span>야 너두?</p>
    </div>
  </body>
  ```

  > ![image-20210220032140091](/assets/ImagesForPosts/2021-02-16-CSS(Cascading Style Sheets)크기 단위와 Selector/image-20210220032140091.png)

- 인접 형제 선택자(Adjacent Sibling Selector) : `+`

  - tag1과 동일 레벨에 위치하고 tag1의 바로 뒤에 위치하는 tag2를 선택

    -> tag1과 tag2 사이에 다른 tag 위치시 선택 불가
   ```html
    <style>
      h1 + h2 {
        color: red;
      }
      h1 + p {
        color: blue;
      }	/* h1과 p 사이에 h2가 있으므로 적용x */
    </style>
  </head>
  <body>
    <div>
      <h1>hahaha</h1>
      <h2>
        <p>영어가 안되면 야너두스쿨</p>
      </h2>
      <p><span>서경석</span>야 너두?</p>
    </div>
  </body>  
   ```

  > ![image-20210220032852730](/assets/ImagesForPosts/2021-02-16-CSS(Cascading Style Sheets)크기 단위와 Selector/image-20210220032852730.png)

  

- 일반 형제 선택자(General Sibling Selector) : `~`

  - tag1과 동일 레벨에 위치하고 tag1의 뒤에 위치하는 tag2를 선택

    -> tag1과 tag2 사이에 다른 tag 위치해도 선택 가능

  ```html
    <style>
      h1 + h2 {
        color: red;
      }
      h1 ~ p {
        color: blue;
      }
    </style>
  </head>
  <body>
    <div>
      <h1>hahaha</h1>
      <h2>
        <p>영어가 안되면 야너두스쿨</p>
      </h2>
      <p><span>서경석</span>야 너두?</p>
    </div>
  </body>
  ```

  > ![image-20210220033152005](/assets/ImagesForPosts/2021-02-16-CSS(Cascading Style Sheets)크기 단위와 Selector/image-20210220033152005.png)



##### 가상 클래스 Selector(Pseudo-Class Selector)

- 가상 클래스는 요소에 특정 이벤트 발생 시를 선택하는 문법
- ex) p 태그 요소에 마우스가 올라갔을 때

> 가상 클래스의 종류
>
> - `link` : 방문하지 않은 링크가 적용된 요소
> - `visited` : 방문한 링크가 적용된 요소
> - `hover` : 특정 요소에 마우스가 올라간 상태
> - `active` : 링크 요소를 클릭한 상태(마우스로 누르고 있는 상태)
> - `focus` : 특정 요소에 포커스가 있는 상태



  **가상 셀렉터는 가상 요소 셀렉터 이외에는 한개의 `:` 을 사용한다**

```html
  <style>
    a:link {
      color: pink; 
    }
    a:visited {
      color: tomato 
    }
    a:hover {
      color: blue 
    }
    a:active {
      color:greenyellow; 
    }
    input:focus {
      color : blueviolet;
    }
  </style>
</head>
<body>
  <div>
    <h1>hahaha</h1>
    <a href="http://www.google.com">구글로이동</a>
    <form action="naver.com">
      텍스트<input type="text"><br>
      <input type="submit" value="전송">
    </form>
    </div>
</body>
```

> 1. 초기화면
>
> ![image-20210220034753706](/assets/ImagesForPosts/2021-02-16-CSS(Cascading Style Sheets)크기 단위와 Selector/image-20210220034753706.png)
>
> 
>
> 2. 구글로 이동에 마우스 올림
>
> ![image-20210220034848627](/assets/ImagesForPosts/2021-02-16-CSS(Cascading Style Sheets)크기 단위와 Selector/image-20210220034848627.png)
>
> 
>
> 3. 구글로 이동을 클릭해서 방문한 후
>
>    ![image-20210220035131072](/assets/ImagesForPosts/2021-02-16-CSS(Cascading Style Sheets)크기 단위와 Selector/image-20210220035131072.png)
>
>    
>
> 4. 인풋 상자에 포커스 있을 시
>
>    ![image-20210220035341253](/assets/ImagesForPosts/2021-02-16-CSS(Cascading Style Sheets)크기 단위와 Selector/image-20210220035341253.png)
>
>    
>
> 5. 인풋 상자에 포커스 없을 시
>
> ![image-20210220035410525](/assets/ImagesForPosts/2021-02-16-CSS(Cascading Style Sheets)크기 단위와 Selector/image-20210220035410525.png)
>
> 
>
> 6. 구글로 이동을 클릭하고 있을 시
>
> ![image-20210220035459180](/assets/ImagesForPosts/2021-02-16-CSS(Cascading Style Sheets)크기 단위와 Selector/image-20210220035459180.png)



- UI 요소 상태 Selector(UI Element States Pseudo-Class)

  - `enabled` : UI 선택자가 사용 가능한 상태

  - `disabled` : UI 선택자가 사용 불가능한 상태

  - `checked` : UI 선택자가 체크된 상태

  - `indeterminate` : UI 선택자 상태가 결정되지 않은 상태

    ex) 체크박스에 체크가 안되었거나, 라디오 버튼들이 하나도 체크되지 않은 상태

  ```html
    <style>
      input[type="radio"]:indeterminate + span {
        color: red; 
      }
      input[type="radio"]:checked + span {
        color: green 
      }
      input[type="checkbox"]:enabled + span {
        color: blue 
      }
      input[type="checkbox"]:disabled + span {
        color: violet; 
      }
    </style>
  </head>
  <body>
    <div>
      <h1>hahaha</h1>
      <form action="naver.com">
        <input type="radio" name="rad" value="1111"><span>1111</span><br>
        <input type="radio" name="rad" value="2222"><span>2222</span><br>
        <input type="checkbox" name="check" value="3333"><span>3333</span><br>
        <input type="checkbox" name="check" value="4444" disabled><span>4444</span><br>
        <input type="text" name="tex">
        <input type="submit" value="제출">
      </form>
      </div>
  </body>
  ```

  > 1. 아무것도 선택하지 않은 초기 상태
  >
  >    ![image-20210220041206322](/assets/ImagesForPosts/2021-02-16-CSS(Cascading Style Sheets)크기 단위와 Selector/image-20210220041206322.png)
  >
  >    
  >
  > 2. 1111 체크
  >
  >    ![image-20210220041228536](/assets/ImagesForPosts/2021-02-16-CSS(Cascading Style Sheets)크기 단위와 Selector/image-20210220041228536.png)
  >
  >    
  >
  > 3. 2222 체크
  >
  > ![image-20210220041245044](/assets/ImagesForPosts/2021-02-16-CSS(Cascading Style Sheets)크기 단위와 Selector/image-20210220041245044.png)

  

- 구조 가상 클래스 선택자 (Structured Pseudo-Class)

  - `first-child` : 부모의 첫 번째 자식인 요소 선택

  - `last-child` : 부모의 마지막 자식인 요소 선택

  - `nth-child(n)` : 부모의 첫 번째 자식 요소부터 시작해서 n번째 요소 선택(인덱스 시작은 1부터)

    > 2n-1을 넣어 홀수만 고를 수 있다. (짝수 : 2n)

  - `nth-last-child(n)` : 부모의 마지막 자식 요소부터 뒤에서 시작해서 n번째 요소 선택(인덱스 시작은 1부터)

    > 2n-1을 넣어 홀수만 고를 수 있다. (짝수 : 2n)

  ```html
      <style>
        p:first-child { //p태그 이면서 첫번째 자식인 것
          color: red;
        }
        p:last-child {
          color: green;
        }
        p:nth-child(2) {
          color: blue;
        }
        p:nth-last-child(3) {
          color: violet;
        }
      </style>
    </head>
    <body>
      <div>
        <h2>테스팅</h2>
        <div>
          <p>발라모굴리스</p>
          <p><span>아이어를</span> 위하여!</p>
          <p>라니스터는 항상 빚을 갚는다</p>
          <p>Winter is Coming</p>
          <p>오늘 헤어졌어요..</p>
        </div>
        <div> <!-- 새로운 div로 부모가 바뀜-->
          <h2>first-child는 어려워</h2> <!-- 첫번째 자식이지만 p태그가 아님-->
          <p>아둔 토리다스</p>
          <p><span>나의 검은</span>당신의 것이오</p>
          <p>구른다</p>
          <p>당신의 뜻대로 따르겠소</p>
          <h2>last-child가 먹히는가?</h2>
        </div>
      </div>
  ```

  > ![image-20210309030847758](/assets/ImagesForPosts/2021-02-16-CSS(Cascading Style Sheets)크기 단위와 Selector/image-20210309030847758.png)

  

  ```html
      <style>
        p:nth-child(2n-1) { // 홀수
          color: blue;
        }
        p:nth-last-child(2n-1) { // 홀수
          color: violet;
        }
      </style>
    </head>
    <body>
      <div>
        <h2>테스팅</h2>
        <div>
          <p>css셀렉터..</p>
          <p>발라모굴리스</p>
          <p><span>아이어를</span> 위하여!</p>
          <p>라니스터는 항상 빚을 갚는다</p>
          <p>Winter is Coming</p>
          <p>오늘 헤어졌어요..</p>
        </div>
      <div>
  ```

  > ![image-20210309031946936](/assets/ImagesForPosts/2021-02-16-CSS(Cascading Style Sheets)크기 단위와 Selector/image-20210309031946936.png)

  

  

  - `first-of-type` : '선택자에 해당하는 요소의 부모 요소의 자식 요소 중에서 선택자에 해당하는 요소만 뽑아'(이하 a) 첫 번째 요소 선택
  - `last-of-type` : 'a' 이 중 마지막 요소 선택
  - `nth-of-type(n)` : 'a' 앞에서부터 n번째 요소 선택
  - `nth-last-of-type(n)` : 'a' 뒤에서부터 n번째 요소 선택

  > 위에서 첫 번째 자식이지만 p태그 아닌 h2 태그여서 선택이 되지 않은 경우가 있다.
  >
  > 이럴 때 사용하는 것 

  ```html
      <style>
        p:first-of-type {
          color: red;
        }
        p:last-of-type {
          color: green;
        }
        p:nth-of-type(3) {
          color: blue;
        }
        p:nth-last-of-type(3) {
          color: violet;
        }
      </style>
    </head>
    <body>
      <div>
        <h2>테스팅</h2>
        <div>
          <p>css셀렉터..</p>
          <p>발라모굴리스</p>
          <p><span>아이어를</span> 위하여!</p>
          <p>라니스터는 항상 빚을 갚는다</p>
          <p>Winter is Coming</p>
          <p>오늘 헤어졌어요..</p>
        </div>
        <div>
          <h2>first-child는 어려워</h2>
          <p>아둔 토리다스</p>	<!--p태그중 첫 번째-->
          <p><span>나의 검은</span>당신의 것이오</p>
          <p>구른다</p>
          <p>당신의 뜻대로 따르겠소</p> <!--p태그중 마지막-->
          <h2>last-child가 먹히는가?</h2>
        </div>
      </div>
  ```

  > ![image-20210309033322284](/assets/ImagesForPosts/2021-02-16-CSS(Cascading Style Sheets)크기 단위와 Selector/image-20210309033322284.png)

  

  

- 부정 선택자 (Negation Pseudo-Class)

  - `not(선택자)` : 선택자에 해당하지 않는 모든 요소 선택

  ```html
      <style>
        p:not(.masterYee) {
          color: red;
        }
      </style>
    </head>
    <body>
      <div>
        <h2>테스팅</h2>
        <div>
          <p>css셀렉터..</p>
          <p class="masterYee">발라모굴리스</p>
          <p><span>아이어를</span> 위하여!</p>
          <p>라니스터는 항상 빚을 갚는다</p>
          <p>Winter is Coming</p>
          <p class="masterYee">오늘 헤어졌어요..</p>
        </div>
        <div>
          <h2 class="masterYee">first-child는 어려워</h2>
          <p>아둔 토리다스</p>
          <p class="masterYee"><span>나의 검은</span>당신의 것이오</p>
          <p>구른다</p>
          <p>당신의 뜻대로 따르겠소</p>
          <h2>last-child가 먹히는가?</h2>
        </div>
      </div>
  ```
  
  > ![image-20210309034241067](/assets/ImagesForPosts/2021-02-16-CSS(Cascading Style Sheets)크기 단위와 Selector/image-20210309034241067.png)
  
  
  
- 정합성 체크 선택자(Validity Pseudo-Class)

  - `valid(선택자)` : 정합성이 검증된 input 또는 form 요소 선택
  - `invalid(선택자)` : 정합성 검증이 실패한 input 또는 form 요소 선택

  

  **input 태그 유효성 검사와 정합성 체크 선택자**

  1. required 속성

     - input 태그로 생성된 입력창에 반드시 데이터를 입력해야 함.(데이터가 입력되어야 정합성이 검증됐다고 판단함)

     ```html
         <style>
           input[type='text']:invalid {
             background-color: pink;
           }
           input[type='text']:valid {
             background-color: lawngreen;
           }
         </style>
       </head>
       <body>
         <h2>정합성 선택자</h2>
         <form>
           <input type="text" required />
           <input type="submit" />
         </form>
     ```

     > 1. 입력x
     >
     > ![image-20210309035447507](/assets/ImagesForPosts/2021-02-16-CSS(Cascading Style Sheets)크기 단위와 Selector/image-20210309035447507.png)
     >
     > 2. 입력o
     >
     > ![image-20210309035529235](/assets/ImagesForPosts/2021-02-16-CSS(Cascading Style Sheets)크기 단위와 Selector/image-20210309035529235.png)

  

  2. pattern 속성

     - input 태그 입력창에 넣은 데이터가 데이터 포맷에 맞으면 정합성이 검증됐다고 판단함
     - pattern 값은 정규 표현식(Regex) [`사용 예시 참조 링크`](http://www.w3bai.com/ko/tags/att_input_pattern.html)

     ```html
         <style>
           input[type='text']:invalid {
             background-color: pink;
           }
           input[type='text']:valid {
             background-color: lawngreen;
           }
         </style>
       </head>
       <body>
         <h2>정합성 선택자</h2>
         <form>
           <!--0~9의 숫자로 6글자 체크-->
           <input type="text" pattern="[0-9]{6}" /> 
           <input type="submit" />
         </form>
     ```

     > 1. 문자+숫자 6글자
     >
     > ![image-20210309040140595](/assets/ImagesForPosts/2021-02-16-CSS(Cascading Style Sheets)크기 단위와 Selector/image-20210309040140595.png)
     >
     > 2. 숫자 7글자
     >
     > ![image-20210309040217424](/assets/ImagesForPosts/2021-02-16-CSS(Cascading Style Sheets)크기 단위와 Selector/image-20210309040217424.png)
     >
     > 3. 숫자 6글자
     >
     > ![image-20210309040227872](/assets/ImagesForPosts/2021-02-16-CSS(Cascading Style Sheets)크기 단위와 Selector/image-20210309040227872.png)





##### 가상 요소 선택자(Pseudo-Element Selector)

- 선택한 요소 안의 특정 부분을 선택(ex: 특정 요소의 첫글자 등)
- `first-letter` : 요소의 첫 글자 선택
- `first-line` : 요소의 첫 라인 선택 (**block 요소에만 적용 가능**)
- `after` : 요소의 뒤에 위치하는 공간 선택, content property와 함께 사용
- `before` : 요소의 앞에 위치하는 공간 선택, content property와 함께 사용
- `selection` : 요소에서 드래그한 부분 선택
- **다른 가상 선택자와 다르게 두개의 콜론(`::`)을 사용함**

```html
    <style>
      h2::before {
        content: '비포!';
        color: blue;
      }
      h2::after {
        content: '앱터!';
        color: darkgreen;
      }
      p::first-letter {
        color: lightcoral;
        font-size: 3em;
      }
      p::first-line {
        color: lightskyblue;
        font-size: 2em;
      }
      p::selection {
        background-color: lightseagreen;
      }
    </style>
  </head>
  <body>
    <h2>로렘을 불러보자 에치투</h2>
    <p>
      Lorem, ipsum dolor sit amet consectetur adipisicing elit.
      Unde eum, iure dolores eius, aspernatur repellat debitis 
      reiciendis natus eveniet tenetur quae quo vitae nihil! Nam, 
      quibusdam. Iureipsanihil inventore.
    </p>
  </body>
```

> ![image-20210309042243406](/assets/ImagesForPosts/2021-02-16-CSS(Cascading Style Sheets)크기 단위와 Selector/image-20210309042243406.png)
>
> - 두 번째 문장에 드래그를 해보았다.



