# useState 타입 정의

## Intro
React는 JavaScript의 라이브러리로, 모든 React 기능은 결국 JavaScript의 개념에서 파생되었거나, JavaScript로 구현되어 있다. 그러면서 React의 대표 Hook인 `useState` 또한 JavaScript로 구현할 수 있을 것이라 예상해, 직접 구현해보기로 했다.

이번에는 구현 전, `useState` 함수가 어떻게 구성되어 있는지 먼저 알아보자.

---

## useState 타입 정의
먼저 React 프로젝트에서 `useState`의 타입 정의를 보면 아래와 같다.
1. React `useState` 코드
```jsx
const [count, setCount] = useState(0)
```
2. TypeScript로 작성된 `useState`의 타입 정의
```ts
function useState<S>(initialState: S | (() => S)): [S, Dispatch<SetStateAction<S>>];
```

---

## 제네릭 타입 매개변수
자세한 타입 정의를 알아보기 전, 먼저 제네릭 타입 매개변수에 대해 알면 좋다.
클래스, 인터페이스, 메서드 등을 정의할 때 사용되는 타입 플레이스홀더로, 코드 재사용성 및 타입 안정성을 높이는 데 도움을 준다.

여기서 사용되는 알파벳은 특별한 의미가 없다. 즉 어떤 알파벳이든 사용할 수 있지만, 관례적으로 많이 사용되는 알파벳들이 있다. 관례를 따르면 코드의 가독성을 높이는 데 도움이 될 수 있다.

1. T: "Type"의 약자로, 가장 일반적으로 사용된다.
2. E: "Element"의 약자로, 컬렉션의 요소 타입을 나타낼 때 주로 사용된다.
3. K: "Key"의 약자로, 맵의 키 타입을 나타낼 때 사용된다.
4. V: "Value"의 약자로, 맵의 값 타입을 나타낼 때 사용된다.
5. N: "Number"의 약자로, 숫자 관련 타입에 사용된다.
6. S: "State"나 "String"의 약자로 사용된다.
7. A: "Any"의 약자로, 어떤 타입이든 될 수 있음을 나타낸다.

---

## 타입 정의 자세히 알아보기
그럼 다시 타입 정의에 대해 조금 더 자세히 뜯어보자.

`<S>`: 제네릭 타입 매개변수로 **상태의 타입**을 나타낸다.

`initialState: S | (() => S)`: **초기 상태의 값을 받는 매개변수**이다.
- `S` 타입의 값이거나 `S` 타입의 값을 반환하는 함수이다.

`[S, Dispatch<SetStateAction<S>>]`: **`useState` 함수의 반환 타입**을 나타낸다.
- 배열의 형태로 두 개의 요소를 반환한다.
    - `S`: 현재 상태 값
    - `Dispatch<SetStateAction<S>>`: 상태를 업데이트하는 함수

---

`Dispatch<SetStateAction<S>>` 또한 자세히 뜯어보자.
1. `Dispatch`: 상태를 업데이트하는 함수의 형태를 정의한다.

```ts
type Dispatch<A> = (value: A) => void;
```

- `<A>`: 제네릭 타입 매개변수로, 함수가 받을 인자의 타입을 나타낸다.
- `(value: A) => void`: `A` 타입의 값을 인자로 받고, 아무것도 반환하지 않는 함수를 의미한다.
- `'void'`는 함수가 명시적인 반환 값이 없다는 것을 나타낸다.

---

2. `<SetStateAction<S>>`: 상태 설정 액션(상태를 업데이트하는 방식을 나타내는 개념)의 형태를 정의한다.
```ts
type SetStateAction<S> = S | ((prevState: S) => S);
```

- `<S>`는 제네릭 타입 매개변수로, 상태의 타입을 나타냅니다.
- `S | ((prevState: S) => S)`: 다음 두 가지 중 하나임을 의미한다.
    - `S`: 새로운 상태 값
    - `(prevState: S) => S`: 이전 상태를 인자로 받아 새 상태를 반환하는 함수

