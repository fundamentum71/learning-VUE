<template>
	<div class="wrapper">
		<PostForm @create="createPost" />
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
		};
	},
	methods: {
		createPost(post) {
			this.posts.push(post);
		},
		removePost(post) {
			this.posts = this.posts.filter((item) => item.id !== post.id);
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
