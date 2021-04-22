---
title: 'CSS Flexbox'
toc : true
toc_sticky: true
categories: [Frontend]
tags: [Web, CSS, Flexbox]
---



## Flexbox

기존 layout(float, position 기반)보다 더 세련된 방식의 니즈에 부합하기 위한 CSS3의 새로운 layout 방식

>- float 와 position은 레이아웃을 위한 property가 아니어서 표현이 불가능한 레이아웃도 있었
>고 구현이 복잡했음
>- flexbox는 복잡한 레이아웃이라도 적은 코드로 보다 간단하게 구현 가능
>
>- 요소의 사이즈가 불명확하거나 동적으로 변화할 때에도 유연한 레이아웃을 실현 가능

🎊 IE 에서 flexbox의 완벽한 지원이 되지 않기 때문에 크로스 브라우징을 생각하여 잘 사용하지 않았지만 IE의 점유율이 떨어져서 이제 갈수록 사용하는 추세!



### 🎪차근차근 이해해보자!

---

#### block 요소

아래 코드는 div가 block 요소이므로 수직으로 쌓인다.

```html
  <style>
    .container {
      margin: 10px;
      padding: 10px;
      border-radius: 5px;
      background: lightgreen;
    }
     .item {
      width: 100px;
      height: 100px;
      border: 2px solid red;
      border-radius: 5px;
      background: aqua;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
  </div>
</body>
```

> ![image-20210419232844595](/assets/ImagesForPosts/2021-04-22-CSS Flexbox/image-20210419232844595.png)







#### .item 을 수평으로 정렬하려면?

1. **item class를 inline-block으로 변경(inline은 width/height를 가질 수 없으므로)**

```css
.item {
  width: 100px;
  height: 100px;
  border: 2px solid red;
  border-radius: 5px;
  background: aqua;
  display: inline-block; /* 위의 코드에서 .item의 css만 수정 */
}
```

> ![image-20210419233124482](/assets/ImagesForPosts/2021-04-22-CSS Flexbox/image-20210419233124482.png)
>
> - 이 경우 item 사이에 원하지 않는 빈 공간이 들어가게 됨(div태그 사이의 개행문자도 공백으로 인식해버리므로)







2. **float 설정**

```css
.item {
  width: 100px;
  height: 100px;
  border: 2px solid red;
  border-radius: 5px;
  background: aqua;
  float: left; /* 위의 코드에서 .item의 css만 수정 */
}
```

> ![image-20210419233651606](/assets/ImagesForPosts/2021-04-22-CSS Flexbox/image-20210419233651606.png)
>
> - 이 경우 부모 태그(.container) 안에 자식 태그(.item)가 포함되지 않게 됨(자식 태그가 부유 객체가 되기 때문에 부모 태그 입장에서는 자식 태그가 없는 것으로 판정하여 자식 태그의 height를 인식하지 못하기 때문)



- 위의 문제점을 해결하기 위해 clearfix 사용

```css
  <style>
    .container {
      margin: 10px;
      padding: 10px;
      border-radius: 5px;
      background: lightgreen;
    }
    .item {
      width: 100px;
      height: 100px;
      border: 2px solid red;
      border-radius: 5px;
      background: aqua;
      float: left;
    }
    .clearfix::after {
      content: '';
      clear: both;
      display: block;
    }
  </style>
</head>
<body>
  <div class="container clearfix">
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
  </div>
</body>
```

> ![image-20210420000422013](/assets/ImagesForPosts/2021-04-22-CSS Flexbox/image-20210420000422013.png)







3. **flexbox 사용**

간단하다😎

```html
  <style>
    .container {
      margin: 10px;
      padding: 10px;
      border-radius: 5px;
      background: lightgreen;
      display: flex;
    }
    .item {
      width: 100px;
      height: 100px;
      border: 2px solid red;
      border-radius: 5px;
      background: aqua;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
  </div>
</body>
```

> ![image-20210420001612590](/assets/ImagesForPosts/2021-04-22-CSS Flexbox/image-20210420001612590.png)







### flexbox container 와 flexbox item

---

flexbox는 <u>상위 부모 요소</u>인 **flex-container**와 <u>하위 자식 요소</u>인 **flex-item** 으로 구성됨

