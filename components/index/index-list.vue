<template>
	<view class="base_data animated fadeInLeft">
		<view class="bd_user my-f-ai my-f-jc-sb">
			<!-- 头像 -->
			<view class="my-f-ai my-font">
				<!-- mode 模式，widthFix 固定  lazy-load懒加载-->
				<image 
					:src="boxInfo.userPic" 
					mode="widthFix"
					lazy-load
				>
				</image>
				{{boxInfo.userName}}
			</view>
			<view class="my-f-ai" v-show="!boxInfo.isFocus" @tap="tapFocus()">
				<view class="icon iconfont icon-zengjia"></view>关注
			</view>
		</view>
		<!-- 标题 -->
		<view class="bd_title">{{boxInfo.conTitile}}</view>
		<!-- 背景图片 -->
		<view class="bd_img my-f-ai-jc-c">
			<image
				:src="boxInfo.imgPath" 
				mode="widthFix" 
				lazy-load
			>
			</image>
			<template v-if="boxInfo.conType == '2'">
				<view class="icon iconfont icon-bofang bd_img_play"></view>
				<view class="bd_img_play_info">
					{{boxInfo.videoPlayNum}} 次播放 {{boxInfo.videoTime}}
				</view>
			</template>
		</view>
		<!-- 背景图片下方操作区 -->
		<view class="bd_handle my-f-ai my-f-jc-sb">
			<!-- 左侧，点赞区 -->
			<view class="my-f-ai my-font">
				<view class="my-f-ai" :class="{'active': boxInfo.dcInfo.dcType == '1'}" @tap="handleDC('ding')">
					<view class="icon iconfont icon-icon_xiaolian-mian"></view> {{boxInfo.dcInfo.dzNum}}
				</view>
				<view class="my-f-ai" :class="{'active': boxInfo.dcInfo.dcType == '2'}" @tap="handleDC('cai')">
					<view class="icon iconfont icon-kulian"></view> {{boxInfo.dcInfo.cNum}}
				</view>
			</view>
			<!-- 右侧 转发评论 -->
			<view class="my-f-ai my-font">
				<view class="my-f-ai">
					<view class="icon iconfont icon-pinglun1"></view> {{boxInfo.commentNum}}
					</view>
				<view class=" my-f-ai">
					<view class="icon iconfont icon-zhuanfa"></view> {{boxInfo.shareNum}}
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				curData: {}
			}
		},
		// 接收父组件传值
		props: {
			boxInfo: Object, // 数据类型
			index: Number // 数据下标
		},
		methods: {
			// 关注
			tapFocus () {
				this.curData = this.boxInfo
				this.curData.isFocus = true
				// 官网 API-->界面 --> 交互反馈, 弹出框
				uni.showToast({
				    title: '关注成功',
				});
				this.toParentData()
			},
			// 操作顶和踩
			handleDC (type) {
				this.curData = this.boxInfo
				switch (type){
					case 'ding':
						// 如果当前状态是顶的状态不处理
						if (this.curData.dcType == '1') {
							return;
						}
						// 如果当前状态是踩，踩的数字--
						if (this.curData.dcType == '2') {
							this.curData.dcInfo.cNum--;
						}
						// 点赞数字加一
						this.curData.dcInfo.dzNum++;
						// 将当前状态变为点赞
						this.curData.dcType = '1'
						this.toParentData()
						break;
					case 'cai':
						// 如果当前状态是踩的状态不处理
						if (this.curData.dcType == '2') {
							return;
						}
						// 如果当前状态是顶，顶的数字--
						if (this.curData.dcType == '1') {
							this.curData.dcInfo.dzNum--;
						}
						// 踩数字加一
						this.curData.dcInfo.cNum++;
						// 将当前状态变为点踩
						this.curData.dcType = '2'
						this.toParentData()
						break;
					default:
						break;
				}
			},
			toParentData () {
				this.$emit('mergeData', this.curData, this.index)
				this.curData = {}
			}
		}
	}
</script>

<!-- scoped 设置作用域，只有当前组件可以使用 -->
<style scoped>
	/** 引入css */
	@import '../../css/index/index.css'
</style>
