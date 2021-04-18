---
title: 'CSS Inheritance'
toc : true
toc_sticky: true
categories: [Frontend]
tags: [Web, CSS, Inheritance]
---



##	Inheritance

요소간엔 부모와 자식관계가 있고 상속은 상위(부모, 조상) 요소에 적용된 property 값을 하위(자식, 자손) 요소가 물려 받는 것을 의미함

> 생산성을 높일 수 있지만 복잡한 상속관계로 인해 복잡도가 올라갈 수 있기 때문에 우선순위 확인이 필요함



🦝예제

```html
  <style>
    .inherit {
      color: red;
      border: 3px solid yellowgreen;
      padding: 30px;
    }
  </style>
</head>
<body>
  <div class="inherit">
    <p>상속 테스트</p>
    <strong>상속이 되는가?</strong><br />
    <button>버튼</button>
  </div>
</body>
```

> ![image-20210418192034989](/assets/ImagesForPosts/2021-04-18-CSS Inheritance/image-20210418192034989.png)
>
> - color property 값은 p태그와 strong태그에 상속됨
> - border property, padding property 값은 부모에만 적용되었을뿐 자식 요소들에게 상속되지 않음(상속이 되었다면 각 태그에 태두리가 생겨야함)
> - button 태그는 상속받지 못함







#### 주요 property의 상속 여부

- 가능 :  visibility, opacity, color, font, text-align, line-height, white-space
- 불가능 : width/height, margin, padding, border, box-sizing, display, background, vertical-align, position(top/bottom/left/right), z-index, overflow, float







#### 강제 상속 설정 (inherit)

상속되지 않는 property 값을 상속하고 싶을 때 자식 요소에 해당 property를 `inherit` 으로 설정하면 됨

```html
  <style>
    .inherit {
      color: red;
      border: 3px solid yellowgreen;
      padding: 30px;
    }
    button {
      color: inherit;
    }
    strong {
      border: inherit;
    }
  </style>
</head>
<body>
  <div class="inherit">
    <p>상속 테스트</p>
    <strong>상속이 되는가?</strong><br />
    <button>버튼</button>
  </div>
</body>
```

> ![image-20210418193320159](/assets/ImagesForPosts/2021-04-18-CSS Inheritance/image-20210418193320159.png)
>
> - strong 태그에 border와 button 태그에 color가 상속됨







### Cascading과 CSS 우선순위

---

 요소는 다양한 CSS property 적용과 상속으로 인해 하나 이상의 CSS가 적용될 수 있다. 이때 충돌을 피하기 위해 <u>CSS 적용 우선순위</u>를 정해놓고 이에 기반하여 특정 요소에 적용될 property 값을 정함

🎈이를 **캐스캐이딩(Cascading Order)**이라고 함





#### cascading의 3가지 규칙

1. 중요도
   - CSS가 어디에 선언 되었는가에 따라 우선순위가 달라짐
2. 명시도
   - 적용 대상을 명확하게 특정할수록 명시도가 높아지고 우선순위가 높아짐
3. 선언 순서
   - HTML 문서 뒤쪽에 있는 CSS 일수록 우선순위가 높음







#### 중요도

1 순위 : head 태그 내의 style 요소

2 순위 : head 태그 내의 style 태그 내의 @import문

3 순위 : `<link>` 로 연결된 CSS 파일

4 순위 : `<link>`로 연결된 CSS 파일 내의 @import문

5 순위 : 브라우저 default 스타일시트







#### 명시도

- 우선순위 계산에 가장 큰 영향을 미침

> **!important > 인라인 스타일 > 아이디 선택자 > 클래스/어트리뷰트/가상 선택자 > 태그 선택자 > 전체 선택자 > 상위 요소에 의해 상속된 속성**



##### 명시도 계산법

- id 선택자의 갯수 * 100

- class/attribute/pseudo class 선택자의 갯수 * 10

- tag/pseudo-element 선택자의 갯수 * 1

  ➕ 각각의 값을 더해서 계산 (점수가 동일할 경우 중요도와 선언 순서에 따라 적용됨)

 참고 : [명시도 계산 사이트](https://specificity.keegan.st/)

> 💯ex)
>
> - ul#primary-nav li.active	= 112
> - nav > a:hover::before	= 013 
> - h1.tmp.table#gra	= 121





#### 선언 순서

나중에 선언된 스타일이 우선 적용됨
