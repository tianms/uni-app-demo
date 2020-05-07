<template>
	<view class="uni-tab-bar">
		<scroll-view class="uni-swiper-tab" scroll-x>
			<block v-for="(tab,index) in tabBars" :key="tab.id">
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
		data() {
			return {
				tabIndex: 0,
				tabBars: [
					{
						name: '关注',
						id: 'guanzhu'
					}, 
					{
						name: '推荐',
						id: 'tuijian'
					}, 
					{
						name: '体育',
						id: 'tiyu'
					},
					{
						name: '热点',
						id: 'redian'
					}, 
					{
						name: '财经',
						id: 'caijing'
					}, 
					{
						name: '娱乐',
						id: 'yule'
					}
				]
			}
		},
		methods: {
			tabTap (index) {
				this.tabIndex = index
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
</style>
