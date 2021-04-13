---
title: 'CSS Animation'
toc : true
toc_sticky: true
categories: [Frontend]
tags: [Web, CSS, Animation]
---



## Animation

transition과 유사하게 HTML 요소에 적용되는 CSS 스타일을 다른 CSS 스타일로 부드럽게 전환시켜줌

>  transition VS animation
>  **transition**은 단순히 요소의 스타일 변화에 주안점이 있다면 animation은 중간에 변경되는 요소의 움직임을 세밀하게 시간 흐름 단위로 제어할 수 있다.

- animation은 애니메이션을 나타내는 CSS 스타일과 애니메이션의 흐름을 나타내는 키프레임(@keyframes)들로 이루어짐

- JS 기반 애니메이션보다 렌더링 성능이 좋지만 경우에 따라서 JS 애니메이션을 쓰는 편이 좋음
  - CSS 애니메이션 : 가벼운 효과 (ex: width 변경 애니메이션)
  - JS 애니메이션 : 세밀한 제어가 필요한 효과(ex: 바운스, 중지, 되감기, 감속 등)





### animation 주요 property

| 프로퍼티                    | 설명                                                         | 기본값  |
| :-------------------------- | :----------------------------------------------------------- | :-----: |
| `animation-name`            | @keyframes 애니메이션 **이름** 지정                          |         |
| `animation-duration`        | **한 싸이클의 애니메이션에 소요되는 시간**을 초 단위(s) 또는 밀리 초 단위(ms)로 지정 |   0s    |
| `animation-timing-function` | 애니메이션 **속도**를 설정하는 함수를 지정                   |  ease   |
| `animation-delay`           | 애니메이션 **시작 전 대기 시간**을 초 단위(s) 또는 밀리 초 단위(ms)로 지정 |   0s    |
| `animation-iteration-count` | 애니메이션 **재생 횟수**를 지정                              |    1    |
| `animation-direction`       | 애니메이션 **종료 후 반복될 때 진행 방향** 지정              | normal  |
| `animation-fill-mode`       | 애니메이션 **종료 또는 대기 요소의 스타일**을 지정           |         |
| `animation-play-state`      | 애니메이션 **재생 상태**(재생 또는 중지)를 지정              | running |
| `animation`                 | 단축 property                                                |         |







#### keyframes

from 또는 0%에 설정한 스타일 -> to 또는 100%까지, 그 중간 시점을 %로 표기하여 각 시점에 설정한 스타일로 변경되는 스타일을 설정 가능

1. @keyframes에 이름 지정

   ```css
   @keyframes test{}
   ```

   

2. @keyframes에 원하는 시점에 스타일 지정

   - from 또는 0% : 시작 프레임
   - to 또는 100% : 마지막 프레임
   - 0% ~ 100% 사이 : 시작과 끝 중간 사이의 원하는 시점 프레임

   ```css
   @keyframes test{
       from {
           left: 0;
       }
       50% {
           left: 60px;
       }
       to {
           left: 200px;
       }
   }
   ```



3. 애니메이션 요소 지정

   - `animation-name`에 정의한 @keyframes 이름 넣기
   - `animation-duration`에 한 싸이클의 애니메이션에 소요되는 시간 지정
   - `animation-iteration-count`에 애니메이션 반복 횟수 지정

   ```css
   .box1 {
         position: absolute;
         width: 100px;
         height: 100px;
         background: firebrick;
         border-radius: 5px;
         animation-name: move, fadeOut;
         animation-duration: 3s, 3s;
         animation-iteration-count: infinite;
   }
   ```





##### 💫여러 키프레임 설정

```html
  <style>
    .box1 {
      position: absolute;
      width: 100px;
      height: 100px;
      background: firebrick;
      border-radius: 5px;
      animation-name: move, fadeOut;
      animation-duration: 3s, 3s;
       animation-iteration-count: infinite;
    }
    @keyframes move {
      from {
        left: 0;
      }
      50% {
        left: 60px;
      }
      to {
        left: 200px;
      }
    }
    @keyframes fadeOut {
      from {
        opacity: 1;
      }
      to {
        opacity: 0;
      }
    }
  </style>
</head>
<body>
  <div class="box1"></div>
</body>
```

> ![animation](/assets/ImagesForPosts/2021-04-14-CSS Animation/animation.gif)







#### animation-duration

