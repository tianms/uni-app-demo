<template>
	<view>
		<!-- 自定义导航栏 -->
		<news-nav-bar :tabBars="tabBars" :tabIndex="tabIndex" @change-tab="changeTab"></news-nav-bar>
	
		<view class="uni-tab-bar">
			<!-- 滑块视图容器 :style动态拼接单位，不支持使用upx，可以通过转换计算后使用px -->
			<!-- @@change监听改变，改变时触发swiperChange事件，同步顶部选项卡的下标使两部分保持一致 -->
			<!-- :current 当前所在滑块的下标，与顶部选项卡的下标一致 -->
			<swiper class="swiper-box" :style="{height: swiperHeight + 'px'}" @change="swiperChange" :current="tabIndex">
				<!-- swiper-item 每一个滑块，里面放置当前滑块要展示的内容 -->
				<!-- 关注 -->
				<swiper-item>
					<!-- 下面这个滑块视图展示内容，所以为纵向滚动 -->
					<!-- @scrolltolower触底事件 -->
					<scroll-view scroll-y class="list" @scrolltolower="loadMoreGz()">
						<!-- 图文内容 -->
						<block v-for="(item, index) in gzList.list" :key="index">
							<common-list :item="item" :index="index" @mergeData="mergeData()"></common-list>
						</block>
						<!-- 上拉加载 -->
						<pull-on-load :loadText="gzList.loadText"></pull-on-load>
					</scroll-view>
				</swiper-item>
				<!-- 话题 -->
				<swiper-item>
					<!-- 下面这个滑块视图展示内容，所以为纵向滚动 -->
					<!-- @scrolltolower触底事件 -->
					<scroll-view scroll-y class="list" >
						<!-- 搜索框 -->
						<!-- 官网->组件->表单组件->input -->
						<view class="search-input">
							<!-- placeholder-class 占位符的class样式，里面直接对应class名称 图表使用一致 -->
							<input class="uni-input" type="text" placeholder-class="icon iconfont icon-sousuo topic-search" placeholder="搜索内容"/>
						</view>
						<!-- 轮播图 -->
						<!-- indicator-dots 面板指示点，就是图片中间的小点  true显示 -->
						<!-- autoplay是否自动播放，true自动播放  interval间隔时间  duration动画过度时间 -->
						<swiper class="topic-swiper" :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
							<block v-for="(item, index) in topic.swiperBanner" :key="index">
								<swiper-item>
									<image :src="item.src" mode="widthFix" lazy-load></image>
								</swiper-item>
							</block>
						</swiper>
						<!-- 热门分类 -->
						<topic-nav :navList="topic.navList"></topic-nav>
						<!-- 最近更新 -->
						<topic-new-list :newList="topic.newList"></topic-new-list>
					</scroll-view>
				</swiper-item>
			</swiper>
		</view>
	</view>
</template>

<script>
	import newsNavBar from '../../components/news/news-nav-bar.vue';
	import commonList from '../../components/common/common-list.vue';
	// 引入上拉加载组件
	import pullOnLoad from '../../components/common/pull-on-load.vue';
	// 标签组件
	import topicNav from '../../components/news/topic-nav.vue';
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
		data() {
			return {
				swiperHeight: 0,
				tabIndex: 0,
				tabBars: [
					{name: '关注', id: 'guanzhu'},
					{name: '话题', id: 'huati'}
				],
				gzList: {
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
				// 话题信息
				topic: {
					// banner图列表集合
					swiperBanner: [
						{'src': '../../static/demo/banner2.jpg'},
						{'src': '../../static/demo/banner2.jpg'},
						{'src': '../../static/demo/banner2.jpg'}
					],
					// 热门标签内容集合
					navList: [
						{'name': '最新'},
						{'name': '游戏'},
						{'name': '打卡'},
						{'name': '情感'},
						{'name': '故事'},
						{'name': '喜爱'}
					],
					// 最近更新内容集合
					newList: [
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
				}
			}
		},
		components: {
			newsNavBar,
			commonList,
			pullOnLoad,
			topicNav,
			topicNewList
		},
		methods: {
			// 合并数据
			mergeData (data, index) {
				this.list[index] = data
			},
			// 改变点击的菜单
			changeTab (index) {
				this.tabIndex = index
			},
			// 点击切换
			swiperChange (e) {
				// 获取当前滑块的下标，改变对应的导航菜单的下标，使之同步改变
				this.tabIndex = e.detail.current
			},
			// 加载更多
			loadMoreGz () {
				if (this.gzList.loadText != '上拉加载更多') {
					return;
				}
				
				this.gzList.loadText = '加载中....'
				
				// 此setTimeOut为模拟向后台发送请求获取数据
				// 注意：setTimeOut(function() {}) 如果使用这种方式，this在function(){}中就会不生效，需要在外面定义一个对象接收this，才可以在里面使用
				// var _self = this;
				// setTimeout(function () {
				// 	_self.gzList.list.push(data);
				// }, 1000)
				setTimeout(()=> {
					
					// 数据加载完成
					var data = 
					{
						userPic: '../../static/img/index/user.jpg',
						userName: '发发发',
						userSex: 0, // 0：男，1：女
						userAge: 25 + this.gzList.list.length,
						isFocus: false,
						title: '我是标题吞吞吐吐拖',
						titlePic: '../../static/demo/datapic/13.jpg',
						video: false,
						share: false,
						address: '深圳 龙岗',
						shareNum: 20 + this.gzList.list.length,
						commentNum: 30 + this.gzList.list.length,
						goodNum: 20 + this.gzList.list.length
					}
					
					this.gzList.list.push(data);
					this.gzList.loadText = '上拉加载更多'
					
					// 如果没有数据
					// this.gzList.loadText = '没有更多数据了'
				}, 1000)
			}
		}
	}
</script>

<style>
	/* 搜索框 */
	.search-input {
		padding: 20upx;
	}
	/* 搜索框中的输入框 */
	.search-input input {
		background: #F4F4F4;
		border-radius: 10upx;
	}
	/* 占位符样式 */
	.topic-search {
		display: flex;
		justify-content: center;
		font-size: 28upx;
	}
	/* 搜索框 */
	
	/* 轮播图 */
	.topic-swiper {
		padding: 0 20upx 20upx 20upx;
	}
	/* 轮播图中的图片 */
	.topic-swiper image {
		width: 100%;
		border-radius: 10upx;
	}
	/* 轮播图 */
	
	
</style>
