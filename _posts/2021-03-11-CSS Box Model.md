---
title: 'CSS Box Model'
toc : true
toc_sticky: true
categories: [Frontend]
tags: [Web, CSS, Box]
---

## Box Model

> 웹 디자인은 contents를 담을 box model을 정의하고 CSS 속성을 통해 스타일(배경, 폰트와 텍스트 등)과 위치 및 정렬을 지정하는 것.

- 모든 HTML 요소는 box 형태로 되어있다.
- 하나의 박스는 네 부분(영역)으로 이루어 진다.
  - content / padding / border / margin

![css-box-model-box-sizing](/assets/ImagesForPosts/2021-03-11-CSS Box Model/css-box-model-box-sizing.png)

1. Content
   - 글이나 이미지, 비디오 등 요소의 실제 내용
   - width, height property를 가짐
2. Padding (안쪽 여백)
   - Border(테두리) 안쪽의 내부 여백
   - 배경색, 이미지 지정 가능(기본색은 투명)
3. Border

   - 테두리 영역, 두께 지정 가능
4. Margin (바깥쪽 여백)
   - 테두리 바깥의 외부 여백
   - 배경색 지정 불가

```html
  <style>
      div {
        background-color: lightcoral;
        width: 200px;
        padding: 20px;
        border: 10px solid lightgreen;
        margin: 20px;
      }
  </style>
</head>
<body>
  <div>CSS BOX MODEL TEST 입니다. CSS BOX MODEL TEST 입니다.</div>
</body>
```

> ![image-20210310214534246](/assets/ImagesForPosts/2021-03-11-CSS Box Model/image-20210310214534246.png)





**※ 마진 상쇄**

- block의 top 및 bottom margin이 때로는 (결합되는 마진 중 크기가) 가장 큰 한 마진으로 결합(combine, 상쇄(collapsed))된다.



### 주요 property

---

#### box-sizing, width / height property

- `box-sizing` property는 default로 `content-box`가 지정되어 있다.
  - 이 경우 `width` / `height`는 content 영역의 너비와 높이다.
- `box-sizing` property가 `border-box`로 지정되어 있으면
  - 이 경우 `width` / `height`는 content + padding + border 영역의 너비와 높이다.
- `width` / `height` 를 포함하여 모든 box model 관련 property (box-sizing, padding, border, margin 등)는 **상속**되지 않는다.

> 컨텐츠가 지정된 `width` / `height` 보다 크면 content 영역 밖으로 컨텐츠가 넘칠 수 있는데,
>
> 이 때, `overflow` property를 `hidden`으로 설정하면 넘친 컨텐츠를 감출 수 있다. ( 차지했던 영역도 같이 삭제)

```html
    <style>
      div {
        background-color: lightcoral;
        width: 200px;
        height: 200px;
        border: 10px solid lightgreen;
      }
    </style>
  </head>
  <body>
    <div>
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Libero, incidunt ut doloribus, laudantium similique explicabo quaerat totam perferendis minima delectus voluptas possimus veniam aut
      numquam laboriosam unde autem mollitia quisquam.
    </div>
    <p>TEST</p>
  </body>
```

> 1. box-sizing : content-box
>
> ![image-20210310220327816](/assets/ImagesForPosts/2021-03-11-CSS Box Model/image-20210310220327816.png)
>
> ​	1.1 overflow : hidden
>
> ![image-20210310220415936](/assets/ImagesForPosts/2021-03-11-CSS Box Model/image-20210310220415936.png)
>
> 2. box-sizing : border-box
>
> ![image-20210310220442700](/assets/ImagesForPosts/2021-03-11-CSS Box Model/image-20210310220442700.png)
>
> ​	2.1 overflow : hidden
>
> ![image-20210310220459781](/assets/ImagesForPosts/2021-03-11-CSS Box Model/image-20210310220459781.png)



**※ 참고 : CSS 스타일링과 box-sizing**

- css 적용 시, 모든 block 요소는 box-sizing을 border-box로 설정하는 것이 일반적
- box-sizing은 default로 상속이 되지 않고 HTML 요소의 default box-sizing은 content-box 이므로, 전체 요소에 box-sizing을 border-box로 설정하기 위해 다음과 같은 css 설정을 많이 함

