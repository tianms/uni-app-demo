<!-- 自定义导航组件 -->
<template>
	<view>
		<!-- uni-nav-bar 自定义顶部导航 -->
		<!-- fixed 固定 border导航栏下面自带的边框是否显示 -->
		<uni-nav-bar :fixed="true" :statusBar="true" @clickRight="openAdd" :border="false">
			<!-- 左边 -->
			<block slot="left">
				<view class="nav-left">
					<view class="icon iconfont icon-qiandao"></view>
				</view>
			</block>
			<!-- 中间 -->
			<view class="nav-tab-bar my-f-ai-jc-c">
				<block v-for="(tab, index) in tabBars" :key="tab.id">
					<view class="my-f-ai-jc-c" :class="{'active': tabIndex == index}" @tap="clickTab(index)">
						{{ tab.name }}
						<!-- 下划线 -->
						<view v-if="(tabIndex == index)" class="nav-tab-bar-line"></view>
					</view>
				</block>
			</view>
			<!-- 右边 -->
			<block slot="right">
				<view class="nav-right" @tap="openAdd">
					<view class="icon iconfont icon-bianji1"></view>
				</view>
			</block>
		</uni-nav-bar>
	</view>
</template>

<script>
	import uniNavBar from '../uni-nav-bar/uni-nav-bar.vue';
	export default {
		props: {
			tabBars: Array,
			tabIndex: Number
		},
		components: {
			uniNavBar
		},
		methods: {
			// 点击菜单
			clickTab (index) {
				this.$emit('change-tab', index);
			},
			// 打开发布页
			openAdd () {
				uni.navigateTo({
					url: '../../pages/add-input/add-input'
				});
			}
		}
	}
</script>

<style scoped>
	.nav-left>view, .nav-right>view {
		font-size: 35upx;
	}
	.nav-left>view {
		color: #FF6919;
	}
	.nav-left {
		margin-left: 16upx;
	}
	.nav-right {
		width: 100%;
		margin-right: -200upx;
	}
	.nav-tab-bar {
		width: 100%;
		margin-left: -20upx;
	}
	.nav-tab-bar>view {
		font-size: 30upx;
		padding: 0 15upx;
		font-weight: bold;
		color: #969696;
		position: relative;
	}
	.active {
		color: #333333!important;
	}
	/* 标签下的下划线 */
	.nav-tab-bar-line {
		border-bottom: 5upx solid #FEDE33;
		border-top: 5upx solid #FEDE33;
		width: 70upx;
		border-radius: 20upx;
		position: absolute;
		bottom: 0upx;
		left: 10upx;
	}
</style>
