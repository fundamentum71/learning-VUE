<template>
	<div class="post">
		<div>
			<div><strong>Название: </strong> {{ post.title }}</div>
			<div><strong>Описание: </strong>{{ post.body }}</div>
		</div>
		<div class="post__btns">
			<my-button class="btn" style="margin-top: 0">Удалить</my-button>
		</div>
	</div>
</template>
<script>
export default {
	props: {
		post: {
			type: Object,
			required: true,
		},
	},
};
</script>
<style scoped>
.post {
	margin-top: 15px;
	padding: 15px;
	border: 2px solid teal;
	display: flex;
	justify-content: space-between;
	align-items: center;
}
</style>
