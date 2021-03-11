---
title: 'CSS Background'
toc : true
toc_sticky: true
categories: [Frontend]
tags: [Web, CSS, Background]
---



### CSS Background property

background는 해당 요소의 배경 이미지 또는 색상 설정



#### 1. background-image property

요소에 배경 이미지를 설정

```html
<style>
  div {
      background-image: url(hos.gif);
      height: 200px;
      color: lightcoral;
  }
</style>
</head>
<body>
    <div>Background image</div>
</body>
```

> ![image-20210311034427290](/assets/ImagesForPosts/2021-03-11-CSS Background/image-20210311034427290.png)





####  2. background-repeat property

배경 이미지가 요소 사이즈보다 작을 때, 반복해서 해당 사이즈를 채울 것인지 설정

| property 값 | 설명                                                         |
| ----------- | ------------------------------------------------------------ |
| `repeat`    | 요소의 배경 영역을 채울 때까지 이미지 반복, 이미지가 넘치면 짜름(default) |
| `space`     | 요소가 짤리지 않을 만큼만 이미지 반복. 처음과 마지막 반복 이미지는 요소의 양쪽 끝에 고정 후, 각 이미지 사이의 남은 여백을 고르게 분배. 이미지가 짤리는 경우는 이미지 크기가 요소 사이즈보다 클 경우이다. |
| `round`     | 요소 사이즈가 늘어나면 그 때 반복해서 이미지를 채우고 이미지가 짤리지 않도록 전체 반복 이미지 사이즈도 재조정 |
| `no-repeat` | 이미지를 반복하지 않음. 반복하지 않은 이미지의 위치는 `background-position` property로 설정 가능 |

```html
<style>
  div {
      background-image: url(hos.gif);
      height: 200px;
      color: lightcoral;
      background-repeat: space;
  }
</style>
</head>
<body>
  <div>Background image</div>
</body>
```

> 1. `space` : 줄이거나 늘려도 이미지의 사이즈는 그대로이다.
>
> ![image-20210311035210447](/assets/ImagesForPosts/2021-03-11-CSS Background/image-20210311035210447.png)
>
> ![image-20210311035229557](/assets/ImagesForPosts/2021-03-11-CSS Background/image-20210311035229557.png)
>
> 
>
> 2. `round` : 줄이거나 늘리면 이미지의 사이즈가 조정된다.
>
> ![image-20210311035315994](/assets/ImagesForPosts/2021-03-11-CSS Background/image-20210311035315994.png)
>
> ![image-20210311035327451](/assets/ImagesForPosts/2021-03-11-CSS Background/image-20210311035327451.png)
>
> 
>
> 3. `no-repeat`
>
> ![image-20210311035411356](/assets/ImagesForPosts/2021-03-11-CSS Background/image-20210311035411356.png)



- 반복 세부 설정

| 한 개의 값으로 설정 시                | 두 개의 값으로 설정 시 |
| ------------------------------------- | ---------------------- |
| `repeat-x` : 가로로만 이미지 반복     | `repeat no-repeat`     |
| `repeat-y` : 세로로만 이미지 반복     | `no-repeat repeat`     |
| `repeat` : 가로/세로 모두 이미지 반복 | `repeat repeat`        |
| `space`                               | `space space`          |
| `round`                               | `round round`          |
| `no-repeat`                           | `no-repeat no-repeat`  |

```html
<style>
  div {
      background-image: url(hos.gif);
      height: 200px;
      color: lightcoral;
      background-repeat: no-repeat repeat;
  }
</style>
</head>
<body>
  <div>Background image</div>
</body>
```

> 1. `no-repeat repeat`
>
> ![image-20210311040108462](/assets/ImagesForPosts/2021-03-11-CSS Background/image-20210311040108462.png)
>
> 
>
> 2. `repeat-x`
>
> ![image-20210311040145301](/assets/ImagesForPosts/2021-03-11-CSS Background/image-20210311040145301.png)
>
> 
>
> 3. `repeat space`
>
> ![image-20210311040226868](/assets/ImagesForPosts/2021-03-11-CSS Background/image-20210311040226868.png)



- 복수의 이미지 설정 가능
  - 먼저 설정된 이미지가 앞에 나옴 (따라서 repeat 설정 시 먼저 설정된 이미지로 덮일 수 있음)

```html
  <style>
    div {
      background-image: url(hos.gif), url(http://rssgo.co.kr/web/files/attach/images/148/024/010/270fcd179e8cc9c73a4d658546e9f2d4.gif);
      height: 200px;
      color: lightcoral;
      background-repeat: no-repeat repeat;
    }
  </style>
</head>
<body>
  <div>Background image</div>
</body>
```

> ![image-20210311040731307](/assets/ImagesForPosts/2021-03-11-CSS Background/image-20210311040731307.png)



