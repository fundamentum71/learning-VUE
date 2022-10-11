<template>
	<div>
		<h1>Страница с постами</h1>
		<my-input
			v-focus
			:model-value="searchQuery"
			@update:model-value="setSearchQuery"
			placeholder="Поиск..."
		>
		</my-input>
		<div class="app__btns">
			<my-button @click="showDialog"> Создать пост </my-button>
			<my-selected
				:model-value="selectedSort"
				@update:model-value="setSelectedSort"
				:options="sortOptions"
			></my-selected>
		</div>

		<my-dialog v-model:show="dialogVisible">
			<PostForm @create="createPost" />
		</my-dialog>

		<PostList :posts="sortedAndSearchedPosts" @remove="removePost" v-if="!isPostLoading" />
		<h3 v-else>Идет загрузка...</h3>
		<div v-intersection="loadMorePosts" class="observe"></div>

		<!--<div class="page__wrapper">
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
		</div>-->
	</div>
</template>

<script>
import PostForm from '@/components/PostForm.vue';
import PostList from '@/components/PostList.vue';
import axios from 'axios';
import { mapState, mapGetters, mapActions, mapMutations } from 'vuex';

export default {
	components: {
		PostForm,
		PostList,
	},
	data() {
		return {
			posts: [],
			dialogVisible: false,
			//isPostLoading: false,
			//selectedSort: '',
			//searchQuery: '',
			//page: 1,
			//limit: 10,
			//totalPages: 0,
			//sortOptions: [
			//	{ value: 'title', name: 'По названию' },
			//	{ value: 'body', name: 'По описанию' },
			//],
		};
	},
	methods: {
		...mapMutations({
			setPage: 'post/setPage',
			setSearchQuery: 'post/setSearchQuery',
			setSelectedSort: 'post/setSelectedSort',
		}),
		...mapActions({
			loadMorePosts: 'post/loadMorePosts',
			fetchPosts: 'post/fetchPosts',
		}),

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
		//changePage(pageNumber) {
		//	this.page = pageNumber;
		//},
	},
	components: { PostForm, PostList, PostForm },
	mounted() {
		this.fetchPosts();
		//let options = {
		//	rootMargin: '0px',
		//	threshold: 1.0,
		//};
		//let callback = (entries, observer) => {
		//	if (entries[0].isIntersecting && this.page < this.totalPages) {
		//		this.loadMorePosts();
		//	}
		//};
		//let observer = new IntersectionObserver(callback, options);
		//observer.observe(this.$refs.observer);
	},
	computed: {
		...mapState({
			posts: (state) => state.post.posts,
			isPostLoading: (state) => state.post.isPostLoading,
			selectedSort: (state) => state.post.selectedSort,
			searchQuery: (state) => state.post.searchQuery,
			page: (state) => state.post.page,
			limit: (state) => state.post.limit,
			totalPages: (state) => state.post.totalPages,
			sortOptions: (state) => state.post.sortOptions,
		}),
		...mapGetters({
			sortedPosts: 'post/sortedPosts',
			sortedAndSearchedPosts: 'post/sortedAndSearchedPosts',
		}),
	},
	watch: {
		//page() {
		//	this.fetchPosts();
		//},
	},
};
</script>

<style>
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
.observe {
	height: 30px;
	background: green;
}
</style>
