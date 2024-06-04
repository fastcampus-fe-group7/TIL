# relative와 absolute

## 목표

CSS 속성 중 `position`이라는 속성이 있고, 그 중 `relative`와 `absolute` 이 두 가지 값이 가장 난이도가 높다.
**1)기준**과 **2)문서 흐름(Content-Flow)** 두 가지 관점에서 두 속성값을 이해해보자.

## relative

### 1. 기준의 관점

요소의 **원래 위치**를 기준으로 한다.

- 여기서 중요한 점은, content, padding, border를 포함한 **전체 박스 모델**를 기준으로 하는 것이다.
- `top`, `right`, `bottom`, `left` 4가지 속성을 사용하여 원래 위치에서 상대적으로 이동시킨다.

#### 원래 위치 (위치 속성이 0인 경우)

<img width="150" alt="image" src="https://github.com/red-dev-Mark/TIL/assets/93127663/8b12b8e8-1ed0-4821-8fa6-f3d4e9bebbe8">

#### `top: 20px;` 인 경우

<img width="150" alt="image" src="https://github.com/red-dev-Mark/TIL/assets/93127663/d855a93a-3b6b-476f-937b-2bb126599a7b">

#### `top: 20px; right: 90px;` 인 경우

<img width="150" alt="image" src="https://github.com/red-dev-Mark/TIL/assets/93127663/1ec61fe4-d1b3-4f22-a5ac-616218ec30b2">


### 2. 문서 흐름(Content-Flow)의 관점

요소를 문서의 일반적인 흐름(Content-Flow)에 따라 배치한다.

- 이는 블록 레벨 요소와 인라인 요소의 배치 방식를 따른다는 의미이다.

### 3. relative 정리

**1)요소를 문서의 일반적인 흐름에 따라 배치**한 다음, top, right, bottom, left 속성에 따라 **2)원래 요소 위치에서 상대적으로 이동**시킨다.

---

## absolute

### 1. 기준의 관점

요소를 부모 요소의 위치에서 분리하고, 가장 가까운 조상 요소 중 `position`이 `relative`, `absolute`인 요소를 기준으로 이동한다.

- 만약 이러한 조상 요소가 없다면, `body` 요소 기준이 됨.
- top, right, bottom, left를 줘야 이동
  - `position: abosolute`만 주면 아무런 변화가 생기지 않는다.

#### absolute 추가 Tip

##### 1. 더 엄밀히 하면, **부모 요소의 padding box**가 기준

- padding box: content 영역과 padding을 포함한 영역.
- border과 padding 경계를 기준으로 한다.
  - 이 의미는 top, right을 0으로 해도 부모의 border는 가려지지 않는다는 것

##### 2. top, right, bottom, left이 적용되지 않는 곳은 `padding`의 영향을 받는다.

- 부모 요소 `padding: 20px`, 자식 요소 `top:0`, `left:0`인 경우 (이해를 돕기 위해 부모 요소 `border: 10px`)
    - 적용이 되었기에 자식 요소는 부모 요소의 padding을 무시한다.<br>
    <img width="170" alt="image" src="https://github.com/red-dev-Mark/TIL/assets/93127663/49b0f1d1-f68f-4d5f-bf41-8e25d24a8d2c">
- 부모 요소 `padding: 20px`, 자식 요소 `top:0`, `right:0`인 경우
    - 적용이 되었기에 자식 요소는 부모 요소의 padding을 무시한다.<br>
    <img width="170" alt="image" src="https://github.com/red-dev-Mark/TIL/assets/93127663/40f2f6c9-0b62-41f9-91b7-31e37f2b08a3">
- 부모 요소 `padding: 20px`, 자식 요소 `top`만 0인 경우
    - 오른쪽을 제외한, 왼쪽 padding 영향만 받은 이유는 Content-Flow 때문이다.<br>
    <img width="170" alt="image" src="https://github.com/red-dev-Mark/TIL/assets/93127663/bfe8d3b3-caaf-445a-954c-ccf38b99465b">

##### 3. `top`, `right`, `bottom`, `left`이 모두 0일 경우, Content-Flow의 영향을 받는다.
- `top`과 `bottom`이 같이 0이면 `top`이 우세
- `right`과 `left`이 같이 0이면 `left`이 우세


### 2. 문서 흐름(Content-Flow)의 관점
요소를 일반적인 문서 흐름에서 제거하고, 위치를 절대적으로 배치한다.
- 위와 같이, 요소는 가장 가까운 위치의 지정 조상 요소를 기준으로 배치한다.
- 다른 요소들은 absolute로 설정된 요소가 차지하던 공간을 인식하지 않는다.

### 3. absolute 정리

**1)일반적인 문서 흐름에서 제거**한 다음, top, right, bottom, left 속성에 따라 **2)지정된 조상 요소를 기준으로 절대적으로 이동**시킨다. 문서 흐름에서 제거되므로, **3)그 자리에 다른 요소들이 위치할 수 있다.**
