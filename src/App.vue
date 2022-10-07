<template>
	<div class="wrapper">
		<h1>Страница с постами</h1>
		<my-button @click="showDialog" style="margin-bottom: 15px"> Создать пост </my-button>
		<my-dialog v-model:show="dialogVisible">
			<PostForm @create="createPost" />
		</my-dialog>

		<PostList :posts="posts" @remove="removePost" v-if="!isPostLoading" />
		<h3 v-else>Идет загрузка...</h3>
	</div>
</template>

<script>
import PostForm from '@/components/PostForm.vue';
import PostList from '@/components/PostList.vue';
import axios from 'axios';

export default {
	components: {
		PostForm,
		PostList,
	},
	data() {
		return {
			posts: [],
			dialogVisible: false,
			isPostLoading: false,
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
		async fetchPosts() {
			try {
				this.isPostLoading = true;
				const responce = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10');
				this.posts = responce.data;
			} catch (e) {
				alert('error');
			} finally {
				this.isPostLoading = false;
			}
		},
	},
	components: { PostForm, PostList, PostForm },
	mounted() {
		this.fetchPosts();
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
</style>
