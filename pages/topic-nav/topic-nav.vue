<template>
	<view>
		<!-- swiper-tab  顶部选项卡 -->
		<swiper-tab-head :tabBarList="tabBarList" :tabIndex="tabIndex" @tabTap="tabTap"></swiper-tab-head>
		
		<!-- 顶部选项卡下的文本内容，功能与顶部选项卡类似，可以横向滚动和竖向滚动 -->
		<view class="uni-tab-bar">
			<!-- 滑块视图容器 :style动态拼接单位，不支持使用upx，可以通过转换计算后使用px -->
			<!-- @@change监听改变，改变时触发swiperChange事件，同步顶部选项卡的下标使两部分保持一致 -->
			<!-- :current 当前所在滑块的下标，与顶部选项卡的下标一致 -->
			<swiper class="swiper-box" :style="{height: swiperHeight + 'px'}" @change="swiperChange" :current="tabIndex">
				<block v-for="(swiper, swIndex) in swiperList" :key="swIndex">
					<!-- swiper-item 每一个滑块，里面放置当前滑块要展示的内容 -->
					<swiper-item>
						<!-- 下面这个滑块视图展示内容，所以为纵向滚动 -->
						<!-- @scrolltolower触底事件 -->
						<scroll-view scroll-y class="list" @scrolltolower="loadMore(swIndex)">
							<template v-if="swiper.list.length > 0">
								<!-- 最近更新 -->
								<topic-new-list :newList="swiper.list"></topic-new-list>
								<!-- 上拉加载 -->
								<pull-on-load :loadText="swiper.loadText"></pull-on-load>
							</template>
							<template v-else>
								<!-- 无内容展示页 -->
								<no-thing></no-thing>
							</template>
						</scroll-view>
					</swiper-item>
				</block>
			</swiper>
		</view>
	</view>
</template>

