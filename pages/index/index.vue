<template>
	<view>
		首页
		<!-- swiper-tab -->
		<swiper-tab-head :tabBarList="tabBarList" :tabIndex="tabIndex" @tabTap="tabTap"></swiper-tab-head>
		
		<view class="uni-tab-bar">
			<!-- 滑块视图容器 :style动态拼接单位，不支持使用upx @change改变时触发的方法 :current 当前所在滑块的下标 -->
			<swiper class="swiper-box" :style="{height: swiperHeight + 'px'}" @change="swiperChange" :current="tabIndex">
				<block v-for="(swiper, swIndex) in swiperList" :key="swIndex">
					<!-- swiper-item 每一个滑块，里面放置展示的内容 -->
					<swiper-item>
						<scroll-view scroll-y class="list" @scrolltolower="loadMore(tabIndex)">
							<template v-if="swiper.list.length > 0">
								<!-- 图文列表 -->
								<block v-for="(item, index) in swiper.list" :key="index">
									<!-- 引入封装的组件， :boxInfo和:index 为组件中props定义接收父组件的值 -->
									<index-list :boxInfo="item" :index="index" @mergeData="mergeData()"></index-list>
								</block>
								<!-- 上拉加载 -->
								<pull-on-load :loadText="swiper.loadText"></pull-on-load>
							</template>
							<template v-else>
								<!-- 没有内容 -->
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
	
	export default {
		// 当页面渲染完成后执行
		onLoad() {
			// this.init()
			uni.getSystemInfo({
			    success: (res) => {
					let height = res.windowHeight - uni.upx2px(100);
					this.swiperHeight = height;
			    }
			});
		},
		// 原生导航栏点击监听
		onNavigationBarSearchInputClicked () {
			uni.navigateTo({
				url: '../search/search'
			})
		},
		data() {
			return {
				swiperHeight: 0,
				dataList: [],
				swiperList: [
					{
						loadText: '上拉加载更多',
						list: [
							{
								userPic:'../../static/img/index/user.jpg', //  用户图片
								userName: '小明', // 用户名
								isFocus: false, // 是否关注，false：未关注，true：关注
								conTitile: '小明巅峰时刻', // 内容标题
								conType:'1', // 内容类型，1：图片，2：视频
								imgPath: '../../static/img/index/background.jpg', // 图片路径
								videoPath: '', // 视频路径
								videoPlayNum: '', // 视频播放次数
								videoTime: '', // 视频时长
								dcInfo: { // 点赞踩信息
									dcType: '1', // 点赞踩类型，0：为操作，1:点赞，2：踩
									dzNum: '221', // 点赞数
									cNum: '12' // 踩数
								},
								commentNum: '33', // 评论数
								shareNum: '12' // 分享数
							},
							{
								userPic:'../../static/img/index/user.jpg', //  用户图片
								userName: '宁王', // 用户名
								isFocus: true, // 是否关注，false：未关注，true：关注
								conTitile: '宁王巅峰时刻', // 内容标题
								conType:'2', // 内容类型，1：图片，2：视频
								imgPath: '../../static/img/index/background.jpg', // 图片路径
								videoPath: '', // 视频路径
								videoPlayNum: '20W', // 视频播放次数
								videoTime: '2:47', // 视频时长
								dcInfo: { // 点赞踩信息
									dcType: '1', // 点赞踩类型，0：为操作，1:点赞，2：踩
									dzNum: '1313', // 点赞数
									cNum: '444' // 踩数
								},
								commentNum: '9926', // 评论数
								shareNum: '5555' // 分享数
							}
						]
					},
					{
						loadText: '上拉加载更多',
						list: [
							{
								userPic:'../../static/img/index/user.jpg', //  用户图片
								userName: '小明', // 用户名
								isFocus: false, // 是否关注，false：未关注，true：关注
								conTitile: '小明巅峰时刻', // 内容标题
								conType:'1', // 内容类型，1：图片，2：视频
								imgPath: '../../static/img/index/background.jpg', // 图片路径
								videoPath: '', // 视频路径
								videoPlayNum: '', // 视频播放次数
								videoTime: '', // 视频时长
								dcInfo: { // 点赞踩信息
									dcType: '1', // 点赞踩类型，0：为操作，1:点赞，2：踩
									dzNum: '221', // 点赞数
									cNum: '12' // 踩数
								},
								commentNum: '33', // 评论数
								shareNum: '12' // 分享数
							},
							{
								userPic:'../../static/img/index/user.jpg', //  用户图片
								userName: '宁王', // 用户名
								isFocus: true, // 是否关注，false：未关注，true：关注
								conTitile: '宁王巅峰时刻', // 内容标题
								conType:'2', // 内容类型，1：图片，2：视频
								imgPath: '../../static/img/index/background.jpg', // 图片路径
								videoPath: '', // 视频路径
								videoPlayNum: '20W', // 视频播放次数
								videoTime: '2:47', // 视频时长
								dcInfo: { // 点赞踩信息
									dcType: '1', // 点赞踩类型，0：为操作，1:点赞，2：踩
									dzNum: '1313', // 点赞数
									cNum: '444' // 踩数
								},
								commentNum: '9926', // 评论数
								shareNum: '5555' // 分享数
							},
							{
								userPic:'../../static/img/index/user.jpg', //  用户图片
								userName: '小明', // 用户名
								isFocus: false, // 是否关注，false：未关注，true：关注
								conTitile: '小明巅峰时刻', // 内容标题
								conType:'1', // 内容类型，1：图片，2：视频
								imgPath: '../../static/img/index/background.jpg', // 图片路径
								videoPath: '', // 视频路径
								videoPlayNum: '', // 视频播放次数
								videoTime: '', // 视频时长
								dcInfo: { // 点赞踩信息
									dcType: '1', // 点赞踩类型，0：为操作，1:点赞，2：踩
									dzNum: '221', // 点赞数
									cNum: '12' // 踩数
								},
								commentNum: '33', // 评论数
								shareNum: '12' // 分享数
							},
							{
								userPic:'../../static/img/index/user.jpg', //  用户图片
								userName: '宁王', // 用户名
								isFocus: true, // 是否关注，false：未关注，true：关注
								conTitile: '宁王巅峰时刻', // 内容标题
								conType:'2', // 内容类型，1：图片，2：视频
								imgPath: '../../static/img/index/background.jpg', // 图片路径
								videoPath: '', // 视频路径
								videoPlayNum: '20W', // 视频播放次数
								videoTime: '2:47', // 视频时长
								dcInfo: { // 点赞踩信息
									dcType: '1', // 点赞踩类型，0：为操作，1:点赞，2：踩
									dzNum: '1313', // 点赞数
									cNum: '444' // 踩数
								},
								commentNum: '9926', // 评论数
								shareNum: '5555' // 分享数
							}
						]
					},
					{
						loadText: '上拉加载更多',
						list: [
							{
								userPic:'../../static/img/index/user.jpg', //  用户图片
								userName: '小明', // 用户名
								isFocus: false, // 是否关注，false：未关注，true：关注
								conTitile: '小明巅峰时刻', // 内容标题
								conType:'1', // 内容类型，1：图片，2：视频
								imgPath: '../../static/img/index/background.jpg', // 图片路径
								videoPath: '', // 视频路径
								videoPlayNum: '', // 视频播放次数
								videoTime: '', // 视频时长
								dcInfo: { // 点赞踩信息
									dcType: '1', // 点赞踩类型，0：为操作，1:点赞，2：踩
									dzNum: '221', // 点赞数
									cNum: '12' // 踩数
								},
								commentNum: '33', // 评论数
								shareNum: '12' // 分享数
							},
							{
								userPic:'../../static/img/index/user.jpg', //  用户图片
								userName: '宁王', // 用户名
								isFocus: true, // 是否关注，false：未关注，true：关注
								conTitile: '宁王巅峰时刻', // 内容标题
								conType:'2', // 内容类型，1：图片，2：视频
								imgPath: '../../static/img/index/background.jpg', // 图片路径
								videoPath: '', // 视频路径
								videoPlayNum: '20W', // 视频播放次数
								videoTime: '2:47', // 视频时长
								dcInfo: { // 点赞踩信息
									dcType: '1', // 点赞踩类型，0：为操作，1:点赞，2：踩
									dzNum: '1313', // 点赞数
									cNum: '444' // 踩数
								},
								commentNum: '9926', // 评论数
								shareNum: '5555' // 分享数
							},
							{
								userPic:'../../static/img/index/user.jpg', //  用户图片
								userName: '小明', // 用户名
								isFocus: false, // 是否关注，false：未关注，true：关注
								conTitile: '小明巅峰时刻', // 内容标题
								conType:'1', // 内容类型，1：图片，2：视频
								imgPath: '../../static/img/index/background.jpg', // 图片路径
								videoPath: '', // 视频路径
								videoPlayNum: '', // 视频播放次数
								videoTime: '', // 视频时长
								dcInfo: { // 点赞踩信息
									dcType: '1', // 点赞踩类型，0：为操作，1:点赞，2：踩
									dzNum: '221', // 点赞数
									cNum: '12' // 踩数
								},
								commentNum: '33', // 评论数
								shareNum: '12' // 分享数
							},
							{
								userPic:'../../static/img/index/user.jpg', //  用户图片
								userName: '宁王', // 用户名
								isFocus: true, // 是否关注，false：未关注，true：关注
								conTitile: '宁王巅峰时刻', // 内容标题
								conType:'2', // 内容类型，1：图片，2：视频
								imgPath: '../../static/img/index/background.jpg', // 图片路径
								videoPath: '', // 视频路径
								videoPlayNum: '20W', // 视频播放次数
								videoTime: '2:47', // 视频时长
								dcInfo: { // 点赞踩信息
									dcType: '1', // 点赞踩类型，0：为操作，1:点赞，2：踩
									dzNum: '1313', // 点赞数
									cNum: '444' // 踩数
								},
								commentNum: '9926', // 评论数
								shareNum: '5555' // 分享数
							},
							{
								userPic:'../../static/img/index/user.jpg', //  用户图片
								userName: '小明', // 用户名
								isFocus: false, // 是否关注，false：未关注，true：关注
								conTitile: '小明巅峰时刻', // 内容标题
								conType:'1', // 内容类型，1：图片，2：视频
								imgPath: '../../static/img/index/background.jpg', // 图片路径
								videoPath: '', // 视频路径
								videoPlayNum: '', // 视频播放次数
								videoTime: '', // 视频时长
								dcInfo: { // 点赞踩信息
									dcType: '1', // 点赞踩类型，0：为操作，1:点赞，2：踩
									dzNum: '221', // 点赞数
									cNum: '12' // 踩数
								},
								commentNum: '33', // 评论数
								shareNum: '12' // 分享数
							},
							{
								userPic:'../../static/img/index/user.jpg', //  用户图片
								userName: '宁王', // 用户名
								isFocus: true, // 是否关注，false：未关注，true：关注
								conTitile: '宁王巅峰时刻', // 内容标题
								conType:'2', // 内容类型，1：图片，2：视频
								imgPath: '../../static/img/index/background.jpg', // 图片路径
								videoPath: '', // 视频路径
								videoPlayNum: '20W', // 视频播放次数
								videoTime: '2:47', // 视频时长
								dcInfo: { // 点赞踩信息
									dcType: '1', // 点赞踩类型，0：为操作，1:点赞，2：踩
									dzNum: '1313', // 点赞数
									cNum: '444' // 踩数
								},
								commentNum: '9926', // 评论数
								shareNum: '5555' // 分享数
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
			noThing
		},
		methods: {
			init () {
				console.log('初始化数据----')
				// 从后台获取数据
				this.dataList = [
					{
						userPic:'../../static/img/index/user.jpg', //  用户图片
						userName: '小明', // 用户名
						isFocus: false, // 是否关注，false：未关注，true：关注
						conTitile: '小明巅峰时刻', // 内容标题
						conType:'1', // 内容类型，1：图片，2：视频
						imgPath: '../../static/img/index/background.jpg', // 图片路径
						videoPath: '', // 视频路径
						videoPlayNum: '', // 视频播放次数
						videoTime: '', // 视频时长
						dcInfo: { // 点赞踩信息
							dcType: '1', // 点赞踩类型，0：为操作，1:点赞，2：踩
							dzNum: '221', // 点赞数
							cNum: '12' // 踩数
						},
						commentNum: '33', // 评论数
						shareNum: '12' // 分享数
					},
					{
						userPic:'../../static/img/index/user.jpg', //  用户图片
						userName: '宁王', // 用户名
						isFocus: true, // 是否关注，false：未关注，true：关注
						conTitile: '宁王巅峰时刻', // 内容标题
						conType:'2', // 内容类型，1：图片，2：视频
						imgPath: '../../static/img/index/background.jpg', // 图片路径
						videoPath: '', // 视频路径
						videoPlayNum: '20W', // 视频播放次数
						videoTime: '2:47', // 视频时长
						dcInfo: { // 点赞踩信息
							dcType: '1', // 点赞踩类型，0：为操作，1:点赞，2：踩
							dzNum: '1313', // 点赞数
							cNum: '444' // 踩数
						},
						commentNum: '9926', // 评论数
						shareNum: '5555' // 分享数
					}
				]
			},
			// 点击菜单
			tabTap (index) {
				this.tabIndex = index
			},
			// 滑动改变时
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
				setTimeout(()=> {
					
					var data = 
					{
						userPic:'../../static/img/index/user.jpg', //  用户图片
						userName: '小狗.....', // 用户名
						isFocus: false, // 是否关注，false：未关注，true：关注
						conTitile: '小狗堕落时刻', // 内容标题
						conType:'1', // 内容类型，1：图片，2：视频
						imgPath: '../../static/img/index/background.jpg', // 图片路径
						videoPath: '', // 视频路径
						videoPlayNum: '', // 视频播放次数
						videoTime: '', // 视频时长
						dcInfo: { // 点赞踩信息
							dcType: '1', // 点赞踩类型，0：为操作，1:点赞，2：踩
							dzNum: '22155', // 点赞数
							cNum: '0' // 踩数
						},
						commentNum: '332323', // 评论数
						shareNum: '1234' // 分享数
					}
					
					this.swiperList[tabIndex].list.push(data);
					this.swiperList[tabIndex].loadText = '上拉加载更多'
					
				}, 1000)
			},
			// 合并数据
			mergeData (data, index) {
				this.swiperList[this.tabIndex].list[index] = data
			}
		}
	}
</script>

<style>
</style>
