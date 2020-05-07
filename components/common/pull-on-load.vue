<!-- 上拉加载数据组件 -->
<template>
	<view class="load-more">{{loadText}}</view>
</template>

<script>
	export default {
		props: {
			loadText: String
		}
	}
</script>

<style>
	.load-more {
		text-align: center;
		color: #AAAAAA;
		padding: 15upx;
	}
</style>
