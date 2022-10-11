<template>
	<navbar></navbar>
	<div class="wrapper">
		<router-view></router-view>
	</div>
</template>
<script>
import Navbar from '@/components/Navbar';
export default {
	components: {
		Navbar,
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
