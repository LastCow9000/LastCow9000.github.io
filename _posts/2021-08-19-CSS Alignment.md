---
title: 'CSS Alignment'
toc : true
toc_sticky: true
categories: [Frontend]
tags: [Web, CSS, Alignment]
---



# CSS 정렬



## 요약 정리


###### div 박스 내의 텍스트를 가운데 정렬하려면?
```css
- 수평 →  text-align: center
- 수직 →  line-height: {height에 설정한 높이값과 동일한 값(height: 80px 라면 80px)}
```


###### flex 관련 가운데 정렬
```css
- 수평 → justify-content: center
- 수직 → align-content: center
```







## 1. 수평 정렬



### inline/inline-block 요소

정렬 대상 요소(inline/inline-block)의 **부모 요소**에 `text-align: center`

```css
<style>
  div {
    text-align: center;
  } 
</style>
<body>
  <p style="font-size: 30px">css alignment</p>
  <div class="container">
    <a href="#">inline align1</a>
    <span>inline align3</span>정렬을 해보자!
  </div>
</body>
```

![스크린샷 2021-08-19 오전 4.16.34](/assets/ImagesForPosts/2021-08-19-CSS Alignment/스크린샷 2021-08-19 오전 4.16.34.png)




### block 요소
1. 정렬 대상 요소에 너비를 명시적으로 지정
2. `margin-right`와 `margin-left`에 `auto`

> 너비를 명시적으로 지정하지 않으면?
>
> 너비는 full width가 되므로 중앙 정렬이 필요X

```css
<style>
  .block {
    width: 300px;
    margin: 0 auto;
  }
  .box {
    height: 300px;
    width: 300px;
    background-color: burlywood;
  }
</style>
<body>
  <p style="font-size: 30px">css alignment</p>
  <div class="container">
    <div class="block">inline align1</div>
    <p class="block">정렬을>inline align3</p>
    <div class="box block"></div>
    정렬을 해보자!
  </div>
</body>
```

![스크린샷 2021-08-19 오전 4.25.01](/assets/ImagesForPosts/2021-08-19-CSS Alignment/스크린샷 2021-08-19 오전 4.25.01.png)





### 여러개의 block 요소

- 아래와 같이 기본적으로 수직 정렬됨. 

![스크린샷 2021-08-19 오후 7.47.09](/assets/ImagesForPosts/2021-08-19-CSS Alignment/스크린샷 2021-08-19 오후 7.47.09.png)



- 요소들을 수직 정렬말고 수평 정렬 하려면 inline-block 요소로 변경 후 부모 요소에 `text-align: center`

```css
<style>
  p,
  .container {
    text-align: center;
  }
  .block {
    display: inline-block;
    height: 300px;
    width: 300px;
    background-color: burlywood;
  }
</style> 
<body>
  <div class="container">
    <p style="font-size: 30px">css alignment</p>
    <div class="block">inline align1</div>
    <p class="block">정렬을>inline align3</p>
  </div>
</body>
```

![스크린샷 2021-08-19 오후 7.49.18](/assets/ImagesForPosts/2021-08-19-CSS Alignment/스크린샷 2021-08-19 오후 7.49.18.png)









## 2. 수직 정렬



### inline/inline-block 요소

---

#### a. 정렬 대상의 부모 요소에 padding-top과 padding-bottom 값을 동일하게 지정
```css
<style>
  .container {
    padding: 50px;
  }
</style>
<body>
  <div class="container">
		<a class="child" href="#">single line</a><span class="child">vertical_alignment Lorem 			ipsum dolor, sit amet consectetur adipisicing elit. Accusamus alias quibusdam excepturi 		laboriosam eligendi. Id officia itaque laboriosam voluptatem, dolores eligendi 							accusantium, molestias non atque voluptate nam ipsam, rerum cupiditate?</span>
	</div>
</body>
```

![스크린샷 2021-08-19 오후 8.11.31](/assets/ImagesForPosts/2021-08-19-CSS Alignment/스크린샷 2021-08-19 오후 8.11.31.png)



#### b. padding이 지정 불가능한 요소일 경우 height와 line-height 값을 같게 지정(여러 줄 일경우 행간이 너무 넓어져서 X)

```css
<style>
  .container {
    height: 300px;
    line-height: 300px;
  }
</style>
<body>
  <div class="container">
		<a class="child" href="#">single line</a>ertical_alignment Lorem ipsum dolor, sit amet 			consectetur adipisicing elit.
	</div>
</body>
```

![스크린샷 2021-08-19 오후 8.23.51](/assets/ImagesForPosts/2021-08-19-CSS Alignment/스크린샷 2021-08-19 오후 8.23.51.png)



### block 요소

---

#### 가운데 정렬
부모 요소를 기준으로 절대 위치를 지정한