✅ flexbox를 사용하기 위해서는 부모 요소의 display 속성에 flex를 지정!



#### flex-container 관련 property

| property          | 설명                                                         |
| ----------------- | ------------------------------------------------------------ |
| `display`         | flex-container 정의                                          |
| `flex-direction`  | flex-item 들의 주축(main axis) 방향 설정                     |
| `flex-wrap`       | flex-item 들을 1행 또는 복수의 행으로 배치하는 설정          |
| `flex-flow`       | flex-direction과 flex-wrap을 한번에 설정할 수 있는 단축 property |
| `justify-content` | 주축(main axis) 기반 정렬 방법                               |
| `align-content`   | 교차 축(cross axis) 기반 정렬 방법(2행 이상)                 |
| `align-items`     | 교차 축(cross axis) 기반 정렬 방법(모든 item에 적용)         |







##### display property

- `flex` : block 특성의 flex-container 정의 (flex container 간 수직 정렬)
- `inline-flex` : inline 특성의 flex-container 정의 (flex container 간 수평 정렬)

> 부모 요소에 위의 값을 지정하면 자동으로 자식 요소들은 flex-item이 됨

```html
  <style>
    .container {
      margin: 10px;
      padding: 10px;
      border-radius: 5px;
      background: lightgreen;
      display: flex;
    }
    .item {
      width: 100px;
      height: 100px;
      border: 2px solid red;
      border-radius: 5px;
      background: aqua;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
  </div>
  <div class="container">
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
  </div>
</body>
```

> - display: flex
>
> ![image-20210420020643774](/assets/ImagesForPosts/2021-04-22-CSS Flexbox/image-20210420020643774.png)
>
> 
>
> - display: inline-flex
>
> ![image-20210420020423918](/assets/ImagesForPosts/2021-04-22-CSS Flexbox/image-20210420020423918.png)







##### flex-direction property

- `row` : 좌 → 우 수평 정렬(좌측 정렬)
- `row-reverse` :  우 → 좌 수평 정렬(우측 정렬)
- `column` : 위 → 아래 수직 정렬
- `column-reverse` : 아래 → 위 수직 정렬



```html
  <style>
    .container1 {
      margin: 10px;
      width: 400px;
      border-radius: 5px;
      background: lightgreen;
      display: flex;
      flex-direction: row-reverse;
    }
    .container2 {
      margin: 10px;
      width: 400px;
      border-radius: 5px;
      background: lightgreen;
      display: flex;
      flex-direction: row;
    }
    .container3 {
      margin: 10px;
      width: 400px;
      border-radius: 5px;
      background: lightgreen;
      display: flex;
      flex-direction: column-reverse;
    }
    .container4 {
      margin: 10px;
      width: 400px;
      border-radius: 5px;
      background: lightgreen;
      display: flex;
      flex-direction: column;
    }
    .item {
      margin: 5px;
      width: 70px;
      height: 70px;
      border: 2px solid red;
      border-radius: 5px;
      background: aqua;
      color: red;
      font-size: 30px;
    }
  </style>
</head>
<body>
  <div class="container1">
    row-reverse
    <div class="item">1</div>
    <div class="item">2</div>
    <div class="item">3</div>
  </div>
  <div class="container2">
    row
    <div class="item">1</div>
    <div class="item">2</div>
    <div class="item">3</div>
  </div>
  <div class="container3">
    column-reverse
    <div class="item">1</div>
    <div class="item">2</div>
    <div class="item">3</div>
  </div>
  <div class="container4">
    column
    <div class="item">1</div>
    <div class="item">2</div>
    <div class="item">3</div>
  </div>
</body>
```

> ![image-20210420022629499](/assets/ImagesForPosts/2021-04-22-CSS Flexbox/image-20210420022629499.png)







##### flex-wrap property

- `nowrap` : flex-item들을 개행하지 않고 1행에 배치(default)

  - 각 flex-item들의 너비는 flex-container에 들어갈 수 있는 크기로 자동 축소됨

  - 그러나 flex-item들의 width 합이  flex-container width보다 클 때, flex-item들이 넘치게 됨

    이때 `overflow: auto`를 설정하면 넘치지 않고 가로 스크롤이 생김