```css
*,
*::before,
*::after {
    box-sizing: border-box;
}
```





#### max-width / max-height property

요소 너비가 브라우저 너비보다 클 경우, 가로 스크롤바가 생길 수 있음

- 이 때, `max-width`를 사용하면 자동으로 요소 너비가 줄어듬

```html
    <style>
      div {
        background-color: lightcoral;
        width: 1200px;
        border: 10px solid lightgreen;
      }
    </style>
  </head>
  <body>
    <div>
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Libero, incidunt ut doloribus, laudantium similique explicabo quaerat totam perferendis minima delectus voluptas possimus veniam aut
      numquam laboriosam unde autem mollitia quisquam.
    </div>
    <p>TEST</p>
  </body>
```

> 1. width :1200px
>
> ![image-20210310220738321](/assets/ImagesForPosts/2021-03-11-CSS Box Model/image-20210310220738321.png)
>
> 
>
> 2. max-width : 1200px
>
> ![image-20210310220844596](/assets/ImagesForPosts/2021-03-11-CSS Box Model/image-20210310220844596.png)





#### margin / padding property

- `margin` 또는 `padding` 에 -top, -bottom, -left, -right 를 붙여서 설정 가능

- `margin` 또는 `padding` 에 윗쪽, 우측, 아랫쪽, 좌측(시계방향)의 값을 순서대로 작성하여 단축 property 사용 가능

  - 4개의 property 값 설정 시

  ```html
      <style>
        div {
          background-color: lightcoral;
          border: 10px solid lightgreen;
          margin: 10px 20px 30px 40px;
          /*  아래 설정과 같다.
          margin-top: 10px;
          margin-right: 20px;
          margin-bottom: 30px;
          margin-left: 40px;
          */
        }
      </style>
    </head>
    <body>
      <div>드뇌 빌뇌브</div>
      <div>Arrival</div>
      <div>시카리오</div>
    </body>
  ```

  > ![image-20210310221732698](/assets/ImagesForPosts/2021-03-11-CSS Box Model/image-20210310221732698.png)
  >
  > ![image-20210310222213823](/assets/ImagesForPosts/2021-03-11-CSS Box Model/image-20210310222213823.png)

  

  - 3개의 property 값 설정 시

  ```css
  <style>
    div {
          background-color: lightcoral;
          border: 10px solid lightgreen;
          margin: 10px 20px 40px;
          /*  아래 설정과 같다.
          margin-top: 10px;
          margin-right: 20px;
          margin-left: 20px;
          margin-bottom: 40px;
          */
        }
  </style>
  ```

  > ![image-20210310222142573](/assets/ImagesForPosts/2021-03-11-CSS Box Model/image-20210310222142573.png)
  >
  > ![image-20210310222053536](/assets/ImagesForPosts/2021-03-11-CSS Box Model/image-20210310222053536.png)

  

  - 2개의 property 값 설정 시

  ```css
  <style>
  	div {
          background-color: lightcoral;
          border: 10px solid lightgreen;
          margin: 10px 40px;
          /*  아래 설정과 같다.
          margin-top: 10px;
          margin-bottom: 10px;
          margin-right: 40px;
          margin-left: 40px;
          */
  	}
  </style>
  ```

  > ![image-20210310222405799](/assets/ImagesForPosts/2021-03-11-CSS Box Model/image-20210310222405799.png)
  >
  > ![image-20210310222420832](/assets/ImagesForPosts/2021-03-11-CSS Box Model/image-20210310222420832.png)

  

  - 1개의 property 값 설정 시

  ```css
  <style>
  	div {
          background-color: lightcoral;
          border: 10px solid lightgreen;
          margin: 40px;
          /*  아래 설정과 같다.
          margin-top: 40px;
          margin-right: 40px;
          margin-bottom: 40px;
          margin-left: 40px;
          */
  	}
  </style>
  ```

  > ![image-20210310222558922](/assets/ImagesForPosts/2021-03-11-CSS Box Model/image-20210310222558922.png)
  >
  > ![image-20210310222610468](/assets/ImagesForPosts/2021-03-11-CSS Box Model/image-20210310222610468.png)



