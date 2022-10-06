<template>
	<div class="wrapper">
		<div>
			<form>
				<h2>Создание поста</h2>
				<input
					v-bind:value="title"
					@input="title = $event.target.value"
					class="inputClass"
					type="text"
					placeholder="Название"
				/>
				<input
					v-bind:value="body"
					@input="body = $event.target.value"
					class="inputClass"
					type="text"
					placeholder="Описание"
				/>
				<button class="btn" @click="createPost">Создать</button>
			</form>
		</div>
		<div class="post" v-for="post in posts">
			<div><strong>Название: </strong> {{ post.title }}</div>
			<div><strong>Описание: </strong>{{ post.body }}</div>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			posts: [
				{ id: 1, title: 'JavaScript', body: 'Описание поста' },
				{ id: 2, title: 'JavaScript 2', body: 'Описание поста 2' },
				{ id: 3, title: 'JavaScript 3', body: 'Описание поста 3' },
			],
			title: '',
			body: '',
		};
	},

	methods: {
		createPost() {},
	},
};
</script>

<style>
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
}

.wrapper {
	width: 800px;
	margin: 30px auto;
}

.inputClass {
	width: 100%;
	border: 1px solid teal;
	padding: 10px 15px;
	margin-top: 10px;
}

form {
	display: flex;
	flex-direction: column;
}

.btn {
	align-self: flex-end;
	margin-top: 15px;
	padding: 10px 15px;
	background: none;
	color: teal;
	border: 1px solid teal;
	cursor: pointer;
}

.post {
	margin-top: 15px;
	padding: 15px;
	border: 2px solid teal;
}
</style>