<script>
	// 引入封装的内容组件
	import indexList from '../../components/index/index-list.vue';
	// 引入swiper-tab滑动菜单组件
	import swiperTabHead from '../../components/swiperTab/swiper-tab-head.vue';
	// 引入上拉加载组件
	import pullOnLoad from '../../components/common/pull-on-load.vue';
	// 引入没有数据展示的页面
	import noThing from '../../components/common/no-thing.vue';
	// 最新更新组件
	import topicNewList from '../../components/news/topic-new-list.vue';
	
	export default {
		// 当页面渲染完成后执行
		onLoad() {
			// this.init() 官网-->接口
			uni.getSystemInfo({
			    success: (res) => {
					// 计算视图高度，动态计算高度
					// res.windowHeight 窗口高度
					let height = res.windowHeight - uni.upx2px(100);
					this.swiperHeight = height;
			    }
			});
		},
		// 监听搜索框点击事件
		onNavigationBarSearchInputClicked () {
			// 触发导航栏点击事件后，跳转到搜索页面
			// 官网->接口->路由
			uni.navigateTo({ // 保留当前页面，跳转到一个页面
				url: '../search/search'
			})
		},
		data() {
			return {
				// 顶部选项卡下内容的高度，计算得到
				swiperHeight: 0,
				swiperList: [
					{
						loadText: '上拉加载更多',
						list: [
							{
								topImgUrl: '../../static/demo/topicpic/13.jpeg',
								title: '话题名称',
								desc: '我是话题描述',
								totalNum: '21',
								todayNum: '12'
							},
							{
								topImgUrl: '../../static/demo/topicpic/14.jpeg',
								title: '话题名称',
								desc: '我是话题描述',
								totalNum: '22',
								todayNum: '9'
							},
							{
								topImgUrl: '../../static/demo/topicpic/15.jpeg',
								title: '话题名称',
								desc: '我是话题描述',
								totalNum: '256',
								todayNum: '114'
							},
							{
								topImgUrl: '../../static/demo/topicpic/13.jpeg',
								title: '话题名称',
								desc: '我是话题描述',
								totalNum: '21',
								todayNum: '12'
							},
							{
								topImgUrl: '../../static/demo/topicpic/14.jpeg',
								title: '话题名称',
								desc: '我是话题描述',
								totalNum: '22',
								todayNum: '9'
							},
							{
								topImgUrl: '../../static/demo/topicpic/15.jpeg',
								title: '话题名称',
								desc: '我是话题描述',
								totalNum: '256',
								todayNum: '114'
							},
							{
								topImgUrl: '../../static/demo/topicpic/13.jpeg',
								title: '话题名称',
								desc: '我是话题描述',
								totalNum: '21',
								todayNum: '12'
							},
							{
								topImgUrl: '../../static/demo/topicpic/14.jpeg',
								title: '话题名称',
								desc: '我是话题描述',
								totalNum: '22',
								todayNum: '9'
							},
							{
								topImgUrl: '../../static/demo/topicpic/15.jpeg',
								title: '话题名称',
								desc: '我是话题描述',
								totalNum: '256',
								todayNum: '114'
							}
						]
					},
					{
						loadText: '上拉加载更多',
						list: [
							{
								topImgUrl: '../../static/demo/topicpic/14.jpeg',
								title: '话题名称',
								desc: '我是话题描述',
								totalNum: '22',
								todayNum: '9'
							},
							{
								topImgUrl: '../../static/demo/topicpic/15.jpeg',
								title: '话题名称',
								desc: '我是话题描述',
								totalNum: '256',
								todayNum: '114'
							},
							{
								topImgUrl: '../../static/demo/topicpic/13.jpeg',
								title: '话题名称',
								desc: '我是话题描述',
								totalNum: '21',
								todayNum: '12'
							},
							{
								topImgUrl: '../../static/demo/topicpic/14.jpeg',
								title: '话题名称',
								desc: '我是话题描述',
								totalNum: '22',
								todayNum: '9'
							},
							{
								topImgUrl: '../../static/demo/topicpic/15.jpeg',
								title: '话题名称',
								desc: '我是话题描述',
								totalNum: '256',
								todayNum: '114'
							},
							{
								topImgUrl: '../../static/demo/topicpic/13.jpeg',
								title: '话题名称',
								desc: '我是话题描述',
								totalNum: '21',
								todayNum: '12'
							},
							{
								topImgUrl: '../../static/demo/topicpic/14.jpeg',
								title: '话题名称',
								desc: '我是话题描述',
								totalNum: '22',
								todayNum: '9'
							},
							{
								topImgUrl: '../../static/demo/topicpic/15.jpeg',
								title: '话题名称',
								desc: '我是话题描述',
								totalNum: '256',
								todayNum: '114'
							}
						]
					},
					{
						loadText: '上拉加载更多',
						list: [
							{
								topImgUrl: '../../static/demo/topicpic/15.jpeg',
								title: '话题名称',
								desc: '我是话题描述',
								totalNum: '256',
								todayNum: '114'
							},
							{
								topImgUrl: '../../static/demo/topicpic/13.jpeg',
								title: '话题名称',
								desc: '我是话题描述',
								totalNum: '21',
								todayNum: '12'
							},
							{
								topImgUrl: '../../static/demo/topicpic/14.jpeg',
								title: '话题名称',
								desc: '我是话题描述',
								totalNum: '22',
								todayNum: '9'
							},
							{
								topImgUrl: '../../static/demo/topicpic/15.jpeg',
								title: '话题名称',
								desc: '我是话题描述',
								totalNum: '256',
								todayNum: '114'
							},
							{
								topImgUrl: '../../static/demo/topicpic/13.jpeg',
								title: '话题名称',
								desc: '我是话题描述',
								totalNum: '21',
								todayNum: '12'
							},
							{
								topImgUrl: '../../static/demo/topicpic/14.jpeg',
								title: '话题名称',
								desc: '我是话题描述',
								totalNum: '22',
								todayNum: '9'
							},
							{
								topImgUrl: '../../static/demo/topicpic/15.jpeg',
								title: '话题名称',
								desc: '我是话题描述',
								totalNum: '256',
								todayNum: '114'
							}
						]
					},
					{
						loadText: '上拉加载更多',
						list: []
					},
					{
						loadText: '上拉加载更多',
						list: []
					},
					{
						loadText: '上拉加载更多',
						list: []
					}
				],
				tabIndex: 0,
				// 顶部选项卡内容，从后台传入
				tabBarList: [
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
		components: {
			indexList,
			swiperTabHead,
			pullOnLoad,
			noThing,
			topicNewList
		},
		// 监听原生标题导航按钮点击事件, 事件来源介绍：官网-->介绍-->框架简介-->生命周期-->页面生命周期中
		onNavigationBarButtonTap(e) {
			switch (e.index){
				case 0: // 左侧的按钮
					break;
				case 1:  // 右侧按钮
					uni.navigateTo({
						url: '../add-input/add-input'
					});
					break;
				default:
					break;
			}
		},
		methods: {
			// 点击事件
			tabTap (index) {
				this.tabIndex = index
			},
			// 滑动事件
			swiperChange (e) {
				// 获取当前滑块的下标，改变对应的导航菜单的下标，使之同步改变
				this.tabIndex = e.detail.current
			},
			// 加载更多
			loadMore (tabIndex) {
				if (this.swiperList[tabIndex].loadText != '上拉加载更多') {
					return;
				}
				
				this.swiperList[tabIndex].loadText = '加载中....'
				
				// 此setTimeOut为模拟向后台发送请求获取数据
				// 注意：setTimeOut(function() {}) 如果使用这种方式，this在function(){}中就会不生效，需要在外面定义一个对象接收this，才可以在里面使用
				// var _self = this;
				// setTimeout(function () {
				// 	_self.swiperList[tabIndex].list.push(data);
				// }, 1000)
				setTimeout(()=> {
					
					// 数据加载完成
					var data = 
					{
						topImgUrl: '../../static/demo/topicpic/15.jpeg',
						title: '话题名称',
						desc: '我是话题描述',
						totalNum: 256,
						todayNum: 114
					}
					
					this.swiperList[tabIndex].list.push(data);
					this.swiperList[tabIndex].loadText = '上拉加载更多'
					
					// 如果没有数据
					// this.swiperList[tabIndex].loadText = '没有更多数据了'
				}, 1000)
			},
			// 合并数据
			mergeData (data, index, swIndex) {
				this.swiperList[swIndex].list[index] = data
			}
		}
	}
</script>

<style>
</style>
