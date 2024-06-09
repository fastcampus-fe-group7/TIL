# overflow

프론트엔드 개발을 하다보면, 설정된 영역보다 많은 양의 컨텐츠를 보여줘야 하는 경우가 종종 생긴다. <br>
➡ 이러한 상황에서, 설정된 영역을 넘치는 컨텐츠를 보여주는 방식에 대해 정의하는 CSS 속성이 바로 `overflow`이다.<br>

`overflow`에 대한 기본 개념과 사용법, 그리고 주의 사항에 대해 알아보자.

## 🎈overflow의 속성값

> overflow : 값;

스타일시트 내, 선택자 내부에 "overflow : 값" 형태로 지정한다.

- `visible(기본 값)`<br>
  ➡ 설정된 영역에 상관없이 모든 컨텐츠를 보여준다.
- `hidden`<br>
  ➡ 설정된 영역에 보이는 부분만 보여주고, 넘친 부분은 잘라낸다.
- `scroll`<br>
  ➡ 스크롤 바를 생성하여 넘친 부분을 보여준다.
- `auto `<br>
  ➡ **넘친 부분이 존재하는 경우**에만 스크롤 바를 생성하여 넘친 부분을 보여준다.
- ~~`clip`~~

## 🎈overflow의 활용

### 1) `overflow`를 설정하지 않았을 때

### 🦴 HTML

```html
<div class="container">
  <p>
    이 편지는 영국에서 최초로 시작되어 1년에 지구 한 바퀴를 돌면서 받는 사람에게
    행운을 주었고 지금은 당신에게로 옮겨진 이 편지는 4일 안에 당신 결을 떠나야
    합니다. 이 편지를 포함해서 7통을 행운이 필요한 사람에게 보내주셔야 합니다.
    복사를 해도 좋습니다. 혹 미신이라고 하실지 모르지만 사실입니다. 만약 보내지
    않으신다면 당신은 7일 내에..
  </p>
</div>
```

### 🌈 CSS

```css
.container {
  width: 300px;
  height: 100px;
  background-color: pink;
}
```

### 💡 결과

![image](https://github.com/fastcampus-fe-group7/TIL/assets/86473590/fb6b05ae-8f28-4330-9176-9dced2b4500d)

- `width`와 `height`로 설정한 영역에서 벗어나는 부분이 그대로 노출된다.

### 2) `overflow`를 설정했을 때 - hidden

### 🌈 CSS

```css
.container {
  width: 300px;
  height: 100px;
  background-color: pink;
  /* hidden */
  overflow: hidden;
}
```

### 💡 결과

![image](https://github.com/fastcampus-fe-group7/TIL/assets/86473590/aad77a5e-9277-45db-ad13-1567bd42ece3)

- container로 설정한 영역을 넘어서는 부분부터 내용이 잘리는 것을 볼 수 있다.

## 🎈overflow-x와 overflow-y

> `overflow-x` : x축(수평) 방향의 overflow를 제어<br> `overflow-y` : y축(수직) 방향의 overflow를 제어

각각 overflow의 하위속성으로, 하나의 축에 대한 overflow를 제어할 수 있다.
일반적인 상황에서 두 속성 정의시, 별 다른 충돌 없이 두 속성이 모두 적용된다.

### CSS

```css
.container {
  width: 300px;
  height: 100px;
  background-color: pink;
  overflow-x: scroll;
  overflow-y: hidden;
}
```

### 결과

![image](https://github.com/fastcampus-fe-group7/TIL/assets/86473590/23906840-dc15-4bd5-b2c5-223e082fe1e9)

- x축 방향에는 scroll이, y축 방향에는 hidden이 정상적으로 적용된 모습이다.

## 🎈overflow-x와 overflow-y 주의사항

W3C의 "CSS Overflow Module Level 3" 문서의 3.1을 보면 이런 사항이 적혀있다.

> "The visible/clip values of overflow compute to auto/hidden (respectively) if one of overflow-x or overflow-y is neither visible nor clip."

❗ (의역) 만약, `overflow-x`나 `overflow-y`중 하나가 visible도 clip도 아닌 다른 값 (hidden, scroll, auto)이라면, visible은 auto, clip은 hidden으로 계산된다.<br>
➡ 무슨 말이냐면..

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="JjqyLJy" data-pen-title="overflow-excption" data-user="unanlee" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/unanlee/pen/JjqyLJy">
  overflow-excption</a> by leeyunhwan (<a href="https://codepen.io/unanlee">@unanlee</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

위와 같이 overflow-x가 auto(visible이 아닌 값), overflow-y가 visible 값을 가질 경우, overflow-y의 값은 auto로 변경된다.<br>
➡ 따라서 부모로부터 y축 방향으로 넘친 영역(🟦blue area)이 visible 처리되지않고, auto로 처리되어 스크롤이 생성된 모습을 띠게된다.

## 결론

일반적인 사항에선 `overflow-x`와`overflow-y`가 별다른 충돌없이 병합되나, 위와 같은 예외사항에선 아래와 같이 작동된다.

- `overflow-x`: visible, `overflow-y`: auto <br>-> `overflow-x`: auto, `overflow-y`: auto

- `overflow-x`: visible, `overflow-y`: scroll <br>-> `overflow-x`: auto, `overflow-y`: scroll

- `overflow-x`: visible, `overflow-y`: hidden <br>-> `overflow-x`: auto, `overflow-y`: hidden

- `overflow-x`: clip, `overflow-y`: auto <br>-> `overflow-x`: hidden, `overflow-y`: auto

- `overflow-x`: clip, `overflow-y`: scroll <br>-> `overflow-x`: hidden, `overflow-y`: scroll

- `overflow-x`: clip, `overflow-y`: hidden <br>-> `overflow-x`: hidden, `overflow-y`: hidden

[표]

| <center>값</center>      | <center>의미</center>                           |
| ------------------------ | ----------------------------------------------- |
| <center>visible</center> | <center>**그대로** 보여줌</center>              |
| <center>hidden</center>  | <center>넘치는 부분만 **삭제**</center>         |
| <center>scroll</center>  | <center>**스크롤** 생성(**항상**)</center>      |
| <center>auto</center>    | <center>**스크롤** 생성(**넘칠 때만**)</center> |

## 참고

https://www.w3.org/TR/css-overflow-3/