위의 두 타입을 조합되면서, `useState`의 반환 타입인 `[S, Dispatch<SetStateAction<S>>]`이 된다.

`Dispatch<SetStateAction<S>>`
- 새로운 상태 값 (`S` 타입)
- 이전 상태를 받아 새 상태를 반환하는 함수 (`(prevState: S) => S` 형태)

---

### Dispatch와 SetStateAction
여기서 Dispatch와 SetStateAction의 차이가 모호할 수 있으나, React 상태 관리 시스템에서 서로 다른 역할을 하는 타입이다.

둘의 차이는 아래와 같다.
#### Dispatch
1. 상태를 업데이트하는 함수의 타입을 정의하는 역할을 한다.
2. 항상 함수 타입이다.
3. 인자를 받아 실제로 상태를 변경하는 동작을 수행한다.
4. 반환값이 없다. (void)

#### SetStateAction
1. 상태를 어떻게 업데이트할지 정의하는 액션의 타입 역할을 한다.
2. 값 또는 함수일 수 있다.
3. 실제 상태 변경을 수행하지 않고, 어떻게 변경할지를 정의한다.

즉, `SetStateAction`는 `Dispatch`가 상태를 업데이트하는데 있어, 어떻게 업데이트할지를 정의하는 역할을 한다. 또 `Dispatch`가 `useState`의 두 번째 요소의 타입으로 사용된다면, `SetStateAction`은 `Dispatch` 함수의 인자 타입으로 사용된다.

---

## 타입 정의를 통한 `useState` 동작 알아보기
위 타입 정의를 보면 `useState`가 다음과 같이 동작함을 알 수 있다.
1. `useState`는 초기 상태 값(`initialState`) 혹은 초기 상태를 생성하는 함수(`(() => S)`)를 받는다.

2. 현재 상태 값(`S`)과 그 상태를 업데이트할 수 있는 함수(`Dispatch<SetStateAction<S>>`), 두 가지 요소를 배열로 반환한다.

3. 상태 업데이트 함수(`Dispatch<SetStateAction<S>>]`)는 새 상태 값(`S`)을 직접 받거나, 이전 상태를 기반으로 새 상태를 계산하는 함수(`(prevState: S) => S`)를 받을 수 있다.

---

## 요약
다시 돌아가 React의 `useState`는 아래와 같이 구성되어 있다.
```jsx
const [count, setCount] = useState(0)
```

여기서 `useState`는 타입 정의를 보면, 다음과 같다는 것을 알 수 있다.
```ts
// 초기 상태의 값을 받는 매개변수
0 === `initialState: S | (() => S)`
```

`useState`이 반환하는 타입 정의를 보면 아래와 같다.
```ts
// 초기 상태의 값을 받는 매개변수
[count, setCount] === [S, Dispatch<SetStateAction<S>>]
```
즉 `count`는 `S` 타입 정의를 갖는 현재 상태 값이고, `setCount`는 `Dispatch<SetStateAction<S>>`의 타입 정의를 갖는 상태를 업데이트하는 함수이다.

여기서 더 들어가보면,
```ts
type Dispatch<A> = (value: A) => void;
type SetStateAction<S> = S | ((prevState: S) => S);
```
`setState`는 `A` 제네틱 타입 매개변수를 통해 다양한 타입의 값을 처리할 수 있고, 반환값이 없다.

`<SetStateAction<S>>` 타입 정의를 통해 새로운 상태 값 또는 이전 상태를 인자로 받아 새 상태를 반환하는 함수를 인자로 받을 수 있다.

---

## Outro
`useState`는 React의 대표적인 Hook으로 자주 사용한다. 그런데 이 함수의 타입 정의와 동작 원리에 대해서는 깊게 고민해본 적이 없다. 이번 타입 정의를 보면서도 useState 초기값에 값이 아닌 함수를 인자로 전달할 수 있다는 것과, 또한 setState에 함수가 아닌 새로운 값을 넣을 수 있다라는 것을 알게 되었다. 다음에는 Vanilla JS로 `useState`를 구현해보면서 동작 원리를 알아보자.