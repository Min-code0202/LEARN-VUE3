# Composition API란?
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
# Composition API의 장점

Composition API를 사용하면 동일한 논리적 관심사 코드를 그룹화할 수 있어, 코드를 분석하기 쉽고 유지보수가 용이하다. 또한 논리적 관심사 코드를 외부 유틸리티 파일로 추출하기도 쉽다.

## 코드 재사용성

Composition API의 가장 큰 장점은 [**Composable 함수**](https://vuejs.org/guide/reusability/composables.html)를 통해 로직을 재사용할 수 있다는 점이다.  
Options API의 기본 재사용 메커니즘인 Mixin이 가지고 있던 단점을 해결할 수 있다.

Composition API의 재사용 기능은 커뮤니티에서 발전된 여러 프로젝트를 만들어냈다:

- [**VueUse**](https://vueuse.org/): 구성 가능한 유틸리티 함수들의 모음
- [**immutable data**](https://vuejs.org/guide/extras/reactivity-in-depth.html#immutable-data)
- [**state machines**](https://vuejs.org/guide/extras/reactivity-in-depth.html#state-machines)
- [**RxJS**](https://vueuse.org/rxjs/readme.html#vueuse-rxjs): Vue의 반응성 시스템과 쉽게 통합 가능

### Composition API는 Options API의 주요 제한 사항을 해결한다:

- Hook을 사용하여 관련 코드 조각을 함께 그룹화할 수 있다.
- Composable 함수를 통해 애플리케이션 전역에서 코드를 쉽게 재사용할 수 있다.

---

## TypeScript

Composition API는 TypeScript와 자연스럽게 통합되며, 타입 추론과 정의가 뛰어나다. Options API보다 유연하게 타입을 정의할 수 있다.
