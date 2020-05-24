<!-- 热门分类组件 -->
<template>
	<view class="topic-nav">
		<view class="my-f-ai-jc-sb">
			<view>热门分类</view>
			<view class="my-f-ai" @tap="openNav">
				更多
				<view class="icon iconfont icon-jinru"></view>
			</view>
		</view>
		<view class="my-f-ai">
			<block v-for="(item, index) in navList" :key="index">
				<view class="my-f-ai-jc-c">{{item.name}}</view>
			</block>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			navList: Array
		},
		methods: {
			openNav() {
				uni.navigateTo({
					url: '../../pages/topic-nav/topic-nav',
				});
			}
		},
	}
</script>

<style scoped>
	.topic-nav {
		border-top: 1upx solid #EEEEEE;
		border-bottom: 1upx solid #EEEEEE;
		padding: 20upx;
	}
	.topic-nav>view:first-child {
		margin-bottom: 10upx;
	}
	.topic-nav>view:first-child view {
		color: #9E9E9E;
	}
	/* 热门分类 */
	.topic-nav>view:first-child>view:first-child {
		color: #333333;
		font-size: 32upx;
	}
	/* 跟那个多 */
	.topic-nav>view:first-child>view:last-child {
		
	}
	/* 标签 */
	.topic-nav>view:last-child {
		
	}
	/* 每一个分类标签 */
	.topic-nav>view:last-child view {
		flex: 1;
		background: #DDDDDD;
		color: #9E9E9E;
		border-radius: 10upx;
		margin: 0 10upx;
	}
</style>