> - 위에서 background-repeat property에 값 구분을 콤마(,)로 해줄 경우
>   - 각각의 이미지에 대해서 값 설정이 됨
>
>  ```css
>  background-repeat: no-repeat, repeat;
>  ```

>  ![image-20210311041059613](/assets/ImagesForPosts/2021-03-11-CSS Background/image-20210311041059613.png)





#### 3. background-size property

배경 이미지 사이즈 설정, [참고](https://cssreference.io/property/background-size/)

- `auto` : 이미지 크기 유지
- length
  - 값을 두 개 넣으면 첫 번째 값이 가로 크기, 두 번째 값이 세로 크기
  - 값을 한 개 넣으면 가로 크기로 설정되고 세로 크기는 원본 이미지의 비율에 맞게 자동 설정
  - px, % 등의 값으로 설정 가능
- `cover` : 요소 사이즈를 다 채울 수 있게 이미지를 확대 또는 축소, 비율 유지
- `contain` : 요소 사이즈를 벗어나지 않는 최대 크기로 이미지를 확대 또는 축소, 비율 유지
- `initial` : 기본값으로 설정

```html
<style>
  div {
      background-image: url(hos.gif), url(http://rssgo.co.kr/web/files/attach/images/148/024/010/270fcd179e8cc9c73a4d658546e9f2d4.gif);
      height: 200px;
      color: lightcoral;
      background-repeat: no-repeat;
      background-size: 5%, 50%;
  }
</style>
</head>
<body>
  <div>Background image</div>
</body>
```

> 1. 5%, 50%
>
> ![image-20210311042609178](/assets/ImagesForPosts/2021-03-11-CSS Background/image-20210311042609178.png)
>
> 
>
> 2. 5%, cover
>
> ![image-20210311042628414](/assets/ImagesForPosts/2021-03-11-CSS Background/image-20210311042628414.png)
>
> 
>
> 3. 5%, contain
>
> ![image-20210311042644840](/assets/ImagesForPosts/2021-03-11-CSS Background/image-20210311042644840.png)





#### 4. background-attachment property

- `scroll` : default. 브라우저를 스크롤하면 배경 이미지는 스크롤 되어서 안보여질 수 있음
- `fixed` : 스크롤이 되더라도 배경 이미지는 고정됨

```html
<style>
  body {
      background-image: url(hos.gif);
      height: 200px;
      color: lightcoral;
      background-repeat: repeat no-repeat;
      background-attachment: fixed;
  }
</style>
<body>
  <p>lorem</p> * 50
</body>
```

> - 스크롤이 중간인데도 background img가 고정되어 표시됨
>
>   
>
>   ![image-20210311043554866](/assets/ImagesForPosts/2021-03-11-CSS Background/image-20210311043554866.png)





#### 5. background-position property

- background-image는 default로 좌측 상단에 이미지 위치
- `background-position` 으로 좌표(x, y)를 지정 가능
- 주요 property 값
  - 두 값으로 설정 가능. 
  - 한 가지 값으로 설정할 경우, 나머지 값은 center -> 정중앙은 `center`
  - `left top` : 좌측 상단
  - `left center` : 좌측 중앙
  - `left bottom` : 좌측 맨아래
  - `right top`
  - `right center`
  - `right bottom`
  - `center top` : 가운데 상단
  - `center center` : 정 가운데
  - `center bottom` : 가운데 맨아래
  - x y : px, em, % 등으로 위치 지정 가능. %의 경우 0% 0%는 좌측 상단, 100% 100%는 우측 하단

```html
  <style>
    div {
        background-image: url(hos.gif);
        height: 200px;
        color: lightcoral;
        background-repeat: no-repeat;
        background-position: left center;
    }
  </style>
</head>
<body>
  <div>background img</div>
</body>
```

> ![image-20210311155523111](/assets/ImagesForPosts/2021-03-11-CSS Background/image-20210311155523111.png)





#### 6. background-color property

CSS 색상 단위로 배경색 설정

- `transparent` : 투명 설정(default)

```html
  <style>
    div {
      background-image: url(hos.gif);
      height: 200px;
      color: lightcoral;
      background-repeat: no-repeat;
      background-position: left center;
      background-color: darkgoldenrod;
    }
  </style>
</head>
<body>
  <div>background img</div>
</body>
```

> ![image-20210311155733395](/assets/ImagesForPosts/2021-03-11-CSS Background/image-20210311155733395.png)





#### 7. background 단축 property

```css
/* 아래와 같은 property들로 단축 설정 가능 */
background: image color repeat attachment position
```

```html
  <style>
    div {
      background: url(hos.gif) repeat-y lightcoral fixed center;
      height: 200px;
      color: aquamarine;
    }
  </style>
</head>
<body>
  <div>background img</div>
</body>
```

> ![image-20210311164608149](/assets/ImagesForPosts/2021-03-11-CSS Background/image-20210311164608149.png)