1. 요소의 높이가 정해져 있을 경우 
   - `margin-top`을 높이의 반만큼 - 값 지정
2. 요소의 높이가 정해져 있지 않을 경우
   - `transform: translateY(-50%)`



- 수평 정렬도 같이 하려면 `margin-left`를 추가하거나 `transform: translateY(-50%, -50%)` 

```css
  <style>
    .box {
      width: 200px;
      height: 200px;
      background-color: blueviolet;
    }
    .parent {
      position: relative;
    }
    .child {
      position: absolute;
      top: 50%;

      margin-top: -100px;
      /* transform: translateY(-50%); */
    }
  </style>
  <body>
    <div class="container">
      <div class="box child">a</div>
    </div>
  </body>
```

<img src="/assets/ImagesForPosts/2021-08-19-CSS Alignment/스크린샷 2021-08-19 오후 8.38.33.png" alt="스크린샷 2021-08-19 오후 8.38.33" style="zoom:50%;" />













## 3. Flexbox


### inline/inline-block 요소 수평 정렬

정렬 대상 부모 요소에 아래와 같이 지정

```css
.parent {  
  display: flex;  
  justify-content: center; 
}
```





### inline/inline-block 요소 수직 정렬

정렬 대상 부모 요소에 `justify-content: center` 와 `flex-direction: column` 를 지정하고 높이를 지정

```css
<style>
  .box {
    width: 200px;
    height: 200px;
    background-color: blueviolet;
  }
  .parent {
    display: flex;
    justify-content: center;
    flex-direction: column;
    height: 500px; /* 높이 지정 */
  }
  p {
    display: inline-block;
  }
</style>
<body>
  <div class="parent">
    <p>Lorem, ipsum dolor sit amet consectetur adipisicing elit. Et aut eaque, repellendus neque voluptates expedita quisquam mollitia dignissimos possimus quasi beatae facilis libero eligendi quos eius voluptatum autem accusamus maxime?</p>
  </div>
</body>
```

![스크린샷 2021-08-19 오후 8.51.03](/assets/ImagesForPosts/2021-08-19-CSS Alignment/스크린샷 2021-08-19 오후 8.51.03.png)





### block 요소 수직 정렬

정렬 대상 부모 요소에 아래와 같이 지정

```css
.parent {
  display: flex;
  flex-direction: column;
  justify-content: center; /* 없어도 됨 */
}
```



```css
<style>
  .box {
    width: 200px;
    background-color: blueviolet;
  }
  .parent {
    display: flex;
    flex-direction: column;
  }
</style>
<body>
  <div class="parent">
    <p>문자열이닷</p>
    <div class="box">AA</div>
    <h3>헤더태그</h3>
  </div>
</body>
```



![스크린샷 2021-08-19 오후 9.13.00](/assets/ImagesForPosts/2021-08-19-CSS Alignment/스크린샷 2021-08-19 오후 9.13.00.png)





### 수평 가운데, 요소내 수직 가운데 정렬

정렬 대상 부모 요소에 아래와 같이 지정

```css
.parent {
  display: flex;
  align-items: center;
  justify-content: center;
}
```



```css
<style>
  .box {
    width: 200px;
    background-color: blueviolet;
  }
  .parent {
    display: flex;
    align-items: center;
    justify-content: center;
  }
</style>
<body>
  <div class="parent">
    <p>문자열이닷</p>
    <div class="box">AA</div>
    <h3>헤더태그</h3>
  </div>
</body>
```



![스크린샷 2021-08-19 오후 9.17.28](/assets/ImagesForPosts/2021-08-19-CSS Alignment/스크린샷 2021-08-19 오후 9.17.28.png) 





- `align-items: center` 미 지정 시

![스크린샷 2021-08-19 오후 9.15.14](/assets/ImagesForPosts/2021-08-19-CSS Alignment/스크린샷 2021-08-19 오후 9.15.14.png)





### 수평 가운데, 요소내 수직 가운데, 요소간 수직 가운데 정렬

정렬 대상 부모 요소에 아래와 같이 지정

```css
.parent {
  display: flex;
  align-items: center;
  flex-direction: column;
}
```



```css
<style>
  .box {
    width: 200px;
    background-color: blueviolet;
  }
  .parent {
    display: flex;
    align-items: center;
    flex-direction: column;
  }
</style>
<body>
  <div class="parent">
    <p>문자열이닷</p>
    <div class="box">AA</div>
    <h3>헤더태그</h3>
  </div>
</body>
```

![스크린샷 2021-08-19 오후 9.31.00](/assets/ImagesForPosts/2021-08-19-CSS Alignment/스크린샷 2021-08-19 오후 9.31.00.png)

![스크린샷 2021-08-19 오후 9.32.37](/assets/ImagesForPosts/2021-08-19-CSS Alignment/스크린샷 2021-08-19 오후 9.32.37.png)

