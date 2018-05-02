<template>
	<div class="container">
		<h2 class="title">{{title}}</h2>
	</div>
</template>

<script>
	export default {
		name: 'Header',
		props: {
			title: {
				type: String,
			},
		},
		data() {
			return {
			};
		}
	}
</script>

<style lang="less">
.container{
	width: 100%;
	height: 44px;
	line-height: 44px;
	text-align: center;
}
</style>