- `wrap` : flex-item들의 너비 합이 flex-container 너비보다 클 때, flex-item들을 복수 행에 배치

  - 기본적으로 좌에서 우, 위에서 아래로 배치

- `warp-reverse` : wrap과 동일하나 역방향으로 배치

```html
  <style>
    .container1 {
      margin: 10px;
      width: 400px;
      border-radius: 5px;
      background: lightgreen;
      display: flex;
      flex-wrap: nowrap;
    }
    .container2 {
      margin: 10px;
      width: 400px;
      border-radius: 5px;
      background: lightgreen;
      display: flex;
      flex-wrap: nowrap;
    }
    .container3 {
      margin: 10px;
      width: 400px;
      border-radius: 5px;
      background: lightgreen;
      display: flex;
      flex-wrap: nowrap;
      overflow: auto;
    }
    .container4 {
      margin: 10px;
      width: 400px;
      border-radius: 5px;
      background: lightgreen;
      display: flex;
      flex-wrap: wrap;
    }
    .container5 {
      margin: 10px;
      width: 400px;
      border-radius: 5px;
      background: lightgreen;
      display: flex;
      flex-wrap: wrap-reverse;
    }
    .item {
      margin: 5px;
      height: 70px;
      border: 2px solid red;
      border-radius: 5px;
      background: aqua;
      color: red;
      font-size: 30px;
    }
  </style>
</head>
<body>
  <div class="container1">
    nowrap
    <div class="item">11</div>
    <div class="item">22</div>
    <div class="item">33</div>
    <div class="item">44</div>
    <div class="item">55</div>
  </div>
  <div class="container2">
    nowrap
    <div class="item">11111</div>
    <div class="item">22222</div>
    <div class="item">33333</div>
    <div class="item">44444</div>
    <div class="item">55555</div>
  </div>
  <div class="container3">
    nowrap overflow:auto
    <div class="item">11111</div>
    <div class="item">22222</div>
    <div class="item">33333</div>
    <div class="item">44444</div>
    <div class="item">55555</div>
  </div>
</body>
<body>
  <div class="container4">
    wrap
    <div class="item">11111</div>
    <div class="item">22222</div>
    <div class="item">33333</div>
    <div class="item">44444</div>
    <div class="item">55555</div>
  </div>
  <div class="container5">
    wrap-reverse
    <div class="item">11111</div>
    <div class="item">22222</div>
    <div class="item">33333</div>
    <div class="item">44444</div>
    <div class="item">55555</div>
  </div>
</body>
```

> ![image-20210420024547384](/assets/ImagesForPosts/2021-04-22-CSS Flexbox/image-20210420024547384.png)







##### flex-flow property

- flex-direction과 flex-wrap 을 한번에 쓸 수 있는 단축 property

```css
/* 사용법 */
flex-flow: flex-direction flew-wrap;
```







##### justify-content

주축(main axis) 기반 수평 정렬 방법

> 주축, 교차 축이란?
>
> flex-item들을 수평 나열 시 => 가로축(수평 방향) = 주축, 세로축 = 교차 축
>
> flex-item들을 수직 나열 시 => 세로축(수직 방향) = 주축, 가로축 = 교차 축



- `flex-start` : 좌측 기준 정렬(default)
- `flex-end` : 우측 기준 정렬
- `center` : 가운데 수평 정렬
- `space-between` : 첫번째는 좌측 끝에, 마지막은 우측 끝에 배치 후 나머지 item들은 균등한 간격으로 정렬
- `space-around` : item들이 균등한 간격으로 정렬

