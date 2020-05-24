<!-- 话题信息 -->
<template>
	<view>
		<!-- 模糊背景 -->
		<view class="topic-bg">
			<!-- aspectFill 保持纵横比缩放图片，只保证图片的短边能完全显示出来。
				也就是说，图片通常只在水平或垂直方向是完整的，另一个方向将会发生截取  -->
			<image :src="topicInfo.topicImgUrl" mode="aspectFill" lazy-load></image>
		</view>
		<!-- 话题信息 -->
		<view class="topic-info">
			<!-- 上部分 图片和标题 -->
			<view class="topic-info-top my-f-ai">
				<image :src="topicInfo.topicImgUrl" mode="widthFix" lazy-load></image>
				<view>#{{topicInfo.topicTitle}}#</view>
			</view>
			<!-- 中间部分 动态数和今日动态数 -->
			<view class="topic-info-center my-f-ai">
				<view>动态 {{topicInfo.totalTopicNum}}</view>
				<view>今日 {{topicInfo.todayTopicNum}}</view>
			</view>
			<!-- 下部分 描述部分 -->
			<view class="topic-info-bottom my-f-ai">
				{{topicInfo.topicDesc}}
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			topicInfo: Object
		}
	}
</script>

<style scoped>
	/* 模糊背景 */
	.topic-bg {
		width: 100%;
		height: 300upx;
		position: relative;
		overflow: hidden;
	}
	.topic-bg image {
		width: 100%;
		position: absolute;
		/* 模糊化效果 */
		filter: blur(10px);
	}
	/* 模糊背景 */
	
	/* 话题信息 */
	.topic-info {
		padding: 0 20upx;
	}
	.topic-info-top {
		position: relative;
	}
	.topic-info-top image {
		width: 150upx;
		height: 150upx;
		border-radius: 20upx;
		position: absolute;
		top: -75upx;
	}
	.topic-info-top view {
		font-size: 35upx;
		margin-left: 170upx;
		flex: 1;
	}
	.topic-info-center view {
		padding: 35upx 0 15upx 0;
		color: #CDCDCD;
	}
	.topic-info-center>view:last-child {
		margin-left: 18upx;
	}
	.topic-info-bottom {
		color: #A3A3A3;
		font-size: 32upx;
	}
	/* 话题信息 */
</style>
