<template>
	<div v-memo="[subscribers, views]">
		<p>{{ msg }}</p>
		<p v-text="msg"></p>
		<p v-html="htmlStr"></p>
		<p v-text="htmlStr"></p>
		<p v-once>{{ msg }} !!!</p>
		<hr />
		<p>subscribers: {{ subscribers }}</p>
		<p>views: {{ views }}</p>
		<p>likes: {{ likes }}</p>
		<button @:click="subscribers++">Subs++</button>
		<button v-on:click="views++">Views++</button>
		<button v-on:click="likes++">Likes++</button>
	</div>
</template>

<script>
import { ref } from 'vue';

export default {
	setup() {
		const msg = ref('Hello');
		const htmlStr = ref('<strong>Hello</strong>');
		const subscribers = ref(4000);
		const views = ref(400);
		const likes = ref(200);

		return { msg, htmlStr, subscribers, views, likes };
	},
};
</script>

<style lang="scss" scoped></style>
