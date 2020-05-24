<!-- 图文列表组件 -->
<template>
	<!-- animated动画效果样式 -->
	<view class="base_data animated fadeInLeft">
		<view class="bd_user my-f-ai my-f-jc-sb">
			<!-- 头像 -->
			<view class="my-f-ai my-font">
				<!-- mode 模式，widthFix 固定  lazy-load懒加载-->
				<!-- 头像图片 -->
				<image 
					:src="curData.userPic" 
					mode="widthFix"
					lazy-load
				>
				</image>
				<!-- 用户名 -->
				{{curData.userName}}
			</view>
			<!-- 关注信息 -->
			<view class="my-f-ai" v-show="!curData.isFocus" @tap="tapFocus()">
				<view class="icon iconfont icon-zengjia"></view>关注
			</view>
		</view>
		<!-- 标题 -->
		<view class="bd_title" @tap="openDetail">{{curData.conTitile}}</view>
		<!-- 背景图片 -->
		<view class="bd_img my-f-ai-jc-c" @tap="openDetail">
			<!-- 图片 -->
			<image
				:src="curData.imgPath" 
				mode="widthFix" 
				lazy-load
			>
			</image>
			<!-- 视频信息 -->
			<template v-if="curData.conType == '2'">
				<view class="icon iconfont icon-bofang bd_img_play"></view>
				<!-- 视频播放信息 -->
				<view class="bd_img_play_info">
					{{curData.videoPlayNum}} 次播放 {{curData.videoTime}}
				</view>
			</template>
		</view>
		<!-- 背景图片下方操作区 -->
		<view class="bd_handle my-f-ai my-f-jc-sb">
			<!-- 左侧，点赞区 -->
			<view class="my-f-ai my-font">
				<!-- 点赞信息 -->
				<view class="my-f-ai" :class="{'active': curData.dcInfo.dcType == '1'}" @tap="handleDC('ding')">
					<view class="icon iconfont icon-icon_xiaolian-mian"></view> {{curData.dcInfo.dzNum}}
				</view>
				<!-- 踩信息 -->
				<view class="my-f-ai" :class="{'active': curData.dcInfo.dcType == '2'}" @tap="handleDC('cai')">
					<view class="icon iconfont icon-kulian"></view> {{curData.dcInfo.cNum}}
				</view>
			</view>
			<!-- 右侧 转发评论 -->
			<view class="my-f-ai my-font">
				<!-- 评论信息 -->
				<view class="my-f-ai">
					<view class="icon iconfont icon-pinglun1"></view> {{curData.commentNum}}
				</view>
				<!-- 转发信息 -->
				<view class=" my-f-ai">
					<view class="icon iconfont icon-zhuanfa"></view> {{curData.shareNum}}
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				// 将接受到的数据赋值给当前vue创建的新对象，更改的时候更新当前页面创建的对象内容
				curData: this.item
			}
		},
		// 接收父组件传值
		props: {
			item: Object, // 数据类型
			index: Number, // 数据下标
			swIndex: Number
		},
		methods: {
			// 关注
			tapFocus () {
				this.curData.isFocus = true
				// 官网 API-->界面 --> 交互反馈, 弹出框
				uni.showToast({
				    title: '关注成功',
				});
				this.toParentData()
			},
			// 操作顶和踩
			handleDC (type) {
				switch (type){
					case 'ding':
						// 如果当前状态是顶的状态不处理
						if (this.curData.dcInfo.dcType == '1') {
							return;
						}
						// 如果当前状态是踩，踩的数字--
						if (this.curData.dcInfo.dcType == '2') {
							this.curData.dcInfo.cNum--;
						}
						// 点赞数字加一
						this.curData.dcInfo.dzNum++;
						// 将当前状态变为点赞
						this.curData.dcInfo.dcType = '1'
						this.toParentData()
						break;
					case 'cai':
						// 如果当前状态是踩的状态不处理
						if (this.curData.dcInfo.dcType == '2') {
							return;
						}
						// 如果当前状态是顶，顶的数字--
						if (this.curData.dcInfo.dcType == '1') {
							this.curData.dcInfo.dzNum--;
						}
						// 踩数字加一
						this.curData.dcInfo.cNum++;
						// 将当前状态变为点踩
						this.curData.dcInfo.dcType = '2'
						this.toParentData()
						break;
					default:
						break;
				}
			},
			// 进入详情页
			openDetail () {
				console.log('进入详情页');
			},
			// 返回到父级信息
			toParentData () {
				this.$emit('mergeData', this.curData, this.index, this.swIndex)
			}
		}
	}
</script>

<!-- scoped 设置作用域，只有当前组件可以使用 -->
<style scoped>
	/** 引入css */
	@import '../../css/index/index.css'
</style>
