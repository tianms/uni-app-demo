<template>
	<view>
		<!-- 小纸条列表 -->
		<view class="paper-list my-f-ai">
			<!-- 头像 -->
			<image src="../../static/img/index/user.jpg" mode="widthFix" lazy-load></image>
			<!-- 内容 -->
			<view>
				<!-- 昵称和时间 -->
				<view class="my-f-ai-jc-sb">
					我是昵称
					<view>10:21</view>
				</view>
				<!-- 信息和条数 -->
				<view class="my-f-ai-jc-sb">
					我是信息
					<uni-badge class="uni-badge-left-margin" text="123" type="error" />
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import uniBadge from '@/components/uni-badge/uni-badge.vue';
	export default {
		components: {
			uniBadge
		},
		data() {
			return {
			}
		},
		methods: {
		}
	}
</script>

<style>
	/* 小纸条列表 */
	.paper-list {
		padding: 20upx;
		border-bottom: 1upx solid #EEEEEE;
	}
	.paper-list>image {
		width: 100upx;
		height: 100upx;
		border-radius: 100%;
		margin-right: 20upx;
		flex-shrink: 0;
	}
	.paper-list>view {
		flex: 1;
	}
	.paper-list>view>view:first-child {
		font-size: 35upx;
	}
	.paper-list>view>view:first-child>view {
		color: CBCBCB;
	}
	.paper-list>view>view:last-child {
		color: #888888;
	}
	/* 小纸条列表 */
</style>