- **※ block 특성을 가진 요소에 대한 중앙 정렬**
  1. `width` 지정
  2. `margin-left`: `auto`, `margin-right` : `auto`  또는 `margin` : `10px` `auto`

> **block** : 한 줄 모두 차지 (대표 element -  `<div>`)
>
> **inline** : 콘텐츠 크기 만큼만 차지 (대표 element - `<span>`)

```css
    <style>
      div {
        background-color: lightcoral;
        border: 10px solid lightgreen;
        width: 200px; /* 지정해줘야 함 */
        margin: 1px auto;
      }
    </style>
  </head>
  <body>
    <div>드뇌 빌뇌브</div>
    <div>Arrival</div>
    <div>시카리오</div>
  </body>
```

> ![image-20210310223454132](/assets/ImagesForPosts/2021-03-11-CSS Box Model/image-20210310223454132.png)





#### border property

- `border-style` : 선 스타일 설정

  - [(참조)border-style MDN](https://developer.mozilla.org/ko/docs/Web/CSS/border-style)

- `border-width` : 선 굵기 설정, border-style이 설정되어있어야 사용 가능

  - 1px 와 같이 설정하거나 thin, medium, thick 키워드로 설정 가능
  - 다음과 같이 방향별로 설정 가능
    - `border-top-width`
    - `border-right-width`
    - `border-bottom-width`
    - `border-left-width`

  ```css
      <style>
        div {
          background-color: lightcoral;
          width: 300px;
          border-style: dashed;
          border-top-width: thick;
        }
      </style>
    </head>
    <body>
      <div>Lorem ipsum dolor sit amet consectetur adipisicing elit. 
        Illo similique error quod sint sed ab nihil sunt ipsam quis commodi 
        excepturi incidunt
      </div>
    </body>
  ```

  > ![image-20210311022859749](/assets/ImagesForPosts/2021-03-11-CSS Box Model/image-20210311022859749.png)



- `border-color` : 선 색상 설정,  border-style이 설정되어있어야 사용 가능
- `border-radius` : 테두리 모서리를 둥글게 표시
  - [(참조)border-radius MDN](https://developer.mozilla.org/ko/docs/Web/CSS/border-radius)

```html
    <style>
      div {
        background-color: lightcoral;
        width: 200px;
        border-style: solid;
        border-width: medium;
        border-color: cadetblue;
        border-radius: 10%;
      }
    </style>
  </head>
  <body>
    <div>Lorem ipsum dolor sit amet consectetur adipisicing elit. Illo similique error quod sint sed ab nihil sunt ipsam quis commodi excepturi incidunt</div>
  </body>
```

> ![image-20210311023738283](/assets/ImagesForPosts/2021-03-11-CSS Box Model/image-20210311023738283.png)





##### border 단축 property

- border-width, border-style, border-color 순으로 한번에 설정가능

```html
    <style>
      div {
        background-color: lightcoral;
        width: 200px;
        border: 5px double lightblue;
      }
    </style>
  </head>
  <body>
    <div>Lorem ipsum dolor sit amet consectetur adipisicing elit.</div>
  </body>
```

> ![image-20210311024214557](/assets/ImagesForPosts/2021-03-11-CSS Box Model/image-20210311024214557.png)







## block 과 inline

모든 HTML 태그는 각 태그마다 default로 block 또는 inline 특성을 가짐

> 해당 속성은 display property를 통해 변경 가능함.



### block 특성

- 항상 새로운 라인에 표시
- 화면 너비 전체를 차지 (자동으로 width: 100%, height: auto 가 됨)
- width, height, margin, padding property 설정 가능
- block 요소 안에 inline 요소 포함 가능
- default로 block 특성을 가지는 주요 HTML 태그
  - div
  - h1 ~ h6
  - p
  - ol, ul, li
  - hr
  - form
  - table





### inline 특성

- 새로운 라인으로 시작x (동일한 라인에 다른 요소와 함께 위치 가능)
- content 너비만큼 가로폭 차지
- width, height, margin, padding property 설정 불가
  - 상, 하 여백은 line-height로 설정 가능
- inline 요소 안에 block 요소 포함 불가
- inline 특성을 가지는 요소 뒤에 공백(Enter 또는 Space, Tab 등)이 있을 경우, 정의하지 않은 Space(4px)가 자동으로 지정됨
  - 어떤 공백이든 임의로 Space(4px) 로 변환되어 표현됨
- default로 inline 특성을 가지는 주요 HTML 태그
  - span
  - a
  - strong
  - img
  - br
  - input
  - button
  - textarea
  - select

```html
<div style="background-color: lightcoral; width: 150px">
    block <span>특성</span> 테스트</div> /*block 요소 안에 inline 요소 포함 가능*/
<br />
<span style="background-color: lightcoral; width: 150px">
    inline <div>특성</div> 테스트	/*inline 요소 안에 block 요소 포함 불가*/
</span>
<span>span사이에 엔터가 공백(4px로)</span> /*span태그 사이에 엔터*/
```

> ![image-20210311030802024](/assets/ImagesForPosts/2021-03-11-CSS Box Model/image-20210311030802024.png)





### display property

default로 가진 block 또는 inline 특성을 변경 가능

| property 값  | 설명                                                         |
| ------------ | ------------------------------------------------------------ |
| block        | block 특성을 가지는 요소로 설정                              |
| inline       | inline 특성을 가지는 요소로 설정                             |
| inline-block | inline-block 특성을 가지는 요소로 설정                       |
| none         | 해당 요소를 화면에 표시X (해당 요소가 차지하는 공간까지 사라진다) |

```html
<div style="background-color: lightcoral; width: 150px">block <span>특성</span> 테스트</div>
<br />
<span style="background-color: lightcoral; width: 150px">
    inline
    <div>특성</div>
    테스트
</span>
<span>span사이에 엔터가 공백(4px로)</span>
<span style="background-color: lightcoral; width: 150px; display: block">
    inline
    <div>특성</div>
    테스트
</span>
```

> ![image-20210311031330110](/assets/ImagesForPosts/2021-03-11-CSS Box Model/image-20210311031330110.png)





### inline-block 특성

block과 inline 특성 모두를 가진다.

- 다른 요소와 함께 동일 라인에 표시

- width, height, margin, padding property 설정 가능

  - 상, 하 여백은 margin 또는 inline-height 둘 다 가능

- content 너비만큼 가로폭 차지

- inline 특성을 가지는 요소 뒤에 공백(Enter 또는 Space, Tab 등)이 있을 경우, 정의하지 않은 Space(4px)가 자동으로 지정됨

  - 어떤 공백이든 임의로 Space(4px) 로 변환되어 표현됨
  - 이를 제거하기 위해서는 다음과 같은 방법을 사용

  ```html
  <!-- 1.태그와 태그 사이를 붙임-->
  <span>스페이스제거</span><span>
  스페이스제거</span>
                           
  <!-- 2.태그 닫기와 열기를 붙임-->
  <span>스페이스제거</span
  ><span>스페이스제거</span>
  
  <!-- 3.태그와 태그 사이를 주석 처리함-->
  <span>스페이스제거</span><!--
  --><span>스페이스제거</span>
  ```
  
- inline block 예제 코드

```html
<div style="background-color: lightcoral; width: 150px">
    block <span>특성</span> 테스트
</div>
<br />
<span style="background-color: lightcoral; width: 150px; display: inline-block"> 
    inline-block 테스트 
</span>
<span style="background-color: lightcoral; width: 150px; display: inline-block"> 
    inline-block 테스트 
</span>
```

> ![image-20210311032906980](/assets/ImagesForPosts/2021-03-11-CSS Box Model/image-20210311032906980.png)





### visibility property

요소를 보이게 할 것인지 여부 설정

| property 값 | 설명                                                         |
| ----------- | ------------------------------------------------------------ |
| visible     | 해당 요소를 보이게 함(default)                               |
| hidden      | 해당 요소를 보이지 않게 함. **display: none 은 해당 요소가 차지하는 공간까지 사라지지만, visibility: hidden 은 해당 요소가 차지하는공간은 남겨둠** |
| collapse    | table 요소에 사용하며 행이나 열을 보이지 않게 함             |



