<!-- 顶部选项卡组件 -->
<template>
	<!-- swiperTabStyle自定义样式属性，根据传入的值展示不同的样式 -->
	<view class="uni-tab-bar" :style="swiperTabStyle">
		<!-- 顶部选项卡 -->
		<!-- scroll-view,允许横向，纵向滚动，scroll-x,scroll-y -->
		<scroll-view class="uni-swiper-tab" scroll-x>
			<block v-for="(tab,index) in tabBarList" :key="tab.id">
				<!-- 每一个选项卡信息 -->
				<!-- tabTap 点击选项卡，传入当前的选项卡下标 -->
				<!-- 当前选中的选项卡添加的选中样式 -->
				<!-- tabIndex 是当前选中的选项卡下标 -->
				<!-- swiperTabItemStyle自定义样式属性，根据传入的值展示不同的样式 -->
				<view 
					class="swiper-tab-list" 
					@tap="tabTap(index)" 
					:class="{'active': tabIndex == index }"
					:style="swiperTabItemStyle"
				>
					{{tab.name}}
					<!-- 选中的选项卡下的下划线 -->
					<view class="swiper-tab-line"></view>
				</view>
			</block>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		props: {
			tabBarList: Array,
			tabIndex: Number,
			// 自定义属性样式，默认为空不添加额外样式属性
			swiperTabStyle: {
				type: String,
				default: ''
			},
			// 自定义属性样式，默认为空不添加额外样式属性
			swiperTabItemStyle: {
				type: String,
				default: ''
			}
		},
		methods: {
			// 点击菜单
			tabTap (index) {
				this.$emit('tabTap', index)
			}
		}
	}
</script>

<style scoped>
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
	.active .swiper-tab-line {
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
