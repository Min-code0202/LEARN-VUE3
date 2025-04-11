<template>
	<div>
		<h2>Reactive</h2>
		<button v-on:click="increment">Click {{ state.count }}</button>
		<button v-on:click="increment">Deep Click {{ state.deep.count }}</button>
		<hr />
		<h2>Reactive vs Ref</h2>
		<p>{{ message.value }}</p>
		<!-- ref로 선언한 반응형 객체는 자동으로 언래핑됨(.value 불필요)-->
		<p>{{ refMessage }}</p>
		<button v-on:click="addMessage">add click</button>
		<hr />
		<h2>Destructuring</h2>
		<p>author: {{ author }}</p>
		<p>title: {{ title }}</p>
		<p>author2: {{ author2 }}</p>
		<p>title2: {{ title2 }}</p>
		<p>year: {{ year }}</p>
		<hr />
		<h2>readonly</h2>
	</div>
</template>

<script>
import { reactive, readonly, ref, toRef, toRefs } from 'vue';

export default {
	setup() {
		const state = reactive({
			count: 0,
			deep: {
				count: 0,
			},
		});
		// let message = reactive('Hello');
		// 반응형으로 동작 X
		// 'Hello'는 문자열(primitive type)이기 때문
		// 반응형으로 하고 싶다면 아래처럼 객체로 생성
		let message = reactive({
			value: 'Hello',
		});
		console.log('message: ', message.value);
		console.log('message typeof: ', typeof message.value);

		let refMessage = ref('Hello');

		// ref -> Object
		const count = ref(0);
		const state2 = reactive({
			count, // == count: count
		});
		console.log(count.value); // 0
		console.log(state2.count.value); // undefine
		// ref로 선언한 데이터를 반응형 객체 속성으로 주입하면 자동으로 언래핑
		console.log(state2.count); // 0

		// ref -> Array
		const message2 = ref('Hello');
		const arr = reactive([message2]);
		console.log('arr[0]: ', arr[0].value);

		// Destructuring
		const book = reactive({
			author: 'Vue Team',
			year: '2020',
			title: 'Vue 3 Guide',
			description: '당신은 이 책을 지금 바로 읽습니다 ;)',
			price: '무료',
		});

		let { author, title } = book; // author, title은 반응성을 잃고 primitive type이 됨

		// reactive destructuring
		let { author2, title2 } = toRefs(book);
		let year = toRef(book, 'year');
		const increment = () => {
			state.count++;
			state.deep.count++;
		};
		const addMessage = () => {
			message.value = message.value + '!';
			refMessage.value = refMessage.value + '!';
		};

		// readonly
		const original = reactive({
			count: 0,
		});
		original.count++;
		console.log(original.count);

		const copy = readonly(original);
		copy.count++;
		console.log(copy.count); // readonly로 복사했기 때문에 경고 표시됨

		return {
			state,
			increment,
			message,
			addMessage,
			refMessage,
			state2,
			message2,
			arr,
			author,
			title,
			author2,
			title2,
			year,
		};
	},
};
</script>

<style lang="scss" scoped></style>
