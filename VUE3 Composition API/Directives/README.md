## 디렉티브 (directives)
디렉티브는 `v-` 로 시작하는 **Vue 전용 속성**이다.  
HTML 요소에 특별한 **기능이나 동작**을 부여하는 역할을 한다.

예를 들어:
```html
<h1 v-if="isVisible">안녕하세요!</h1>
```

위 코드는 `isVisible`이 `true`일 때만 `<h1>`을 보여준다.  
`v-if`는 "보여줘!" 라고 HTML에게 지시하는 것이다.

---

## 자주 쓰는 내장 디렉티브들

| 디렉티브       | 설명 |
|----------------|------|
| `v-text`       | 텍스트를 삽입합니다 |
| `v-html`       | HTML 코드를 삽입합니다 |
| `v-show`       | 보여주기/숨기기를 CSS로 처리합니다 |
| `v-if`         | 조건이 참일 때만 렌더링합니다 |
| `v-else`       | 위 조건이 거짓일 때 실행됩니다 |
| `v-else-if`    | `if`가 아니고 다른 조건일 때 실행됩니다 |
| `v-for`        | 목록을 반복해서 보여줍니다 |
| `v-on`         | 이벤트를 처리합니다 (예: 클릭) |
| `v-bind`       | HTML 속성을 Vue 데이터와 연결합니다 |
| `v-model`      | 양방향 바인딩 (입력 양식 등에서 사용) |
| `v-slot`       | 슬롯을 정의할 때 사용합니다 |
| `v-pre`        | 이 영역은 Vue가 무시하게 합니다 |
| `v-once`       | 한 번만 렌더링하고, 다시 렌더링 안함 |
| `v-cloak`      | Vue가 준비될 때까지 숨김 |
| `v-memo (3.2+)`| 렌더링을 캐싱하여 성능 향상 |

---

## 디렉티브 구성
```html
v-on:submit.prevent="onSubmit"
```

각 부분 설명:

- `v-on` → 디렉티브 이름 (이벤트 처리)
- `submit` → 이벤트 이름
- `.prevent` → 수식어: 기본동작 막기
- `"onSubmit"` → 실행할 메서드 이름

---

## 🎨 동적 전달인자

HTML 속성 이름도 **동적으로 바꿔야 할 때** 이렇게 쓸 수 있다:

```html
<a v-bind:[attributeName]="url">링크</a>
```

`attributeName`이 `"href"`이면 결국 `v-bind:href="url"` 과 같아요.

---

## 커스텀 디렉티브
Vue는 직접 디렉티브를 만들 수도 있다. 
예: 엘리먼트에 자동으로 포커스를 주는 `v-focus` 디렉티브 만들기.

더 보기 👉 [Vue 공식 문서 - Custom Directives](https://vuejs.org/guide/reusability/custom-directives.html)

---

## 참고 링크:
- [Vue 공식 문서 (EN)](https://vuejs.org/guide/essentials/template-syntax.html#directives)
- [Vue 3 한국어 문서](https://v3.ko.vuejs.org/api/directives.html#v-text)
