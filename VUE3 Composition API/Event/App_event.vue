<template>
	<div>
		<button @click="printEventInfo('Hello Vue3', $event)">
			inline event handler
		</button>
		<hr />
		<input type="text" @keyup="onKeyupHandler" />
		<hr />
		<div id="modifiers">
			<div @click="clickDiv">
				DIV 영역
				<p @click.self="clickP">
					P 영역
					<!-- <span @click="clickSpan.stop"> SPAN 영역 </span> -->
					<span @click="clickSpan"> SPAN 영역 </span>
					<a href="https://naver.com" @click.prevent="clickA">a 영역</a>
				</p>
			</div>
		</div>
		<button @click="clickDiv">once</button>
	</div>
</template>

<script>
export default {
	setup() {
		const printEventInfo = (message, event) => {
			console.log('message: ', message);
			console.log('event.target: ', event.target);
			console.log('event.tagName: ', event.tagName);
		};
		const onKeyupHandler = () => {
			console.log('event.key: ', event.key);
		};

		const clickDiv = () => {
			console.log('clickDiv');
			// location.href = 'https://naver.com';
		};
		const clickP = () => {
			console.log('clickP');
		};
		const clickSpan = () => {
			console.log('clickSpan');
			// alert('like');
		};
		const clickA = e => {
			e.preventDefault();
			alert('어떤 기능');
		};

		return {
			printEventInfo,
			onKeyupHandler,
			clickDiv,
			clickP,
			clickSpan,
			clickA,
		};
	},
};
</script>

<style scoped>
#modifiers div,
#modifiers p,
#modifiers span {
	padding: 40px;
}
#modifiers div {
	background-color: #ccc;
}
#modifiers p {
	background-color: #999;
}
#modifiers span {
	background-color: #666;
	display: block;
}
</style>
