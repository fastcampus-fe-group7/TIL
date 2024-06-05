# id와 class

<br>

id 선택자와 class 선택자는 모두 특정 HTML 요소에 이름을 붙여주어 개별적인 제어가 가능하도록 하는 용도로 사용되지만, 쓰임이 서로 다르다. 두 선택자의 차이점을 비교해보도록 한다.
<br>


## id 선택자

1. 특징

- 특정 요소 하나를 식별하기 위한 수단으로써 사용한다.
- HTML 문서 내에서 유일하며 단 하나의 요소에 대해서만 지정할 수 있다.
- 하나의 요소에는 단 하나의 id 선택자를 가질 수 있다.

2.  사용법

- 특정 요소 안에 id="값" 형태로 지정한다.
- `<div id="아이디명"></div>`
- #아이디명{ 스타일 : 값; }
### HTML
  ```html
  <p>id class 적용 X</p>
  <div id="man">남자</div>
  <div id="woman">여자</div>
  ```
 ### CSS
 ```css
  div{
    color:white;
  }

  #man{
    background-color:blue;
    width:10%
  }

  #woman{
    background-color:red;
    width:10%
  }
 ```
 ### 결과
  ![idvclass](https://github.com/fastcampus-fe-group7/TIL/assets/86473590/4dc66dfd-5c4e-4ee6-b268-99e29e7832df)

<br>

## class 선택자

1. 특징

- 여러 요소에 공통적으로 적용되는 스타일을 정의하는 수단으로 사용한다.
- HTML 문서 내, 여러 요소에 대해 지정할 수 있다.
- 하나의 요소는 여러 class 선택자를 가질 수 있다.

2. 사용법

- 특정 요소 안에 class="값" 형태로 지정한다.
- `<div class="클래스명"></div>`
- .클래스명{ 스타일 : 값; }

### HTML
```html
<p>일반적인 p 태그</p>
<p class="red">여기만 RED<p>
<div class="korean captine">손흥민</div>
<div class="korean">손흥민</div>
<div class="korean">황희찬</div>
<div class="korean">이강인</div>
<div class="korean">황인범</div>
```
  
 ### CSS
 ```css
p.red{
    color:red;
}

.korean{
    text-decoration:underline;
}

.captain{
    color:red;
}
 ```
  - `ABC.XYZ {}` : 복합 선택자 - 일치 선택자
    - 선택자 ABC와 XYZ를 동시에 만족시키는 요소를 선택
  - `복합 선택자`를 통해 두 가지 이상의 선택자를 만족시키는 요소를 따로 지정할 수 있다.
  
 ### 결과
  ![class-result1](https://github.com/fastcampus-fe-group7/TIL/assets/86473590/aaddb64f-9fe7-4a7c-8b77-ece48e3324ac)



  

3. 주의사항

- 하나의 요소가 여러 개의 class 선택자를 가질 경우, 선택자의 `우선순위`가 같다면 가장 뒤에 선언된 선택자의 속성을 따른다. `우선순위`가 다를 경우, 선택자가 선언된 순서에 관계없이 우선순위가 높은 선택자의 속성을 따른다.
- `선택자 우선순위` : !important(최우선) > inline (1000) > id (100) > class (10) > 태그 (1) > * (0)
  
## 우선순위가 같을 경우
 ### HTML
 ```html
 <div class="green bold">무슨 색?</div>
 <div class="bold green">무슨 색?</div>
 ```

 ### CSS
 ```css
 .green{  
    color:green;
 }

 .bold{
    color:brown;
    font-weight:bold;
 }

 ```

 ### 결과
  ![class-3-result](https://github.com/fastcampus-fe-group7/TIL/assets/86473590/9d9a935e-a7e5-4266-bc6c-75394572442e)
  
  -  요소 속성 내 선언된 순서와는 상관없이 bold의 내용이 적용된다.

## 우선순위가 다를 경우
### HTML
```html
<div id="red"
     class="orange"
     style="color:yellow">
  무슨색이 나올까?
</div>
```

### CSS
```css
div{
  color:blue !important;
}
#red{
  color:red;
}

.orange{
  color:orange;
}
```
### 결과
![image](https://github.com/unanbb/TIL/assets/86473590/bb4fb9c5-0d72-4442-867b-9ff77b4ec37e)

- `div`: 1점, `id`: 100점, `class`: 10점 으로  `id`의 속성이 선택되어야 하지만 `div`의 속성으로 `!important`를 주었으므로 `div`가 최우선이 된다.

## 부모-자식 관계일 경우
- 속성이 부모-자식 관계일 경우에는 선택자의 선언 순서에 관계 없이 자식의 속성으로 대체된다.
  
 ### HTML
```html
<div class="blue">
  <p class="green">무슨 색?</p>
</div>
```

 ### CSS
 ```css
 .green{
  color:green;
 }

 .blue{
  color:blue;
 }
 ```

 ### 결과
  ![child-result](https://github.com/fastcampus-fe-group7/TIL/assets/86473590/b119a93f-c4f9-483a-89f8-cd1a31469f83)

## 정리

[표]
|구분|id|class|
|---|---|---|
|목적|특정 요소 하나를 식별하는 수단|공통된 스타일을 정의하는 수단 |
|선언기호|#|.|
|다중사용|X|O|
|형태|<요소 id="아이디명">|<요소 class="클래스명">|
