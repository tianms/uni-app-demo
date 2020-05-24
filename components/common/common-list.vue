<!-- 公共列表组件 -->
<template>
	<!-- 列表 -->
	<view class="common-list my-f animated fadeInLeft fast">
		<!-- 头像 -->
		<view class="common-list-l">
			<image :src="item.userPic" mode="widthFix" lazy-load></image>
		</view>
		<!-- 内容详情 -->
		<view class="common-list-r">
			<!-- 基本信息 竖直居中，横向靠边 -->
			<view class="my-f-ai my-f-jc-sb">
				<!-- 昵称和性别 -->
				<view class="my-f-ai">
					{{item.userName}}
					<view class="icon iconfont tag-sex" 
					:class="[item.userSex == 0 ? 'icon-nan' : 'icon-nv']">{{item.userAge}}</view>
				</view>
				<view v-show="!isFocus">
					<view class="icon iconfont icon-zengjia" @tap="tapFocus">
						关注
					</view>
				</view>
			</view>
			<!-- 标题 -->
			<view>{{item.title}}</view>
			<!-- 图片和视频 -->
			<view class="my-f-ai-jc-c">
				<!-- 图片 -->
				<image v-if="item.titlePic" :src="item.titlePic" mode="widthFix" lazy-load></image>
				<!-- 视频 -->
				<view v-if="item.video" class="common-list-play icon iconfont icon-bofang"></view>
				<view v-if="item.video" class="common-list-playInfo">
					{{item.video.playNum}} 次播放 {{item.video.playLong}}
				</view>
				<!-- 分享样式 -->
				<view v-if="item.share" class="common-list-share my-f-ai">
					<image :src="item.share.sharePic" mode="widthFix" lazy-load></image>
					<view>{{item.share.shareTitle}}</view>
				</view>
			</view>
			<!-- 操作区 -->
			<view class="my-f-ai my-f-jc-sb">
				<view>{{item.address}}</view>
				<view class="my-f-ai-jc-c">
					<view class="icon iconfont icon-zhuanfa">{{item.shareNum}}</view>
					<view class="icon iconfont icon-pinglun1">{{item.commentNum}}</view>
					<view class="icon iconfont icon-dianzan1">{{item.goodNum}}</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			item: Object,
			index: Number
		},
		data() {
			return {
				isFocus: this.item.isFocus
			}
		},
		methods: {
			// 点击关注
			tapFocus() {
				this.isFocus = true;
				// 官网 API-->界面 --> 交互反馈, 弹出框
				uni.showToast({
				    title: '关注成功',
				});
				// this.toParentData()
			},
			// 返回到父级信息
			toParentData () {
				this.$emit('mergeData', this.curData, this.index)
			}
		}
	}
</script>

<style scoped>
	/* 内容主体 */
	/* 内容 */
	.common-list {
		padding: 20upx;
	}
	/* 左侧内容 */
	.common-list-l {
		/* 不会被压缩 */
		flex-shrink: 0; 
	}
	/* 左侧内容中的图片 */
	.common-list-l image {
		width: 90upx;
		height: 90upx;
		border-radius: 100%;
	}
	/* 右侧内容 */
	.common-list-r {
		flex: 1;
		margin-left: 10upx;
		border-bottom: 1upx solid #EEEEEE;
		padding-bottom: 10upx;
	}
	/* 昵称、性别、年龄、关注 */
	.common-list-r>view:nth-child(1) {
		
	}
	/* 昵称 */
	.common-list-r>view:nth-child(1)>view:first-child {
		color: #999999;
		font-size: 30upx;
	}
	/* 性别、年龄 */
	.tag-sex {
		background: #007AFF;
		color: #FFFFFF;
		font-size: 23upx;
		padding: 4upx 10upx;
		margin-left: 10upx;
		border-radius: 20upx;
		line-height: 22upx;
	}
	/* 关注 */
	.common-list-r>view:nth-child(1)>view:last-child {
		background: #EEEEEE;
		padding: 0 10upx;
		font-size: 20upx;
	}
	/* 标题区 */
	.common-list-r>view:nth-child(2) {
		font-size: 32upx;
		padding: 12upx 0;
	}
	/* 内容中的图片视频 */
	.common-list-r>view:nth-child(3) {
		position: relative;
		margin-bottom: 10upx;
	}
	/* 视频播放相关信息 */
	.common-list-play, .common-list-playInfo {
		position: absolute;
		color: #FFFFFF;
	}
	/* 播放按钮 */
	.common-list-play {
		font-size: 130upx;
	}
	/* 播放信息 */
	.common-list-playInfo {
		right: 10upx;
		bottom: 10upx;
		background: rgba(51, 51, 51, 0.73);
		border-radius: 20upx;
		padding: 0 20upx;
		font-size: 26upx;
	}
	/* 图片 */
	.common-list-r>view:nth-child(3)>image {
		width: 100%;
		border-radius: 10upx;
	}
	/* 分享内容 */
	.common-list-share {
		background: #EEEEEE;
		width: 100%;
		padding: 10upx;
		border-radius: 10upx;
	}
	/* 分享内容的图片 */
	.common-list-share>image {
		width: 200upx;
		height: 150upx;
		margin-right: 10upx;
	}
	/* 操作区域 */
	.common-list-r>view:nth-child(4) {
	}
	/* 操作区域整体颜色 */
	.common-list-r>view:nth-child(4)>view {
		color: #AAAAAA;
	}
	/* 评论转发点赞 */
	.common-list-r>view:nth-child(4)>view:last-child>view {
		margin-left: 10upx;
		padding-left: 5upx;
		font-size: 25upx;
	}
	/* 内容主体 */
</style>
