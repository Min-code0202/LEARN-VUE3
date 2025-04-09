# LEARN-VUE3
VUE3를 공부하고 기록한 리포지토리입니다.

## VUE란?
>User Interface 개발을 위한 **자바스크립트 프레임워크**이다.
>[VUE의 핵심 기능](https://github.com/Min-code0202/LEARN-VUE3/tree/master/VUE%EC%9D%98%20%EA%B8%B0%EB%8A%A5)
## 설치방법
* CDN: head 태그에 아래 코드를 추가하면 된다.
```
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
```
* npm [here](./Vue%20설치방법/REAMME.md)
* CLI [here](./Vue%20설치방법/REAMME.md)
* Vite [here](./Vue%20설치방법/REAMME.md)

## 컴포넌트 (Component)
>자바스크립트에서 재사용할 수 있도록 코드를 분리한 파일을 *모듈*이라고 하는데 Vue에서도 마찬가지로 UI(HTML, CSS, JS)를 재사용할 수 있도록 정의한 것을 *컴포넌트*라고 한다.
   
### 컴포넌트를 사용하는 이유
* 컴포넌트를 사용하면 UI를 재사용 할 수 있다.
* 컴포넌트를 사용하여 UI를 독립적으로 나눔으로써(레이아웃 등) 코드를 클린하게 할 수 있다.

### [컴포넌트 사용법](https://github.com/Min-code0202/LEARN-VUE3/tree/master/%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8%20%EC%9D%B4%ED%95%B4)
  
## Options API vs Composition API 비교
| 항목         | Options API              | Composition API                 |
|--------------|--------------------------|----------------------------------|
| 구조         | `data`, `methods` 등 분리 | 관련 로직을 함수로 묶어 구성      |
| 가독성       | 초보자에게 직관적         | 익숙해지면 더 명확함               |
| 재사용성     | Mixin 사용 (제한적)       | `Composable` 함수로 뛰어남         |
| 타입스크립트 | 제약 있음                 | 최적화되어 있음                    |
| 규모 확장    | 커지면 관리 어려움        | 대규모 프로젝트에 유리             |
| 진입장벽     | 낮음                      | 다소 높음                          |
  
해당 프로젝트에선 주로 `Composition API`를 사용하므로 `Options API`에 대해서는 간단하게 코드상으로만 알아보겠다.
```js
<template>
	<div>
		<button @click="increment">Counter: {{ counter }}</button>
	</div>
</template>

<script>
export default {
	data() {
		return {
			counter: 0,
		};
	},
	methods: {
		increment() {
			this.counter++;
		},
	},
	mounted() {
		console.log('애플리케이션이 마운트 되었습니다!');
	},
};
</script>

<style lang="scss" scoped></style>
```
### ✅ 언제 무엇을 쓰면 좋을까?

- **작고 단순한 컴포넌트** → Options API
- **복잡한 로직 / 대규모 프로젝트** → Composition API
- **타입스크립트를 함께 사용할 경우** → Composition API
  
## Composition API란?
Composition API는 옵련(`data`, `methods`, `mounted`)을 선언하는 대신 가져온 함수(`ref`, `onMounted`)를 사용하여 Vue 컴포넌트를 작성할 수 있는 API 세트를 말한다.  
[Vue3 API Reference](https://vuejs.org/api/)
```
<script setup>
import { onMounted, reactive, ref } from 'vue';

const counter = ref(0);
const increment = () => {
	counter.value++;
};

const books = reactive([]);
const addBook = (title, author) => {
	books.push({ title, author });
};

onMounted(() => {
	console.log('애플리케이션이 마운트 되었습니다!');
});
</script>
```
## Composition API의 장점

Composition API를 사용하면 동일한 논리적 관심사 코드를 그룹화할 수 있어, 코드를 분석하기 쉽고 유지보수가 용이하다. 또한 논리적 관심사 코드를 외부 유틸리티 파일로 추출하기도 쉽다.

### 코드 재사용성

Composition API의 가장 큰 장점은 [**Composable 함수**](https://vuejs.org/guide/reusability/composables.html)를 통해 로직을 재사용할 수 있다는 점이다.  
Options API의 기본 재사용 메커니즘인 Mixin이 가지고 있던 단점을 해결할 수 있다.

Composition API의 재사용 기능은 커뮤니티에서 발전된 여러 프로젝트를 만들어냈다:

- [**VueUse**](https://vueuse.org/): 구성 가능한 유틸리티 함수들의 모음
- [**immutable data**](https://vuejs.org/guide/extras/reactivity-in-depth.html#immutable-data)
- [**state machines**](https://vuejs.org/guide/extras/reactivity-in-depth.html#state-machines)
- [**RxJS**](https://vueuse.org/rxjs/readme.html#vueuse-rxjs): Vue의 반응성 시스템과 쉽게 통합 가능

#### Composition API는 Options API의 주요 제한 사항을 해결한다:

- Hook을 사용하여 관련 코드 조각을 함께 그룹화할 수 있다.
- Composable 함수를 통해 애플리케이션 전역에서 코드를 쉽게 재사용할 수 있다.

---

### TypeScript

Composition API는 TypeScript와 자연스럽게 통합되며, 타입 추론과 정의가 뛰어나다. Options API보다 유연하게 타입을 정의할 수 있다.

---

### 번들 크기 감소 및 오버헤드 최소화

Composition API는 최종 번들 크기를 줄이고 불필요한 오버헤드를 줄이는 데에도 도움이 된다.

---

## [Options API와의 관계](https://vuejs.org/guide/extras/composition-api-faq.html#does-composition-api-cover-all-use-cases)

### Composition API로 기존 모든 사용 사례를 커버할 수 있는가?

Composition API만으로 대부분의 기능을 구현할 수 있다.  
다만, 다음과 같은 몇 가지 옵션은 여전히 필요할 수 있다:

- `props`
- `emits`
- `name`
- `inheritAttrs`

`<script setup>`을 사용할 경우, 일반적으로 `inheritAttrs`만 명시적으로 지정해주면 된다.

---

### 두 API를 함께 사용할 수 있는가?

가능하다. Options API 컴포넌트 내에서 `setup()` 함수를 통해 Composition API를 사용할 수 있다.  
다만, 기존 코드베이스가 Options API로 작성되어 있거나, Composition API 기반 외부 라이브러리와 통합해야 하는 경우에 사용하는 것이 일반적이다.

---

### Options API가 deprecated 될 예정인가?

아니다.  
Vue 팀은 Options API를 계속 지원할 계획이며, 많은 개발자들이 여전히 단순하고 직관적인 Options API를 선호한다.  
Composition API의 장점은 주로 대규모 프로젝트에서 부각되며, Options API는 복잡도가 낮거나 중간 수준의 프로젝트에 여전히 적합한 선택지이다.
