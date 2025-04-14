<template>
	<div>
		<h2>input Value</h2>
		<!-- v-on을 사용해 양방향 바인딩 하는법
		<input
			type="text"
			:value="inputValue"
			@input="event => (inputValue = event.target.value)"
		/>
		-->
		<input type="text" v-model.lazy="inputValue" />
		<p>{{ inputValue }}</p>
		<hr />
		<h2>textarea value</h2>
		<textarea v-model="textareaValue"></textarea>
		<p>{{ textareaValue }}</p>
		<hr />
		<h2>checkbox value</h2>
		<label for="checkbox">{{ checkboxValue }}</label>
		<input
			type="checkbox"
			id="checkbox"
			:checked="checkboxValue"
			@change="event => (checkboxValue = event.target.checked)"
		/>
		<input
			type="checkbox"
			id="checkbox"
			v-model="checkboxValue"
			true-value="Yes"
			false-value="No"
		/>
		<h3>checkbox values</h3>
		<label>
			<input type="checkbox" value="html" v-model="checkboxValues" /> HTML
		</label>
		<label>
			<input type="checkbox" value="Java" v-model="checkboxValues" /> Java
		</label>
		<label>
			<input type="checkbox" value="CSS" v-model="checkboxValues" /> CSS
		</label>
		<p>{{ checkboxValues }}</p>
		<hr />
		<h2>radio value</h2>
		<label>
			<input
				type="radio"
				name="type"
				value="O"
				:checked="radioValue === 'O'"
				@change="event => (radioValue = event.target.value)"
			/>
			O형
		</label>
		<label>
			<input type="radio" name="type" value="A" v-model="radioValue" /> A형
		</label>
		<p>{{ radioValue }}</p>
		<hr />
		<h2>select value</h2>
		<select v-model="selectValue">
			<option value="html">HTML 수업</option>
			<option value="css">CSS 수업</option>
			<option value="javascript">JavaScript 수업</option>
		</select>
		<p>{{ selectValue }}</p>
	</div>
</template>

<script>
import { ref } from 'vue';

export default {
	setup() {
		const inputValue = ref('input박스에 입력하시오');
		const textareaValue = ref('');
		const checkboxValue = ref(true);
		const radioValue = ref('O');
		const selectValue = ref('html');
		const checkboxValues = ref([]);
		return {
			inputValue,
			textareaValue,
			checkboxValue,
			radioValue,
			selectValue,
			checkboxValues,
		};
	},
};
</script>

<style lang="scss" scoped></style>
