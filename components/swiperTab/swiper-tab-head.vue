<template>
	<view class="uni-tab-bar">
		<!-- scroll-view,允许横向，纵向滚动，scroll-x,scroll-y -->
		<scroll-view class="uni-swiper-tab" scroll-x>
			<block v-for="(tab,index) in tabBarList" :key="tab.id">
				<view class="swiper-tab-list" 
					@tap="tabTap(index)"
					:class="{'active': tabIndex==index }"
				>
					{{tab.name}}
					<view class="tab-item-active"></view>
				</view>
			</block>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		props: {
			tabBarList: Array,
			tabIndex: Number
		},
		methods: {
			// 点击菜单
			tabTap (index) {
				this.$emit('tabTap', index)
			}
		}
	}
</script>

<style>
	.uni-tab-bar {
		border-bottom: 1upx solid #EEEEEE;
	}
	.swiper-tab-list {
		font-weight: bold;
		color: #959394;
	}
	/** 选中的字体颜色改变 */
	.uni-tab-bar .active {
		color: #140D0F;
	}
	/** 选中的标签下方 */
	.active .tab-item-active {
		border-top: 6upx solid #FDDA30;
		border-bottom: 6upx solid #FDDA30;
		border-radius: 50upx;
		width: 80upx;
		margin: 0 auto;
	}
	.swiper-box {
		/* height: 700upx!important; */
	}
</style>
