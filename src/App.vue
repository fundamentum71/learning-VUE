<template>
	<div class="wrapper">
		<h1>Страница с постами</h1>
		<my-button @click="showDialog" style="margin-bottom: 15px"> Создать пост </my-button>
		<my-dialog v-model:show="dialogVisible">
			<PostForm @create="createPost" />
		</my-dialog>

		<PostList :posts="posts" @remove="removePost" />
	</div>
</template>

<script>
import PostForm from '@/components/PostForm.vue';
import PostList from '@/components/PostList.vue';

export default {
	components: {
		PostForm,
		PostList,
	},
	data() {
		return {
			posts: [
				{ id: 1, title: 'JavaScript', body: 'Описание поста' },
				{ id: 2, title: 'JavaScript 2', body: 'Описание поста 2' },
				{ id: 3, title: 'JavaScript 3', body: 'Описание поста 3' },
			],
			dialogVisible: false,
		};
	},
	methods: {
		createPost(post) {
			this.posts.push(post);
			this.dialogVisible = false;
		},
		removePost(post) {
			this.posts = this.posts.filter((item) => item.id !== post.id);
		},
		showDialog() {
			this.dialogVisible = true;
		},
	},
	components: { PostForm, PostList, PostForm },
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
</style>
