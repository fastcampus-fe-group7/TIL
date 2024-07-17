# Generator
Generator 함수

# Generator 정의
- 일반 함수는 `function()` 으로 선언하지만, 제너레이터 함수는 `function* ()`로 선언할 수 있다.

- 제너레이터 함수 안에서 `yield`를 통해 결과 값을 반환할 수 있으며, `return`과 다르게 여러번 선언하여 실행할 수 있다.

- `yield`를 통해 제너레이터 함수의 실행을 멈췄다 다시 시작 할 수 있게 만든다.

- generator 함수는 기본적으로 iterable 객체를 생성한다. 
<br>
따라서 `Symbol.iterator`메서드를 자동으로 구현하므로, 이를 통해 생성된 generator 객체는 별도의 Symbol.iterator 메서드를 명시적으로 정의하지 않아도 된다.

# Generator 함수의 장점

1. 비동기 특성을 동기적 코드방식으로 관리 해줍니다.
2. `iterator`와 `iterable`을 쉽게 사용 할 수 있습니다.
3. 제네레이터 함수는 코루틴 특성을 가지고 있습니다.
4. 제네레이터 함수는 동시적인 특성을 갖고 있습니다.
5. 제네레이터 함수는 비동기적 특성을 갖고 있습니다.
6. 메모리 효율에 기여할 수 있습니다.

# Generator 함수 사용법
## 예시
```javascript
  //generator 함수 선언
  function* generateSequence() {
    yield 1;
    yield 2;
    return 3;
  }

  let generator = generateSequence();

  //generator 함수 순회
  let one=generator.next();
  let two=generator.next();
  let three=generator.next();

  console.log(one);
  console.log(two);
  console.log(three);
```
  ## 결과
  ![image](https://github.com/user-attachments/assets/6c98ab22-68bc-4ed8-8750-061533aa041b)

# Iteration Protocol

`데이터 컬렉션을 순회`하기 위한 프로토콜이다. 이터레이션 프로토콜을 준수한 객체(iterable)는 `for...of` 문으로 순회할 수 있고, `Spread`문법의 피연산자가 될 수 있다.

* `spread 문법`이란, `배열이나 객체를 펼쳐서 개별 요소로 분리`하는 문법이다.

  ## 예시
  ```javascript
    const str1="fastcampus group7";
    const str2=[...str1];
    console.log(str2);
  ```

  ## 결과
  ![image](https://github.com/user-attachments/assets/8dd13615-fa75-4c8e-a45d-f56187f05421)
 
## iterable과 iterator
### iterator
`iterator`는 '반복자'라는 의미로, `iterable`의 요소를 탐색하기 위한 포인터이다.
1. `next 메서드`를 가지고 있어야하며, next 메서드를 호출할 때마다 순회할 때의 다음 값을 가진 객체를 반환해야 한다.

2. next 메서드는 {value: data, done: boolean} 형태의 객체를 반환해야한다. value는 현재 순회 중인 값, done은 순회 종료 여부이다. <br>
-> iterator 함수에 return이 존재하면 해당 순회의 done은 true이다.

### iterable
`iterable`은 `순회 가능한 자료구조`이다. <br>
  ->배열, 문자열, Map, Set, DOM 등이 `iterable`에 속한다.
1. `Symbol.iterator 메서드`를 가지고 있어야 한다. <br>
  ![image](https://github.com/user-attachments/assets/ee7d1492-838f-41ee-8ca3-d555f5230c5b)

    -> `iterator`를 반환하는 메서드

2. `for...of`문을 순회할 수 있으며, `Spread` 문법의 대상으로 사용할 수 있다.

### 예시
```javascript
  const iterable=['a','b','c'];
  const iterator=iterable[Symbol.iterator]();

  console.log(iterator.next()); // { value: 'a', done: false }
  console.log(iterator.next()); // { value: 'b', done: false }
  console.log(iterator.next()); // { value: 'c', done: false }
  console.log(iterator.next()); // { value: undefined, done: true }
```

```javascript
  function* generateSequence() {
    yield 1;
    yield 2;
    return 3;
  }
  let generator = generateSequence();
  for(let value of generator) { //generator의 반환값을 value에 저장
    console.log(value); // 1, 2
  }

```
`for...of`문이 `generator`의 `done`속성이 true일 때 반복을 종료하기 때문에, 3은 출력되지 않는다.  
# 결론
|분류|iterator|generator|
|---|---|---|
|구현 방식|next() 메서드 구현| function*()|
|상태 관리|직접 관리|yield|
|코드 복잡도|높음|낮음|
|Symbol.iterator 메서드|직접 구현|자동 구현|

iterator와 generator는 반복 가능한 객체를 생성하는 방법을 제공한다. iterator는 세세한 제어를 가능하게 하지만, generator는 코드의 간결함과 사용의 편리함을 제공하기에 상황에 맞게 선언하여 사용하면 될 것 같다.

# 출처
https://velog.io/@boyeon_jeong/%EC%9D%B4%ED%84%B0%EB%9F%AC%EB%B8%94-%EC%9D%B4%ED%84%B0%EB%A0%88%EC%9D%B4%ED%84%B0-%ED%94%84%EB%A1%9C%ED%86%A0%EC%BB%AC