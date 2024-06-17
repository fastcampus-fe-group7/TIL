# BEM 방법론

## 사전 지식

- HTML의 요소에 스타일을 적용하기 위해 CSS의 선택자를 사용한다. 선택자의 종류에는 태그 선택자, 아이디(ID)선택자, 클래스(Class) 선택자 등이 있다.

## 개념 및 사용법

- CSS 선택자 중 하나인 클래스 선택자의 네이밍 방법론 방식 중 하나로, CSS를 조직화하고 유지보수하기 쉽게 만든다.
- BEM은 Block, Element, Modifier의 각 첫 글자를 따서 지어진 이름이다.
  - 블록(Block)
    - 독립적으로 재사용 가능한 UI 구성 요소를 의미함
    - ex : 메뉴, 버튼, 헤더 등
  - 요소(Element)
    - 블록 내의 특정 부분을 나타내며 블록 없이 존재할 수 없음
    - ex : 메뉴의 항목(탭), 버튼의 텍스트, 헤더의 로고 등
  - 수정자(Modifier)
    - 블록이나 요소의 모양, 상태, 동작을 변경하는데 사용
    - ex : 활성화 상태(active), 크기 변경(large), 색상 변경(red) 등

### 네이밍 규칙

- 블록(Block)
  ```css
  .block {
    /* 스타일 */
  }
  ```
- 요소(Element)
  ```css
  .block__element {
    /* 스타일 */
  }
  ```
- 수정자(Modifier)
  ```css
  .block__element--modifier {
    /* 스타일 */
  }
  ```

### 사용 예시

- 메뉴 컴포넌트

  ```html
  <!-- 메뉴 컴포넌트 구성 (메뉴 블록 - 리스트/아이템/버튼 요소 - 활성화 수정자) -->
  <nav class="menu">
    <ul class="menu__list">
      <li class="menu__item">
        <button class="menu__button menu__button--active">Home</button>
      </li>
      <li class="menu__item">
        <button class="menu__button">About</button>
      </li>
      <li class="menu__item">
        <button class="menu__button">Contact</button>
      </li>
    </ul>
  </nav>
  ```

  ```css
  /* 메뉴 블록 */
  .menu {
    background-color: #f8f9fa;
    padding: 10px;
    border-radius: 5px;
  }

  /* 메뉴 블록의 리스트 요소 */
  .menu__list {
    list-style: none;
    margin: 0;
    padding: 0;
    display: flex;
    gap: 10px;
  }

  /* 메뉴 블록의 아이템 요소 */
  .menu__item {
    list-style: none;
  }

  /* 메뉴 블록의 버튼 요소 */
  .menu__button {
    background-color: #007bff;
    color: white;
    border: none;
    padding: 10px 20px;
    border-radius: 5px;
    cursor: pointer;
  }

  /* 메뉴 블록의 버튼 요소의 활성화 수정자 */
  .menu__button--active {
    background-color: #0056b3;
  }
  ```

### 주의사항

- 수정자 클래스만 사용하면 안됨

  ```html
  <!-- 잘못된 방식 -->
  <button class="btn--secondary"></button>

  <style>
    .btn--secondary {
      display: inline-block;
      color: green;
    }
  </style>

  <!-- 올바른 방식 -->
  <button class="btn btn--submit"></button>

  <style>
    .btn {
      display: inline-block;
      color: blue;
    }
    .btn--submit {
      color: green;
    }
  </style>

  <!-- 기본 블록 요소인 btn의 스타일을 정의한 뒤, 확장하는 형태로 수정자를 사용해야 함 -->
  ```

- 오직 하나의 기본 블록과 하나의 요소 이름만 허용함

  ```html
  <!-- 잘못된 방식 -->
  <nav class="menu">
    <ul class="menu__list">
      <li class="menu__list__item">
        <button class="menu__list__item__button">Home</button>
      </li>
    </ul>
  </nav>

  <!-- menu__list__item은 잘못된 사용임 -->
  <!-- menu__list__item__button도 마찬가지로 잘못됨 -->

  <!-- 올바른 방식 -->
  <nav class="menu">
    <ul class="menu__list">
      <li class="menu__item">
        <button class="menu__button">Home</button>
      </li>
    </ul>
  </nav>

  <!-- menu라는 하나의 블록을 기준으로 각각의 내부 요소별 클래스로 나뉨 -->
  <!-- 따라서, menu__item, menu__button의 형태로 사용함 -->
  ```

- 블록이 다른 블록의 요소로 포함될 수 있음

  ```html
  <div class="card">
    <div class="card__header">
      <h2 class="card__title">Card Title</h2>
    </div>
    <div class="card__body">
      <p class="card__text">This is some content inside the card.</p>
    </div>
    <div class="card__footer">
      <!-- btn 블록이 card 블록의 요소인 button임 -->
      <button class="btn card__button">Action</button>
    </div>
  </div>
  ```

  ```css
  /* 카드 블록 스타일 */
  .card {
    border: 1px solid #ccc;
    padding: 16px;
    border-radius: 8px;
    max-width: 300px;
    margin: 20px auto;
    background-color: #fff;
  }

  .card__header {
    margin-bottom: 16px;
  }

  .card__title {
    font-size: 24px;
    margin: 0;
  }

  .card__body {
    margin-bottom: 16px;
  }

  .card__text {
    font-size: 16px;
  }

  .card__footer {
    text-align: right;
  }

  /* 버튼 블록 스타일 */
  .btn {
    padding: 10px 20px;
    font-size: 16px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    background-color: #007bff;
    color: white;
    transition: background-color 0.3s ease;
  }

  /* 카드 안의 버튼 스타일 */
  .card__button {
    /* card__button은 기본적으로 버튼 블록(.btn) 스타일을 상속 받으며,
  	  카드 블록 버튼 요소에 추가적인 스타일이 필요할 경우 해당 위치에 작성 */
  }
  ```

## BEM 방법론의 장점

- CSS 클래스 네이빙 방식에 일관성을 유지할 수 있기 때문에 여러 개발자가 참여하는 프로젝트에서 코드 가독성을 높이고 유지보수를 용이하게 함
- 코드의 모듈성을 높일 수 있기 때문에 각 블록, 요소, 수정자는 독립적으로 작동하며 특정 부분을 수정하거나 재사용하기 쉬움
- 명확한 구조를 제공하기 때문에 각 코드가 어떤 역할을 하는지 쉽게 파악할 수 있음
- 확장성이 뛰어나기 때문에 새로운 기능이나 디자인 요구사항이 생기더라도 쉽게 추가할 수 있음

## BEM 방법론의 단점

- 깊은 구조의 컴포넌트를 가진 경우, 클래스 명이 길어질 수 있기 때문에 코드 작성 시, 혹은 유지보수 시 번거로울 수 있음
- 팀 전체가 BEM 방법론을 일관되게 적용하지 않으면, 오히려 혼란을 초래할 수 있음
- 프로젝트 규모에 따라 BEM의 구조와 체계성이 과도하고 불필요하게 느껴질 수 있음
