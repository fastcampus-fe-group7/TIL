# 이벤트 핸들링
- 이벤트란, 사용자가 웹 브라우저에서 DOM 요소들과 상호 작용하는 행위를 말한다.
- React의 이벤트 처리는 DOM의 이벤트 처리 방식과 유사하지만, 몇 가지 문법 차이가 있다.

1. 이벤트 이름은 카멜케이스로 작성한다.<br>
  HTML에서는 요소에 이벤트를 직접 작성할 때 `<button onclick="alert("버튼이 눌렸습니다.")>버튼</button>`와 같이 `onclick`이라는 별도의 표기법이 없는 상태로 사용하지만, React에서는 `onClick`과 같이 카멜케이스로 작성해야 한다.

2. 이벤트에는 함수 형태의 값을 전달한다.<br>
  HTML에서 이벤트를 설정할 때 `""`안에 실행할 코드를 직접 선언해 주었지만, React에서는 함수 형태의 객체를 전달한다. 화살표 함수나 외부에 미리 선언한 함수를 가져오기도 한다.
    ```jsx
      const handleEvent= ()=>{
        alert('클릭!');
      }; 
      // HTML에서 이벤트 처리 방식
      <button onclick='handleEvent()'>Event</button>
      
      // React의 이벤트 처리 방식
      // 방법 1
      <button onClick={handleEvent}>Event</button>
      // 방법 2
      <button onClick={()=> alert('클릭!')}>Event</button>
    ```

3. DOM 요소에만 이벤트를 설정할 수 있다.<br>
  `div`, `button`, `input` 등과 같은 DOM 요소에는 이벤트를 설정할 수 있지만, 직접 만든 리액트 컴포넌트에는 이벤트를 자체적으로 설정할 수 없다.
    ```html
      <myComponent onClick={doEvent}/>
    ```

## onClick
- `onClick` 이벤트는 **클릭**이라는 행위를 처리할 때 사용하는 이벤트이다.
- 주로 `<button>`이나 `<a>` 태그와 같이 **클릭**이라는 특정 행위에 웹이 반응해야 할 때 사용한다.

```jsx
  function App() {

  return (
    <div className="App">
      <h1>onClick Practice</h1>
      <button onClick={() => alert('클릭!')}>Button</button>
    </div>
  );
}
```

## onChange
`<input>`, `<textarea>`, `<form>`, `<select>`와 같은 **폼 요소**들은 사용자의 입력값을 받아 제어하는 요소들이다.
- onChange 이벤트는 이러한 입력 필드의 값을 **변경**할 때 발생하는 이벤트이다.
- 사용자가 입력 필드에 값을 입력하고 삭제할 때마다 이벤트가 발생하기 때문에, 실시간으로 값을 업데이트 해야할 때 사용한다.

```jsx
  function App() {
  const [name, setName] = useState("");
  
  const handleChange = (e) => {
  	setName(e.target.value);
  };
  
  return (
  	<div>
      <h1>onChange Practice</h1>
      <input type='text' value={name} onChange={handleChange} />
      <h1>{name}</h1>
    </div>
  ); 
};
```