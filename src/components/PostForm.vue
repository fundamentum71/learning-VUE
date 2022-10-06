<template>
	<form @submit.prevent>
		<h2>Создание поста</h2>
		<input v-model="post.title" class="inputClass" type="text" placeholder="Название" />
		<input v-model="post.body" class="inputClass" type="text" placeholder="Описание" />
		<button class="btn" @click="createPost">Создать</button>
	</form>
</template>
<script>
export default {
	data() {
		return {
			post: {
				title: '',
				body: '',
			},
		};
	},
	methods: {
		createPost() {
			this.post.id = Date.now();
			this.posts.push(newPost);
			this.title = '';
			this.body = '';
		},
	},
};
</script>
<style scoped>
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
</style>
