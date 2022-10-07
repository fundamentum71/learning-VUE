<template>
	<form @submit.prevent>
		<h2>Создание поста</h2>
		<input v-model="post.title" class="inputClass" type="text" placeholder="Название" />
		<input v-model="post.body" class="inputClass" type="text" placeholder="Описание" />
		<MyButton @click="createPost" style="align-self: flex-end"> Создать</MyButton>
	</form>
</template>
<script>
import MyButton from './UI/MyButton.vue';
export default {
	components: {
		MyButton,
	},
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
			this.$emit('create', this.post);
			this.post = {
				title: '',
				body: '',
			};
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
</style>