```html
  <style>
    .container1 {
      margin: 10px;
      width: 400px;
      border-radius: 5px;
      background: lightgreen;
      display: flex;
      justify-content: flex-start;
    }
    .container2 {
      margin: 10px;
      width: 400px;
      border-radius: 5px;
      background: lightgreen;
      display: flex;
      justify-content: flex-end;
    }
    .container3 {
      margin: 10px;
      width: 400px;
      border-radius: 5px;
      background: lightgreen;
      display: flex;
      justify-content: center;
    }
    .container4 {
      margin: 10px;
      width: 400px;
      border-radius: 5px;
      background: lightgreen;
      display: flex;
      justify-content: space-between;
    }
    .container5 {
      margin: 10px;
      width: 400px;
      border-radius: 5px;
      background: lightgreen;
      display: flex;
      justify-content: space-around;
    }
    .item {
      margin: 5px;
      height: 70px;
      border: 2px solid red;
      border-radius: 5px;
      background: aqua;
      color: red;
      font-size: 30px;
    }
  </style>
</head>
<body>
  <div class="container1">
    <div class="item">11111</div>
    <div class="item">22222</div>
    <div class="item">33333</div>
  </div>
  <div class="container2">
    <div class="item">11111</div>
    <div class="item">22222</div>
    <div class="item">33333</div>
  </div>
  <div class="container3">
    <div class="item">11111</div>
    <div class="item">22222</div>
    <div class="item">33333</div>
  </div>
</body>
<body>
  <div class="container4">
    <div class="item">11111</div>
    <div class="item">22222</div>
    <div class="item">33333</div>
  </div>
  <div class="container5">
    <div class="item">11111</div>
    <div class="item">22222</div>
    <div class="item">33333</div>
  </div>
</body>
```

> ![image-20210420051914536](/assets/ImagesForPosts/2021-04-22-CSS Flexbox/image-20210420051914536.png)







##### align-content property

`align-content` : 교차 축 기준 수직 정렬 방법, 복수의 행을 하나로 취급하여 일괄적으로 적용

📐주요 값

| value           | 설명                                                         |
| --------------- | ------------------------------------------------------------ |
| `stretch`       | item 높이를 미설정 시 교차 축을 채우기 위해 자동으로 늘어남(default) |
| `flex-start`    | 첫 행의 시작부터 item들이 정렬, `wrap-reverse` 일 경우 기준이 반대로 바뀜 |
| `flex-end`      | 마지막 행의 끝에서부터 item들이 정렬, `wrap-reverse` 일 경우 기준이 반대로 바뀜 |
| `center`        | 가운데 정렬                                                  |
| `space-between` | 첫번째 item 행은 상단 시작에, 마지막 item 행은 하단 끝에 배치 후 나머지 item행들은 균등한 간격으로 정렬 |
| `space-around`  | item행들이 균등한 간격으로 정렬                              |

```html
  <style>
    .container1 {
      margin: 10px;
      width: 300px;
      height: 400px;
      border-radius: 5px;
      background: lightgreen;
      display: flex;
      flex-wrap: wrap;
      justify-content: space-around;
      align-content: stretch;
    }
    .container2 {
      margin: 10px;
      width: 300px;
      height: 400px;
      border-radius: 5px;
      background: lightgreen;
      display: flex;
      flex-wrap: wrap-reverse;
      justify-content: space-around;
      align-content: stretch;
    }
    .item {
      margin: 5px;
      height: 70px;
      border: 2px solid red;
      border-radius: 5px;
      background: aqua;
      color: red;
      font-size: 30px;
    }
  </style>
</head>
<body>
  <div class="container1">
    <div class="item">11111</div>
    <div class="item">22222</div>
    <div class="item">33333</div>
    <div class="item">44444</div>
    <div class="item">55555</div>
    <div class="item">66666</div>
  </div>
  <div class="container2">
    <div class="item">11111</div>
    <div class="item">22222</div>
    <div class="item">33333</div>
    <div class="item">44444</div>
    <div class="item">55555</div>
    <div class="item">66666</div>
  </div>
</body>
```

