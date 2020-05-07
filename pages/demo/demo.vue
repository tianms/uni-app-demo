<template>
	<view>
		<!-- flex布局演示 -->
		<view class="flux-box">
				<view class="box-item">1</view>
				<view class="box-item">2</view>
				<view class="box-item">3</view>
				<view class="box-item">4</view>
				<view class="box-item">5</view>
				<view class="box-item">6</view>
				
		</view>
		<!-- flex布局演示 -->
		
		<!-- view演示 -->
		<!-- hover-class点击的属性, hover-stay-time：手指松开后保持多久的样式-->
		<view class="view-box animated" 
		hover-class="view-box-hover rubberBand"
		hover-stay-time="800"
		id="view2">第一个view</view>
		<!-- view演示 -->
		
		<!-- text演示 -->
		<!-- 文本支持：\n换行符直接写入   -->
		<!-- selectable:文本是否可选   -->
		<text :selectable="true">这是text\n 这是text\n 这是text\n 这是text\n 这是text</text>
		<!-- text演示 -->
		
		<!-- css3演示 -->
		<view class="box">
			<text>text组件</text>
			<view>1</view>
			<view>2</view>
			<view>3</view>
			<view>4</view>
			<view>5</view>
			<view>6</view>
		</view>
		<!-- css3演示 -->
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			
		}
	}
</script>

<style>
/** view演示 **/
.view-box {
	width: 200upx; /** 转换为px看官网 **/
	height: 200upx;
	background: #007AFF;
	color: #FFFFFF;
	margin: 200upx;
}
.view-box-hover{
	background: red;
}
#view2, text{
	background: yellow;
}
/** view演示 **/

/** css3演示 **/
.box{
	width: 300upx;
	height: 300upx;
	background: #007AFF;
	color: #FFFFFF;
	margin: 100upx;
	padding: 50upx;
}
.box view {
	font-size: 40upx;
}
/**  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ **/
/* .box>view:nth-child(1) {
	background: #09BB07;
}
.box>view:nth-child(2) {
	background: red;
}
.box>view:nth-child(3) {
	background: pink;
} */
/**  每一行两种选择器 **/
/* .box>view:nth-of-type(1) {
	background: #09BB07;
}
.box>view:nth-of-type(2) {
	background: red;
}
.box>view:nth-of-type(3) {
	background: pink;
} */
/**  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ **/
/***0-------------------------------------***/

/* .box>view:first-child {
	background: #09BB07;
}
.box>view:last-child {
	background: pink;
 }*/
/**  开始结尾两种选择器 **/
/* .box>view:first-of-type {
	background: #09BB07;
}
.box>view:last-of-type {
	background: pink;
} */
/***0-------------------------------------***/
/**  ----------===============---------------------**/
/* .box>view:nth-of-type(2n-1) {
	background: #09BB07;
}
.box>view:nth-of-type(2n) {
	background: pink;
} */
/**  奇偶两种选择器 **/
.box>view:nth-of-type(even) {
	background: red;
}
.box>view:nth-of-type(odd) {
	background: pink;
}
/**  ----------===============---------------------**/
/** css3演示 **/


/** flex布局演示 **/
.flux-box {
	height: 500upx;
	width: 100%;
	border: 1upx solid #333333;
	display: flex;
	/* flex-wrap: wrap; */  /**  换行 **/
	/* justify-content: center; */ /** 水平方向布局，常用居中  */
	/* align-items: center; */ /** 竖直方向布局，常用居中 */
	/* flex-direction: column; */ /** 按指定顺序类型排列，column,row */
	/* align-self: flex-end; */ /** 竖直布局 */
}
.box-item{
	background: #007AFF;
	color: #FFFFFF;
	height: 200upx;
	width: 200upx;
	/* line-height: 200upx; */
	font-size: 30upx;
	font-weight: bold;
	/* text-align: center; */
	display: flex;
	align-items: center;
	justify-content: center;
}
.box-item:nth-of-type(odd){
	background: red;
}
.box-item:nth-of-type(even){
	background: pink;
}
/* .box-item:first-of-type {*/
	/* flex-shrink: 0; */ /** 是否被压缩，默认1被压缩，0：不压缩 */
/* } */
.box-item:nth-of-type(1) {
	flex: 1; /** 占得比例大小 */
}
.box-item:nth-of-type(2) {
	flex: 2;
}
.box-item:nth-of-type(3) {
	flex: 1;
}
/** flex布局演示 **/
</style>
