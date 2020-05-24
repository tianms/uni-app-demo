<template>
	<view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		// 监听原生标题导航按钮点击事件, 事件来源介绍：官网-->介绍-->框架简介-->生命周期-->页面生命周期中
		onNavigationBarButtonTap(e) {
			if (e.index == 0) { // 点击取消
				// 官网->接口->路由
				uni.navigateBack({ // 关闭当前页面，返回上一级或者多级
					delta: 1
				});
			}
		},
		// 监听原生标搜索输入框内容变化事件, 事件来源介绍：官网-->介绍-->框架简介-->生命周期-->页面生命周期中
		onNavigationBarSearchInputChanged (e) {
			var text = e.text; // 文本内容
		},
		// 监听原生搜索框搜索事件, 事件来源介绍：官网-->介绍-->框架简介-->生命周期-->页面生命周期中
		onNavigationBarSearchInputConfirmed (e) {
			var text = e.text; // 文本内容
		},
		methods: {
			
		}
	}
</script>

<style>

</style>
