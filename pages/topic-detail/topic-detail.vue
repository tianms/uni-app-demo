<template>
	<view>
		<!-- 话题信息 -->
		<topic-info :topicInfo="topicInfo"></topic-info>
		<!-- tabbar 选项卡 -->
		<swiper-tab-head 
			:tabBarList="tabBarList" 
			:tabIndex="tabIndex" 
			@tabTap="tabTap"
			swiperTabStyle="border-bottom: 0"
			swiperTabItemStyle="width: 50%"
			></swiper-tab-head>
		<!-- 列表信息 -->
		<view>
			<block v-for="(item, index) in topicDetailList" :key="index">
				<!-- template标签作用判断使用， 判断选中的是哪个，隐藏未选中的标签 -->
				<template v-if="tabIndex == index">
					<!-- 列表 -->
					<block v-for="(topicDetail, topicIndex) in item.list" :key="topicIndex">
						<common-list :item="topicDetail" :index="topicIndex" @mergeData="mergeData()"></common-list>
					</block>
					<!-- 上拉加载 -->
					<pull-on-load :loadText="item.loadText"></pull-on-load>
				</template>
			</block>
		</view>
	</view>
</template>

<script>
	import topicInfo from '../../components/topic/topic-info.vue';
	// 引入swiper-tab滑动菜单组件
	import swiperTabHead from '../../components/swiperTab/swiper-tab-head.vue';
	// 公共列表组件
	import commonList from '../../components/common/common-list.vue';
	// 引入上拉加载组件
	import pullOnLoad from '../../components/common/pull-on-load.vue';
	export default {
		components: {
			topicInfo,
			swiperTabHead,
			commonList,
			pullOnLoad
		},
		data() {
			return {
				topicInfo: {
					topicImgUrl: '../../static/demo/topicpic/13.jpeg',
					topicTitle: '忆往事, 敬余生',
					topicDesc: '我是描述',
					totalTopicNum: 999,
					todayTopicNum: 666
				},
				// tabbar 选项卡列表
				tabBarList: [
					{
						name: '默认',
						id: 'moren'
					}, 
					{
						name: '最新',
						id: 'zuixin'
					}
				],
				tabIndex: 0,
				// 与tabBarList 个数一致，每一个对应每一个tabBar
				topicDetailList: [
					{
						loadText: '上拉加载更多',
						list: [
							// 视频
							{
								userPic: '../../static/img/index/user.jpg',
								userName: '收拾收拾',
								userSex: 0, // 0：男，1：女
								userAge: 25,
								isFocus: false,
								title: '我是标题少时诵诗书',
								titlePic: '../../static/demo/datapic/13.jpg',
								video: {
									playNum: '20w',
									playLong: '2:47'
								},
								share: false,
								address: '深圳 龙岗',
								shareNum: 207,
								commentNum: 301,
								goodNum: 202,
							},
							// 图文
							{
								userPic: '../../static/img/index/user.jpg',
								userName: '发发发',
								userSex: 0, // 0：男，1：女
								userAge: 25,
								isFocus: false,
								title: '我是标题吞吞吐吐拖',
								titlePic: '../../static/demo/datapic/13.jpg',
								video: false,
								share: false,
								address: '深圳 龙岗',
								shareNum: 20,
								commentNum: 30,
								goodNum: 20
							},
							// 文字
							{
								userPic: '../../static/img/index/user.jpg',
								userName: '呜呜呜呜',
								userSex: 0, // 0：男，1：女
								userAge: 25,
								isFocus: false,
								title: '我是标题呜呜呜呜',
								titlePic: '',
								video: false,
								share: false,
								address: '深圳 龙岗',
								shareNum: 20,
								commentNum: 60,
								goodNum: 40
							},
							// 分享
							{
								userPic: '../../static/img/index/user.jpg',
								userName: '反反复复',
								userSex: 0, // 0：男，1：女
								userAge: 25,
								isFocus: false,
								title: '我是标题反反复复付',
								titlePic: '',
								video: false,
								share: {
									shareTitle: '',
									sharePic: '../../static/demo/datapic/14.jpg'
								},
								address: '深圳 龙岗',
								shareNum: 250,
								commentNum: 360,
								goodNum: 270
							}
						]
					},
					{
						loadText: '上拉加载更多',
						list: [
							// 文字
							{
								userPic: '../../static/img/index/user.jpg',
								userName: '呜呜呜呜',
								userSex: 0, // 0：男，1：女
								userAge: 25,
								isFocus: false,
								title: '我是标题呜呜呜呜',
								titlePic: '',
								video: false,
								share: false,
								address: '深圳 龙岗',
								shareNum: 20,
								commentNum: 60,
								goodNum: 40
							},
							// 分享
							{
								userPic: '../../static/img/index/user.jpg',
								userName: '反反复复',
								userSex: 0, // 0：男，1：女
								userAge: 25,
								isFocus: false,
								title: '我是标题反反复复付',
								titlePic: '',
								video: false,
								share: {
									shareTitle: '',
									sharePic: '../../static/demo/datapic/14.jpg'
								},
								address: '深圳 龙岗',
								shareNum: 250,
								commentNum: 360,
								goodNum: 270
							},
							// 视频
							{
								userPic: '../../static/img/index/user.jpg',
								userName: '收拾收拾',
								userSex: 0, // 0：男，1：女
								userAge: 25,
								isFocus: false,
								title: '我是标题少时诵诗书',
								titlePic: '../../static/demo/datapic/13.jpg',
								video: {
									playNum: '20w',
									playLong: '2:47'
								},
								share: false,
								address: '深圳 龙岗',
								shareNum: 207,
								commentNum: 301,
								goodNum: 202,
							},
							// 图文
							{
								userPic: '../../static/img/index/user.jpg',
								userName: '发发发',
								userSex: 0, // 0：男，1：女
								userAge: 25,
								isFocus: false,
								title: '我是标题吞吞吐吐拖',
								titlePic: '../../static/demo/datapic/13.jpg',
								video: false,
								share: false,
								address: '深圳 龙岗',
								shareNum: 20,
								commentNum: 30,
								goodNum: 20
							}
						]
					}
				]
			}
		},
		// 官网->框架简介->生命周期->页面生命周期
		// 页面上拉触底事件的处理函数
		onReachBottom() {
			this.loadMore();
		},
		// 官网->接口->界面->下拉刷新
		// 下拉刷新
		onPullDownRefresh() {
			this.getDataList();
		},
		methods: {
			// 点击选项卡
			tabTap (index) {
				this.tabIndex = index
			},
			// 加载更多
			loadMore () {
				if (this.topicDetailList[this.tabIndex].loadText != '上拉加载更多') {
					return;
				}
				
				this.topicDetailList[this.tabIndex].loadText = '加载中....'
				
				// 此setTimeOut为模拟向后台发送请求获取数据
				// 注意：setTimeOut(function() {}) 如果使用这种方式，this在function(){}中就会不生效，需要在外面定义一个对象接收this，才可以在里面使用
				// var _self = this;
				// setTimeout(function () {
				// 	_self.gzList.list.push(data);
				// }, 1000)
				setTimeout(()=> {
					
					// 从后端获取数据 TODO
					// 数据加载完成
					var data = 
					{
						userPic: '../../static/img/index/user.jpg',
						userName: '发发发',
						userSex: 0, // 0：男，1：女
						userAge: 25 + this.topicDetailList[this.tabIndex].list.length,
						isFocus: false,
						title: '我是标题吞吞吐吐拖',
						titlePic: '../../static/demo/datapic/13.jpg',
						video: false,
						share: false,
						address: '深圳 龙岗',
						shareNum: 20 + this.topicDetailList[this.tabIndex].list.length,
						commentNum: 30 + this.topicDetailList[this.tabIndex].list.length,
						goodNum: 20 + this.topicDetailList[this.tabIndex].list.length
					}
					
					this.topicDetailList[this.tabIndex].list.push(data);
					this.topicDetailList[this.tabIndex].loadText = '上拉加载更多'
					
					// 如果没有数据
					// this.topicDetailList[this.tabIndex].loadText = '没有更多数据了'
				}, 1000)
			},
			// 下拉刷新获取数据
			getDataList () {
				// 模拟请求
				setTimeout(()=> {
					// Step:1 从服务端获取数据
					let arr = [
						{
							userPic: '../../static/img/index/user.jpg',
							userName: '呜呜呜呜',
							userSex: 0, // 0：男，1：女
							userAge: 25,
							isFocus: false,
							title: '我是标题呜呜呜呜',
							titlePic: '',
							video: false,
							share: false,
							address: '深圳 龙岗',
							shareNum: 20,
							commentNum: 60,
							goodNum: 40
						}
					];
					// Step:2 更新数据
					this.topicDetailList[this.tabIndex].list = arr;
					// this.topicDetailList[this.tabIndex].list = arr;
					// Step:3 关闭下拉刷新
					// 官网->接口->界面->下拉刷新
					uni.stopPullDownRefresh();
				}, 2000);
			}
		}
	}
</script>

<style>
	
</style>
