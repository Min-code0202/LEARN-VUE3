<template>
	<div>
		<input type="text" @keyup="addTodo" />
		<input type="text" @keyup.enter="addTodo2" />
		<ul>
			<li v-for="(todo, index) in todos" :key="index">{{ todo }}</li>
		</ul>
	</div>
</template>

<script>
import { reactive } from 'vue';

export default {
	setup() {
		const todos = reactive([]);
		const addTodo = e => {
			console.log('event.key', event.key);
			if (event.key === 'Enter') {
				todos.push(e.target.value);
				e.target.value = '';
				e.target.focus();
			}
		};
		const addTodo2 = e => {
			console.log('event.key', event.key);
			todos.push(e.target.value);
			e.target.value = '';
			e.target.focus();
		};
		return { todos, addTodo, addTodo2 };
	},
};
</script>

<style lang="scss" scoped></style>
