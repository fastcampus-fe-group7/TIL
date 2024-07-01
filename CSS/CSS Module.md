# CSS Module
## Intro
MPA(Mulit Page Application)에서는 각 HTML 파일마다 별도의 CSS 파일을 링크해 스타일을 적용하는 것이 일반적이므로 CSS 클래스와 애니메이션 이름이 충돌날 경우가 드물다. 그러나 React와 같은 모던 자바스크립트 프레임워크와 같이 SPA(Single Page Application) 경우, 애플리케이션의 규모가 커질수록 여러 컴포넌트에서 사용된 CSS 클래스명이 서로 중복될 가능성이 높아진다. 이 때 유용한 것이 CSS Module이다.

---

## CSS Module
CSS Module은 컴포넌트 기반의 스타일링을 가능하게 해주는 CSS 파일의 특별한 형태이다. 기본적으로 CSS 클래스 이름을 지역적으로 범위를 지정하여, 전역 네임스페이스에서 충돌하지 않도록 보호한다.

CSS Module을 적용하는 방법은 매우 간단하다. 아래와 같이 특정 모듈만을 위한 CSS 파일을 설정할 수 있다. 
1. CSS Module 파일 (`styles.module.css`):
```
[모듈명].module.css
```
2. JavaScript 파일
```js
import styles from "파일 경로";
//...
<div class="{styles.[클래스명]}">...</div>
```
이렇게 하면 `styles.module.css`의 클래스 이름이 컴파일 시 고유한 해시값으로 변경되어, 다른 CSS 클래스와 충돌하지 않게 된다.

<img width="500" alt="image" src="https://github.com/Dev-FE-1/Toy_Project_Team_1/assets/93127663/8a883376-46cb-48df-8731-04eb3215ba30">

---

## CSS Module 장단점
### 장점
1. 동일한 클래스명의 재정의로 인한 스타일의 전역 오염을 미연에 방지할 수 있음
2. 자동으로 고유한 클래스명으로 변환해주기 때문에 클래스명을 짓기 위한 개발자의 고민을 줄여줄 수 있음
3. 컴포넌트 단위로 스타일을 관리할 수 있어서 스타일의 유지보수가 편함

### 단점
1. 모듈마다 별도의 CSS 파일을 작성해야 하기 때문에 별도로 많은 CSS 파일을 만들어 관리해야 함. 
2. 클래스를 동적으로 추가할 경우 최종 렌더링된 결과물에서 자동 변환된 클래스명이 코드의 가독성을 어지럽히는 경우가 종종 발생
3. 작은 프로젝트에서는 설정과 사용이 다소 번거로울 수 있음

---

## CSS Module 작동 원리
CSS Module이 생성한 고유 클래스 이름을 원래 클래스 이름과 매핑하는 역할은 모듈 번들러(Webpack, Vite 등)가 담당한다.

### 1. CSS 파일 작성
개발자는 CSS Module 파일 `styles.module.css` 에 일반 CSS 코드를 작성

### 2. 로컬 스코핑 및 해싱
번들러는 CSS Module을 처리할 때, 각 클래스 이름을 고유한 이름(보통 해시값)을 추가하여 변환<br>
예를 들어, `styles.module.css`에서 `.container` 클래스가 `styles__container___1a2b3c`와 같은 고유한 이름으로 변환됨

### 3. JavaScript로 변환
번들러는 변환된 클래스 이름을 JavaScript 객체(`styles`)로 매핑한다. 이 객체는 CSS 파일을 `import`할 때 사용됩니다.

### 4. 스타일 적용
컴포넌트 내에서 CSS Module을 `import`하고, 매핑된 고유 클래스 이름을 사용하여 스타일을 적용

<img width="680" alt="image" src="https://github.com/Dev-FE-1/Toy_Project_Team_1/assets/93127663/6aa2c710-86a9-4a5e-9759-3de99557c9c5">

---

## 주의 사항
### 1. CSS Module는 클래스만 전역 네임스페이스에서 충돌하지 않도록 보호한다.
`id`와 태그 선택자의 경우, CSS Module의 영향을 받지 않는다. `id`의 경우, 고유한 값이므로 따로 styles 객체와 상관이 없다. 오히려 CSS Module 파일 내에 작성 시, 예상치 못한 결과를 초래할 수 있다.  

### 2. `styles['wrapper-line']`
객체의 속성에 접근할 때와 클래스 명이 동일하게 하이픈(-)이 포함되어 있으면 객체 접근 시 대괄호 표기법([])을 사용해야한다.
```js
import styles from "파일 경로";
//...
<div class="{styles['wrapper-line']">...</div>
```
---

## 참고자료
1. [CSS Module](https://www.tcpschool.com/react/react_styling_cssmodule)