미지정 시 기본값 0s가 설정되어 애니메이션이 실행되지 않음 







#### animation-timing-function

[transition-timing-function](https://lastcow9000.github.io/frontend/CSS-Transition/#transition-timing-function)과 동일







#### animation-iteration-count

정수로 지정 or infinite(무한 반복)







#### animation-direction

| Value               | 설명                                             |
| :------------------ | :----------------------------------------------- |
| `normal`            | from(0%)에서 to(100%) 방향으로 진행(default)     |
| `reverse`           | to에서 from 방향으로 진행                        |
| `alternate`         | 홀수 번째는 normal로, 짝수 번째는 reverse로 진행 |
| `alternate-reverse` | 홀수 번째는 reverse로, 짝수 번째는 normal로 진행 |

```html
  <style>
    .box1 {
      position: absolute;
      width: 100px;
      height: 100px;
      background: firebrick;
      border-radius: 5px;
      animation-name: move, fadeOut;
      animation-duration: 3s, 3s;
      animation-iteration-count: infinite;
      animation-direction: alternate;
    }
    @keyframes move {
      from {
        left: 0;
      }
      50% {
        left: 60px;
      }
      to {
        left: 200px;
      }
    }
    @keyframes fadeOut {
      from {
        opacity: 1;
      }
      to {
        opacity: 0;
      }
    }
  </style>
</head>
<body>
  <div class="box1"></div>
</body>
```

> ![animation_direction](/assets/ImagesForPosts/2021-04-14-CSS Animation/animation_direction.gif)







#### animation-fill-mode

| Value       | 상태 | 설명                                                        |
| :---------- | :--: | :---------------------------------------------------------- |
| `none`      | 대기 | 시작 프레임(from)에 설정한 스타일을 적용하지 않고 대기      |
|             | 종료 | 애니메이션 실행 전 상태로 요소의 프로퍼티값을 되돌리고 종료 |
| `forwards`  | 대기 | 시작 프레임(from)에 설정한 스타일을 적용하지 않고 대기      |
|             | 종료 | 종료 프레임(to)에 설정한 스타일을 적용하고 종료             |
| `backwards` | 대기 | 시작 프레임(from)에 설정한 스타일을 적용하고 대기           |
|             | 종료 | 애니메이션 실행 전 상태로 요소의 프로퍼티값을 되돌리고 종료 |
| `both`      | 대기 | 시작 프레임(from)에 설정한 스타일을 적용하고 대기           |
|             | 종료 | 종료 프레임(to)에 설정한 스타일을 적용하고 종료             |

✅ 즉!

- `none` : 처음 스타일 → [0% → 100%] → 처음 스타일
- `forwards` : 처음 스타일 → [0% → 100%] → 100%
- `backwards` : 0% → [0% → 100%] → 처음 스타일
- `both` : 0% → [0% → 100%] → 100%



```html
  <style>
    .box {
      position: relative;
      width: 100px;
      height: 100px;
      background: blue;
      color: red;
      border-radius: 5px;
      animation-name: move;
      animation-delay: 1s;
      animation-duration: 3s;
      animation-iteration-count: 1;
      animation-fill-mode: none;
    }
    @keyframes move {
      from {
        background: black;
        left: 0;
      }
      to {
        background: lightgreen;
        left: 200px;
      }
    }
  </style>
</head>
<body>
  <div class="box" style="animation-fill-mode: none">none</div>
  <br />
  <div class="box" style="animation-fill-mode: forwards">forwards</div>
  <br />
  <div class="box" style="animation-fill-mode: backwards">backwards</div>
  <br />
  <div class="box" style="animation-fill-mode: both">both</div>
</body>
```

> ![animation_fillmode](/assets/ImagesForPosts/2021-04-14-CSS Animation/animation_fillmode.gif)







#### animation-play-state

주로 JS와 함께 사용해서 이벤트에 따라 해당 값을 변경

- `paused` : 중지 상태
- `running` : 실행 상태(default)







#### animation 단축 property

```css
/* name, duration */
animation: move 2s;
/* name, duration, iteration-count */
animation: move 2s infinite;
/* name, duration, timing-function, delay */
animation: move 2s linear 3s
/* name, duration, timing-function, delay, iteration-count, direction, fill-mode, play-state */
animation: move 2s linear 3s infinite reverse forwards paused;
```