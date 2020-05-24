<!-- 最近更新组件 -->
<template>
	<!-- 最近更新 -->
	<view class="topic-new">
		<view>最近更新</view>
		<block v-for="(item, index) in newList" :key="index">
			<view class="topic-list my-f animated fadeInLeft fast" @tap="openTopicDetail(index)">
				<image :src="item.topImgUrl" mode="widthFix" lazy-load></image>
				<view>
					<view>#{{item.title}}#</view>
					<view>{{item.desc}}</view>
					<view>动态 {{item.totalNum}} 今日 {{item.todayNum}}</view>
				</view>
			</view>
		</block>
	</view>
</template>

<script>
	export default {
		props: {
			newList:Array,
			index: Number
		},
		methods: {
			// 打开话题详情
			openTopicDetail(index) {
				// TODO uni.navigateTo如何传入参数？？传入后，怎么接收参数
				uni.navigateTo({
					url: '../../pages/topic-detail/topic-detail'
				});
			}
		},
	}
</script>

<style scoped>
	/* 最近更新 */
	.topic-new {
		padding: 20upx;
	}
	/* 标题内容 */
	.topic-new>view:first-child {
		padding-bottom: 5upx;
		font-size: 32upx;
	}
	.topic-list {
		padding: 20upx 0;
		border-bottom: 1upx solid #EEEEEE;
	}
	.topic-list image {
		width: 150upx;
		height: 150upx;
		border-radius: 10upx;
		margin-right: 20upx;
	}
	.topic-list>view>view {
		color: #A4A4A4;
	}
	.topic-list>view>view:first-child {
		color: #333333;
		font-size: 32upx;
	}
	/* 最近更新 */
</style>
