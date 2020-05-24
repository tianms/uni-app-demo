<template>
	<view>
		<!-- 自定义导航 -->
		<!-- statusBar 状态栏 uni-nav-bar中有属性接判断是否展示 -->
		<!-- @clickLeft 监听左边按钮的事件，从uni-nav-bar中的左边按钮的点击事件中会返回到父组件事件处理 -->
		<!-- @clickRight 监听右边按钮的事件，从uni-nav-bar中的左边按钮的点击事件中会返回到父组件事件处理 -->
		<uni-nav-bar left-icon="arrowleft" @clickLeft="back" @clickRight="submit" :statusBar="true" rightText="发布">
			<!-- 中间标题部分，通过插槽写入 -->
			<view class="my-f-ai-jc-c"  style="flex: 1;" @tap="changeLook">
				{{ yinsi }}
				<!-- 文字右边的下拉图标 -->
				<view class="icon iconfont icon-xialazhankai"></view>
			</view>
		</uni-nav-bar>
		
		<!-- 新增主题内容 -->
		<view>
			<!-- 多行输入框 -->
			<!-- 官网->组件->表单组件 -->
			<!-- class="uni-textarea"是官方写好的多行文本样式 -->
			<view class="uni-textarea">
				<textarea v-model="text" placeholder="请输入要发布的内容" />
			</view>
			
			<!-- 上传多图 -->
			<upload-images @sendImgList="getImageList"></upload-images>
			
			<!-- 弹出公告 -->
			<uni-popup ref="showpopup" type="center" :mask-click="true" @change="change">
				<view class="uni-popup gonggao">
					<view class="my-f-ai-jc-c">					
						<!-- 头部图片 -->
						<image src="../../static/common/addinput.png" mode="widthFix"></image>
					</view>
					<view>1、涉及黄色，政治，广告及骚扰信息</view>
					<view>2、涉及人身攻击</view>
					<view>3、留联系方式，透露他人隐私</view>
					<view>一经核实将被封禁，情节严重者永久封禁</view>
					<button type="default" @tap="closePopup">朕知道了</button>
				</view>
			</uni-popup>
		</view>
	</view>
</template>

<script>
	import uniNavBar from '../../components/uni-nav-bar/uni-nav-bar.vue';
	import uploadImages from '../../components/common/upload-images.vue';
	import uniPopup from '../../components/uni-popup/uni-popup.vue';
	export default {
		// 页面渲染完
		onReady() {
			this.openPopup();
		},
		// 监听返回
		onBackPress () {
			// 如果有值
			if (!this.text && this.imageList.length < 1) {
				return;
			}
			if (!this.isAsk) {
				this.saveDraft();
				return true;
			}
		},
		data() {
			return {
				changeLookList: ['所有人可见', '仅自己可见'],
				yinsi: '所有人可见',
				text: '', // 多行文本内容
				imageList: [], // 选中的图片列表
				isAsk: false
				
			}
		},
		components:{
			uniNavBar,
			uploadImages,
			uniPopup
		},
		methods: {
			// 返回
			back () {
				// 返回上一层
				uni.navigateBack({
					delta: 1
				});
			},
			// 发布
			submit () {
				
			},
			// 隐私 
			changeLook () {
				// 官网-->接口-->界面-->交互反馈
				uni.showActionSheet({
					// itemList可选项列表， itemList接收一个数组
					itemList: this.changeLookList, 
					success: res => {
						// res.tapIndex 选择的列表的下标
						this.yinsi = this.changeLookList[res.tapIndex]
					}
				});
			},
			// 获取图片列表
			getImageList (imgList) {
				this.imageList = imgList;
			},
			change(e) {
				// console.log('是否打开:' + e.show)
			},
			// 打开弹出公告
			openPopup () {
				this.$nextTick(() => {
					this.$refs['showpopup'].open();
				})
			},
			// 关闭公告
			closePopup () {
				this.$nextTick(() => {
					this.$refs['showpopup'].close();
				})
			},
			// 保存草稿
			saveDraft () {
				uni.showModal({
					content: '是否要保存为草稿？',
					cancelText: '不保存',
					confirmText: '保存',
					success: res => {
						if (res.confirm) { // 点击保存
							console.log('保存');
						} else {
							console.log('不保存');
						}
						this.isAsk = true;
						this.back();
					}
				});
			}
		}
	}
</script>

<style scoped>
	/* 多行文本样式 */
	.uni-textarea {
		border: 1upx solid #EEEEEE;
	}
	/* 公告下内容样式 */
	.gonggao {
		padding: 30upx;
		border-radius: 15upx;
		width: 500upx;
		background: #FFFFFF;
	}
	.gonggao image {
		width: 70%;
		margin-bottom: 20upx;
	}
	.gonggao button {
		margin-top: 20upx;
		background: #FFE934;
		color: #171606;
	}
	/* 公告下内容样式 */
</style>