> 1. stretch(위는 wrap, 아래는 wrap-reverse)
>
> ![image-20210422222137830](/assets/ImagesForPosts/2021-04-22-CSS Flexbox/image-20210422222137830.png)
>
> 
>
> 2. flex-start(위는 wrap, 아래는 wrap-reverse)
>
> ![image-20210422222222966](/assets/ImagesForPosts/2021-04-22-CSS Flexbox/image-20210422222222966.png)
>
> 
>
> 3. flex-end(위는 wrap, 아래는 wrap-reverse)
>
> ![image-20210422222238914](/assets/ImagesForPosts/2021-04-22-CSS Flexbox/image-20210422222238914.png)
>
> 
>
> 4. center(위는 wrap, 아래는 wrap-reverse)
>
> ![image-20210422222253777](/assets/ImagesForPosts/2021-04-22-CSS Flexbox/image-20210422222253777.png)
>
> 
>
> 5. space-between(위는 wrap, 아래는 wrap-reverse)
>
> ![image-20210422222349238](/assets/ImagesForPosts/2021-04-22-CSS Flexbox/image-20210422222349238.png)
>
> 
>
> 6. space-around(위는 wrap, 아래는 wrap-reverse)
>
> ![image-20210422222405283](/assets/ImagesForPosts/2021-04-22-CSS Flexbox/image-20210422222405283.png)







##### align-items property

`align-items` : 교차 축 기준 수직 정렬 방법, 각 행마다 적용(모든 item에 적용)

📐주요 값

| value        | 설명                                                         |
| ------------ | ------------------------------------------------------------ |
| `stretch`    | item 높이를 미설정 시 교차 축을 채우기 위해 자동으로 늘어남(default) |
| `flex-start` | 첫 행의 시작부터 item들이 정렬, `wrap-reverse` 일 경우 기준이 반대로 바뀜 |
| `flex-end`   | 마지막 행의 끝에서부터 item들이 정렬, `wrap-reverse` 일 경우 기준이 반대로 바뀜 |
| `center`     | 가운데 정렬                                                  |
| `baseline`   | 각 행의 문자 기준선 정렬                                     |

```html
  <style>
    .container1 {
      margin: 10px;
      width: 300px;
      height: 400px;
      border-radius: 5px;
      background: lightgreen;
      display: flex;
      justify-content: space-around;
      flex-wrap: wrap;
      align-items: stretch;
    }
    .container2 {
      margin: 10px;
      width: 300px;
      height: 400px;
      border-radius: 5px;
      background: lightgreen;
      display: flex;
      justify-content: space-around;
      flex-wrap: wrap;
      align-items: stretch;
    }
    .container3 {
      margin: 10px;
      width: 300px;
      height: 400px;
      border-radius: 5px;
      background: lightgreen;
      display: flex;
      justify-content: space-around;
      flex-wrap: wrap-reverse;
      align-items: flex-start;
    }
    .container4 {
      margin: 10px;
      width: 300px;
      height: 400px;
      border-radius: 5px;
      background: lightgreen;
      display: flex;
      justify-content: space-around;
      flex-wrap: wrap-reverse;
      align-items: flex-end;
    }
    .container5 {
      margin: 10px;
      width: 300px;
      height: 400px;
      border-radius: 5px;
      background: lightgreen;
      display: flex;
      justify-content: space-around;
      flex-wrap: wrap;
      align-items: center;
    }
    .container6 {
      margin: 10px;
      width: 300px;
      height: 400px;
      border-radius: 5px;
      background: lightgreen;
      display: flex;
      justify-content: space-around;
      flex-wrap: wrap;
      align-items: baseline;
    }
    .item {
      margin: 5px;
      border: 2px solid red;
      border-radius: 5px;
      background: aqua;
      color: red;
    }
    .itemHeight1 {
      height: 50px;
      font-size: 20px;
    }
    .itemHeight2 {
      height: 200px;
      font-size: 15px;
    }
    .itemHeight3 {
      height: 120px;
      font-size: 35px;
    }
    .itemHeight4 {
      height: 110px;
      font-size: 10px;
    }
    .itemHeight5 {
      height: 150px;
      font-size: 18px;
    }
  </style>
</head>
<body>
  <div class="container1">
    <div class="item">11111</div>
    <div class="item">22222</div>
    <div class="item">33333</div>
    <div class="item">44444</div>
    <div class="item">55555</div>
  </div>
  <div class="container2">
    <div class="item itemHeight1">11111</div>
    <div class="item itemHeight2">22222</div>
    <div class="item itemHeight3">33333</div>
    <div class="item itemHeight4">44444</div>
    <div class="item itemHeight5">55555</div>
  </div>
  <div class="container3">
    <div class="item itemHeight1">11111</div>
    <div class="item itemHeight2">22222</div>
    <div class="item itemHeight3">33333</div>
    <div class="item itemHeight4">44444</div>
    <div class="item itemHeight5">55555</div>
  </div>
  <div class="container4">
    <div class="item itemHeight1">11111</div>
    <div class="item itemHeight2">22222</div>
    <div class="item itemHeight3">33333</div>
    <div class="item itemHeight4">44444</div>
    <div class="item itemHeight5">55555</div>
  </div>
  <div class="container5">
    <div class="item itemHeight1">11111</div>
    <div class="item itemHeight2">22222</div>
    <div class="item itemHeight3">33333</div>
    <div class="item itemHeight4">44444</div>
    <div class="item itemHeight5">55555</div>
  </div>
  <div class="container6">
    <div class="item itemHeight1">11111</div>
    <div class="item itemHeight2">22222</div>
    <div class="item itemHeight3">33333</div>
    <div class="item itemHeight4">44444</div>
    <div class="item itemHeight5">55555</div>
  </div>
</body>
```

