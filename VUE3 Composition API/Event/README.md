# Vue 이벤트 처리 정리

Vue에서는 DOM 이벤트를 처리하기 위해 `v-on` 디렉티브를 사용한다. 자주 사용되므로 `@`으로 축약해서 사용할 수 있다.

---

## 기본 이벤트 처리

```js
const counter = ref(0);
```

```html
<div>
  <button @click="counter += 1">counter {{ counter }}</button>
</div>
```

---

## 메소드 이벤트 핸들러

```js
const printEventInfo = (event) => {
  console.log(event.target);
  console.log(event.target.tagName);
};
```

```html
<button @click="printEventInfo">printEventInfo</button>
```

---

## 이벤트 객체 접근

```js
const printEventInfo2 = (message, event) => {
  console.log('message:', message);
  console.log(event.target);
  console.log(event.target.tagName);
};
```

```html
<button @click="printEventInfo2('hello world', $event)">
  inline event handler
</button>
```

---

## 이벤트 수식어 (Modifiers)

Vue는 자주 사용하는 `event.preventDefault()` 또는 `event.stopPropagation()` 같은 메서드를 위한 수식어를 제공한다.

- `.stop` = 이벤트 전파 중단
- `.prevent` = 기본 동작 방지
- `.capture` = 캡처 단계에서 처리
- `.self` = 이벤트 타겟이 자신일 때만 실행
- `.once` = 이벤트가 한 번만 실행
- `.passive` = 성능 개선용 수식어 (특히 스크롤 이벤트)

```html
<a @click.stop="doThis">링크 클릭 방지</a>
<form @submit.prevent="onSubmit">제출 방지</form>
<a @click.stop.prevent="doThat">두 개 수식어</a>
<form @submit.prevent></form>
<div @click.capture="doThis">캡처 단계</div>
<div @click.self="doThat">자기 자신일 때만 실행</div>
<div @scroll.passive="onScroll">성능 최적화</div>
```

---

## 키보드 키 수식어

특정 키를 처리하기 위한 수식어:

- `.enter`
- `.tab`
- `.delete`
- `.esc`
- `.space`
- `.up`, `.down`, `.left`, `.right`

```html
<input type="text" @keyup.enter="addTodo" />
```

---

## 시스템 키 수식어

- `.ctrl`
- `.alt`
- `.shift`
- `.meta` (Mac: ⌘, Windows: ⊞)

```html
<input @keyup.alt.enter="clear" />
<input @keyup.ctrl.enter="send" />
<div @click.ctrl="doSomething">Ctrl + 클릭</div>
```

---

## `.exact` 수식어

정확한 키 조합일 때만 이벤트 실행:

```html
<!-- Alt나 Shift와 같이 눌려도 실행됨 -->
<button @click.ctrl="onClick">A</button>

<!-- Ctrl만 눌렸을 때만 실행됨 -->
<button @click.ctrl.exact="onCtrlClick">A</button>

<!-- 아무 시스템 키 없이 눌렸을 때만 실행 -->
<button @click.exact="onClick">A</button>
```

---

## 마우스 버튼 수식어

- `.left`
- `.right`
- `.middle`

```html
<button @click.left="handleLeftClick">왼쪽 클릭</button>
<button @click.right="handleRightClick">오른쪽 클릭</button>
<button @click.middle="handleMiddleClick">가운데 클릭</button>
```

---

Vue 이벤트 처리는 굉장히 직관적이고 간단하다. `v-on` 또는 `@`을 사용해서 빠르게 반응형 이벤트 로직을 작성할 수 있고, 수식어(modifiers)를 활용하면 깔끔하게 비즈니스 로직과 분리된 이벤트 조작이 가능하다.
