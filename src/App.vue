<template>
	<div class="wrapper">
		<h1>Страница с постами</h1>
		<my-input v-model="searchQuery" placeholder="Поиск..."> </my-input>
		<div class="app__btns">
			<my-button @click="showDialog"> Создать пост </my-button>
			<my-selected v-model="selectedSort" :options="sortOptions"></my-selected>
		</div>

		<my-dialog v-model:show="dialogVisible">
			<PostForm @create="createPost" />
		</my-dialog>

		<PostList :posts="sortedAndSearchedPosts" @remove="removePost" v-if="!isPostLoading" />
		<h3 v-else>Идет загрузка...</h3>

		<div class="page__wrapper">
			<div
				v-for="pageNumber in totalPages"
				:key="pageNumber"
				class="page"
				:class="{
					'current-page': page === pageNumber ? true : false,
				}"
				@click="changePage(pageNumber)"
			>
				{{ pageNumber }}
			</div>
		</div>
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
			selectedSort: '',
			searchQuery: '',
			page: 1,
			limit: 10,
			totalPages: 0,
			sortOptions: [
				{ value: 'title', name: 'По названию' },
				{ value: 'body', name: 'По описанию' },
			],
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
		changePage(pageNumber) {
			this.page = pageNumber;
		},
		async fetchPosts() {
			try {
				this.isPostLoading = true;
				const response = await axios.get(`https://jsonplaceholder.typicode.com/posts`, {
					params: {
						_page: this.page,
						_limit: this.limit,
					},
				});
				this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit);
				this.posts = response.data;
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
	computed: {
		sortedPosts() {
			return [...this.posts].sort((post1, post2) => {
				return post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]);
			});
		},
		sortedAndSearchedPosts() {
			return this.sortedPosts.filter((post) =>
				post.title.toLowerCase().includes(this.searchQuery.toLowerCase()),
			);
		},
	},
	watch: {
		page() {
			this.fetchPosts();
		},
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

.app__btns {
	margin: 15px 0;
	display: flex;
	justify-content: space-between;
}

.page__wrapper {
	display: flex;
	margin-top: 15px;
}

.page {
	border: 0.1px solid black;
	padding: 10px;
	margin: 5px;
	cursor: pointer;
}
.current-page {
	border: 2px solid teal;
}
</style>