> 1. stretch, item의 height를 설정하지 않았을 경우
>
> ![image-20210422214914646](/assets/ImagesForPosts/2021-04-22-CSS Flexbox/image-20210422214914646.png)
>
> 
>
>    1-1. stretch, item의 height를 설정했을 경우
>
> ![image-20210422214952794](/assets/ImagesForPosts/2021-04-22-CSS Flexbox/image-20210422214952794.png)
>
> 
>
> 2. flex-start, wrap, item의 height를 설정했을 경우
>
> ![image-20210422215320205](/assets/ImagesForPosts/2021-04-22-CSS Flexbox/image-20210422215320205.png)
>
> 
>
>    2-1. flex-start, wrap-reverse, item의 height를 설정했을 경우
>
> ![image-20210422215502713](/assets/ImagesForPosts/2021-04-22-CSS Flexbox/image-20210422215502713.png)
>
> 
>
>    2-2. flex-start, wrap-reverse, item의 height를 설정하지 않았을 경우
>
> ![image-20210422215741722](/assets/ImagesForPosts/2021-04-22-CSS Flexbox/image-20210422215741722.png)
>
> 
>
> 3. flex-end, wrap
>
> ![image-20210422215847194](/assets/ImagesForPosts/2021-04-22-CSS Flexbox/image-20210422215847194.png)
>
> 
>
>    3-1. flex-end, wrap-reverse
>
> ![image-20210422220036123](/assets/ImagesForPosts/2021-04-22-CSS Flexbox/image-20210422220036123.png)
>
> 
>
> 4. center
>
> ![image-20210422220139668](/assets/ImagesForPosts/2021-04-22-CSS Flexbox/image-20210422220139668.png)
>
> 
>
> 5. baseline
>
> ![image-20210422220159888](/assets/ImagesForPosts/2021-04-22-CSS Flexbox/image-20210422220159888.png)









#### flexbox-item 관련 property

| property      | 설명                                                         |
| ------------- | ------------------------------------------------------------ |
| `order`       | flex-item 배치 순서 설정                                     |
| `flex-grow`   | lex item 너비 확대 비율 설정                                 |
| `flex-shrink` | flex item 너비 축소 비율 설정                                |
| `flex-basis`  | flex item 너비 기본값 설정                                   |
| `flex`        | flex-grow, flex-shrink, flex-basis를 한번에 설정할 수 있는 단축 property |
| `align-self`  | flex container의 align-content/align-items보다 우선하여 개별 flex item의 수직 정렬 방법 설정 |







##### order

- order값의 오름차순으로 배치됨
- 임의의 정수(-/+)값 지정 가능(default: 0)

```html
  <style>
    .container1 {
      margin: 10px;
      width: 300px;
      height: 400px;
      border-radius: 5px;
      background: lightgreen;
      display: flex;
      flex-wrap: wrap;
      justify-content: space-around;
    }
    .item {
      margin: 5px;
      height: 70px;
      border: 2px solid red;
      border-radius: 5px;
      background: aqua;
      color: red;
      font-size: 30px;
    }
    .item1 {
      order: 1;
    }
    .item2 {
      order: 2;
    }
    .item3 {
      order: 3;
    }
    .item4 {
      order: 4;
    }
    .item5 {
      order: 5;
    }
    .item6 {
      order: 6;
    }
  </style>
</head>
<body>
  <div class="container1">
    <div class="item item3">11111</div>
    <div class="item item4">22222</div>
    <div class="item item1">33333</div>
    <div class="item item6">44444</div>
    <div class="item item2">55555</div>
    <div class="item item5">66666</div>
  </div>
</body>
```

