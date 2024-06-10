# JavaScript 비동기처리
- 자바스크립트는 싱글스레드 언어이기 때문에 한번에 하나의 작업만 수행할 수 있다.(동기적 처리)
- 동기처리 방식을 사용하는 웹페이지는 처리중 페이지가 멈추는 것 처럼 보이기 때문에 사용자경험 측면에서 문제가 발생할 수 있다.
- 이를 보완하기 위해 비동기적으로 처리할 수 있는 기능을 제공하고 있다.
- 자바스크립트가 지원하는 비동기처리 방식을 알아보자.

## Promise
- Promise는 ES6에 추가된 기능으로 내용은 실행되었지만 결과를 아직 반환하지 않은 객체를 말한다.
- 3가지 상태(Pending(대기) / Fulfilled(성공) / Rejected(실패))를 가지고 있다.
- .then()으로 Fulfilled상태의 로직을 실행한다. .then()을 연계해 연속적인 비동기 처리가 가능하다.
- .catch()로 Rejected상태의 로직을 실행한다.

### 예제
```javascript
const myPromise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("foo");
  }, 300);
});

myPromise
  .then((value) => `${value} and bar`)
  .then((value) => `${value} and bar again`)
  .then((value) => `${value} and again`)
  .then((value) => `${value} and again`)
  .then((value) => {
    console.log(value);
  })
  .catch((err) => {
    console.error(err);
  });
```

## Async/Await
- ES8(ES2017)에 추가된 기능으로 callback, Promise보다 더 직관적이고 단순한 코드를 작성할 수 있다.
- async함수는 항상 promise를 반환한다.
- await는 async함수에서만 유효하며, await가 없는 async함수는 동기적으로 실행된다. await가 있다면 비동기적으로 실행된다.
- Promise와 다르게 에러핸들링이 지원되지 않아 try-catch문을 통해 에러핸들링을 해야한다.

### 예제
```javascript
// Promise.fulfilled 예시
function resolveAfter2Seconds(x) {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve(x);
    }, 2000);
  });
}

async function f1() {
  var x = await resolveAfter2Seconds(10);
  console.log(x); // 10
}

f1();

// Promise.reject 예시
async function f3() {
  try {
    var z = await Promise.reject(30);
  } catch (e) {
    console.log(e); // 30
  }
}
f3();

```

## 정리
- async/await는 앞선 비동기처리 방식인 callback, Promise를 보완하기 위해 나온 기능이다.
- async함수를 선언해도 await없이 사용한다면 동기적처리가 가능하다.
- async함수가 Promise를 반환하므로 Promise의 사용법도 알아두도록 하자.

## 참고자료
- [비동기 JavaScript - MDN](https://developer.mozilla.org/ko/docs/Learn/JavaScript/Asynchronous)
- [await - MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/await)

