<template>
	<div>
		<h2>{{ teacher.name }}</h2>
		<h3>강의가 있습니까?</h3>
		<p>{{ teacher.lectures.length > 0 ? '있음' : '없음' }}</p>
		<p>{{ hasLecture }}</p>
		<p>{{ existLecture() }}</p>
		<p>{{ hasLecture }}</p>
		<p>{{ existLecture() }}</p>
		<button v-on:click="counter++">Counter: {{ counter }}</button>
		<h2>이름</h2>
		<p>{{ fullName }}</p>
		<p>{{ fullName2 }}</p>
	</div>
</template>

<script>
import { computed, reactive, ref } from 'vue';

export default {
	setup() {
		const teacher = reactive({
			name: 'min',
			lectures: ['HTML/CSS', 'JavaScript', 'Vue3'],
		});

		// 아래 두 코드 모두 기능은 같지만 computed가 비용이 적게듦
		// computed는 계산 된 값이 캐시되기 때문
		const hasLecture = computed(() => {
			console.log('computed');
			return teacher.lectures.length > 0 ? '있음' : '없음';
		});

		const existLecture = () => {
			console.log('method');

			return teacher.lectures.length > 0 ? '있음' : '없음';
		};

		const counter = ref(0);

		let firstName = ref('홍');
		let lastName = ref('길동');
		// const fullName = computed(() => firstName.value + ' ' + lastName.value);
		// console.log('Console 출력: ', fullName.value);
		// fullName.value = '김 철수'; // 콘솔에 경고 표시뜸, computed는 readonly이기 때문
		const fullName = computed({
			get() {
				return firstName.value + ' ' + lastName.value;
			},
			set(value) {
				console.log('value: ', value);
				console.log(value.split(' '));
				[firstName, lastName] = value.split(' ');
				console.log('first: ', firstName);
				console.log('last: ', lastName);
			},
		});
		console.log('Console 출력: ', fullName.value);
		fullName.value = '김 철수';

		return {
			teacher,
			hasLecture,
			existLecture,
			counter,
			firstName,
			lastName,
			fullName,
		};
	},
};
</script>

<style lang="scss" scoped></style>