> ![image-20210422224100809](/assets/ImagesForPosts/2021-04-22-CSS Flexbox/image-20210422224100809.png)







##### flex-grow

- 모든  flex item들이 동일한 flex-grow 값을 가지면 모든 flex item은 동일한 너비를 가짐
- flex item들이  서로 다른 flex-grow 값을 가지면 비율에 따른 너비를 가짐
  - flex-grow 값 / 전체 flex-grow 값의 총합

- 양의 정수값만 지정 가능(default: 0)

```html
  <style>
    .container1 {
      margin: 10px;
      border-radius: 5px;
      background: lightgreen;
      display: flex;
      flex-wrap: wrap;
      justify-content: space-around;
    }
    .item {
      margin: 5px;
      height: 70px;
      border: 2px solid red;
      border-radius: 5px;
      background: aqua;
      color: red;
      font-size: 30px;
    }
    .item1 {
      flex-grow: 1;
    }
    .item2 {
      flex-grow: 1;
    }
    .item3 {
      flex-grow: 1;
    }
    .item4 {
      flex-grow: 1;
    }
    .item5 {
      flex-grow: 1;
    }
    .item6 {
      flex-grow: 1;
    }
  </style>
</head>
<body>
  <div class="container1">
    <div class="item item1">111</div>
    <div class="item item2">222</div>
    <div class="item item3">333</div>
    <div class="item item4">444</div>
    <div class="item item5">555</div>
    <div class="item item6">666</div>
  </div>
</body>
```

> 1. 동일한 flex-grow 값(1, 1, 1, 1, 1, 1)
>
> ![image-20210422225010355](/assets/ImagesForPosts/2021-04-22-CSS Flexbox/image-20210422225010355.png)
>
> 
>
> 2. 서로 다른 flex-grow 값(3, 1, 1, 3, 6, 1)
>
> ![image-20210422225124088](/assets/ImagesForPosts/2021-04-22-CSS Flexbox/image-20210422225124088.png)







##### flex-shrink

- 모든  flex item들이 동일한 flex-shrink값을 가지면 동일한 비율로 flex-container 안에서 축소
- flex item들이  서로 다른 flex-shrink값을 가지면 비율에 따라 축소됨
  - flex-shrink값 / 전체 flex-shrink값의 총합

- 양의 정수값만 지정 가능하고 0이면 해제하고 원래 너비로 표시됨(default: 1)

```html
  <style>
    .container1 {
      margin: 10px;
      width: 400px;
      border-radius: 5px;
      background: lightgreen;
      display: flex;
      justify-content: space-around;
    }
    .item {
      margin: 5px;
      width: 400px; /* 각각 400px의 너비를 가짐 */
      border: 2px solid red;
      border-radius: 5px;
      background: aqua;
      color: red;
      font-size: 30px;
    }
    .item1 {
      flex-shrink: 1;
    }
    .item2 {
      flex-shrink: 4;
    }
  </style>
</head>
<body>
  <div class="container1">
    <div class="item item1">111</div>
    <div class="item item2">222</div>
  </div>
</body>
```

> 1. 동일한 flex-shrink 값(1, 1)
>    - 400px에서 각각 50%만큼 줄었음
>
> ![image-20210422230518789](/assets/ImagesForPosts/2021-04-22-CSS Flexbox/image-20210422230518789.png)
>
> 
>
> 2. 서로 다른 flex-shrink 값(1, 4)
>    - 400px에서 1은 1/5만큼(20%) 줄었고 2는 4/5만큼(80%) 줄었음
>
> ![image-20210422230457704](/assets/ImagesForPosts/2021-04-22-CSS Flexbox/image-20210422230457704.png)
>
> 
>
> 3. 0일 때
>
> ![image-20210422230731223](/assets/ImagesForPosts/2021-04-22-CSS Flexbox/image-20210422230731223.png)







##### flex-basis

- 기본값을 px, % 등의 단위로 지정(default: auto)

```html
  <style>
    .container1 {
      margin: 10px;
      width: 400px;
      border-radius: 5px;
      background: lightgreen;
      display: flex;
      justify-content: space-around;
    }
    .item {
      margin: 5px;
      width: 400px; /* 각각 400px의 너비를 가짐 */
      border: 2px solid red;
      border-radius: 5px;
      background: aqua;
      color: red;
      font-size: 30px;
    }
    .item1 {
      flex-basis: 150px;
    }
    .item2 {
      flex-shrink: 250px;
    }
  </style>
</head>
<body>
  <div class="container1">
    <div class="item item1">111</div>
    <div class="item item2">222</div>
  </div>
</body>
```

> - 1은 150px, 2는 250px 크기를 갖는다.
>
> ![image-20210422231130254](/assets/ImagesForPosts/2021-04-22-CSS Flexbox/image-20210422231130254.png)







##### flex

- flex-grow, flex-shrink, flex-basis의 단축 property

- default: 0 1 auto

- 호환성을 위해 개별 property를 사용하는 것을 추천

```html
  <style>
    .container1 {
      border-radius: 5px;
      background: lightgreen;
      display: flex;
    }
    .item {
      border: 2px solid red;
      border-radius: 5px;
      background: aqua;
      color: red;
      font-size: 30px;
    }
    .item1 {
      flex: 0 1 300px;
    }
    .item2 {
      flex: 0 0 300px;
    }
    .item3 {
      flex: 1 1 300px;
    }
    .item4 {
      flex: 0 1 300px;
    }
  </style>
</head>
<body>
  <div class="container1">
    <div class="item item1">shrink1</div>
    <div class="item item2">shrink0</div>
  </div>
  <div class="container1">
    <div class="item item3">grow1</div>
    <div class="item item4">grow0</div>
  </div>
</body>
```

>1. shrink: 1은 기본 너비에서 줄어들지만 0은 유지
>
>![shrink](/assets/ImagesForPosts/2021-04-22-CSS Flexbox/shrink.gif)
>
>
>
>2. grow: 1은 기존 너비에서 늘어나지만 0은 유지
>
>![grow](/assets/ImagesForPosts/2021-04-22-CSS Flexbox/grow.gif)







##### align-self

- flex container의 align-content/align-items보다 우선하여 개별 flex item의 수직 정렬 방법 설정
- align-items와 동일한 값으로 설정 가능(default: auto)

  사용법

```css
.flex-item {
  align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
```



```html
  <style>
    .container1 {
      width: 400px;
      height: 600px;
      border-radius: 5px;
      background: lightgreen;
      display: flex;
      flex-wrap: wrap;
      justify-content: space-around;
      align-items: flex-end;
    }
    .item {
      border: 2px solid red;
      border-radius: 5px;
      background: aqua;
      color: red;
      font-size: 30px;
    }
    .item1 {
      height: 100px;
      align-self: flex-start;
    }
    .item2 {
      height: 200px;
      align-self: center;
    }
    .item3 {
      height: 150px;
      align-self: stretch;
    }
    .item4 {
      height: 50px;
    }
    .item5 {
      height: 100px;
      align-self: baseline;
    }
    .item6 {
      height: 200px;
      align-self: baseline;
    }
  </style>
</head>
<body>
  <div class="container1">
    <div class="item item1">11111</div>
    <div class="item item2">22222</div>
    <div class="item item3">33333</div>
    <div class="item item4">44444</div>
    <div class="item item5">55555</div>
    <div class="item item6">66666</div>
  </div>
</body>
```

> ![image-20210422234420125](/assets/ImagesForPosts/2021-04-22-CSS Flexbox/image-20210422234420125.png)









### 참고

실시간 연습 가능한 사이트

- [Flexbox playground (codepen.io)](https://codepen.io/enxaneta/pen/adLPwv)
- [Flexbox Froggy - CSS flexbox 속성 배우기 게임](http://flexboxfroggy.com/#ko)