<template>
	<view class="content">
<!-- 		<view class="schoolbag margin">
			<u-swiper :list="list1" keyName="image" showTitle indicator :autoplay="false" circular></u-swiper>
		</view> -->
		<view class="affairBag margin padding">
			<navigator url="" class="topTitle padding">
				<text class="jinnnang">党务锦囊</text>
				<view class="rightBox">
					<text class="more">查看更多</text>
					<image src="/static/images/zhe.png" alt="" class="rightLabel" />
				</view>
			</navigator>
			<view class="bagList">
				<view class="listMsg" v-for="(item, index) in bagList" :key="index" >
					<view class="image">
						<image src="../../static/testimg/t1.jpg" mode="aspectFill"></image>
					</view>
					<view class="viewText">
						<text class="listTitle">{{item.listTitle}}</text>
						<view class="viewTime">
							<text class="listTime">{{item.listTime}}</text>
						</view>
					</view>
				</view>
				<!-- <view class="listMsg">
					<view class="image">
						<image src="../../static/testimg/t1.jpg" mode="aspectFill"></image>
					</view>
					<view class="viewText">
						<text class="listTitle">英雄航天员景海鹏、朱杨柱和桂海潮word Time end of</text>
						<view class="viewTime">
							<text class="listTime">2022-2-3</text>
						</view>
					</view>
				</view> -->
			</view>
		</view>
		<view class="learnTest padding margin">
			<navigator url="" class="padding" @click="learnTest">
				<text class="studyTest">学习自测</text>
				<view class="rightBox">
					<text class="more">进入学习</text>
					<image src="/static/images/箭头.png" alt="" class="rightLabel" />
				</view>
			</navigator>
			<view class="bagList padding">
				<view class="listMsg">
					<text class="barText">知识学习</text>
					<u-line-progress :percentage="30" activeColor="#ffe759" class="processBar"></u-line-progress>
				</view>
				<view class="listMsg">
					<text class="barText">知识巩固</text>
					<u-line-progress :percentage="40" activeColor="#ffe759" class="processBar"></u-line-progress>
				</view>
				<view class="listMsg">
					<text class="barText">错题复习</text>
					<u-line-progress :percentage="30" activeColor="#ffe759" class="processBar"></u-line-progress>
				</view>
				<view class="listMsg">
					<text class="barText">考试</text>
					<u-line-progress :percentage="60" activeColor="#ffe759" class="processBar"></u-line-progress>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello',
				list1: [{
					image: 'https://cdn.uviewui.com/uview/swiper/swiper2.png',
					title: '昨夜星辰昨夜风，画楼西畔桂堂东',
				}, {
					image: 'https://cdn.uviewui.com/uview/swiper/swiper1.png',
					title: '身无彩凤双飞翼，心有灵犀一点通'
				}, {
					image: 'https://cdn.uviewui.com/uview/swiper/swiper3.png',
					title: '谁念西风独自凉，萧萧黄叶闭疏窗，沉思往事立残阳'
				}],
				bagList: [{
					listTitle: '英雄航天员景海鹏、朱杨柱和桂海潮',
					listTime: '2022-2-3'
				},{
					listTitle: '英雄航天员景海鹏、朱杨柱和桂海潮',
					listTime: '2022-2-3'
				},{
					listTitle: '英雄航天员景海鹏、朱杨柱和桂海潮word Time end of',
					listTime: '2022-2-3'
				},{
					listTitle: '英雄航天员景海鹏、朱杨柱和桂海潮',
					listTime: '2022-2-3'
				},
				]
			}
		},
		onLoad() {

		},
		methods: {
			learnTest() {
				uni.navigateTo({
					url: '/pages/index/learnTest'
				});
			}
		}
	}
</script>

<style scoped>
	page {
		box-sizing: border-box;
	}

	.margin {
		margin: 70rpx 30rpx;
	}

	.padding {
		padding: 15rpx 20rpx;
	}

	.pic {
		height: 1000rpx;
		width: 50%;
	}

	.affairBag,
	.learnTest {
		background-color: white;
		border-radius: 25rpx;
	}

	.affairBag .rightLabel {
		vertical-align: middle;
		/* line-height: 28rpx; */
		width: 26rpx;
		height: 26rpx;
		margin: 0;
	}

	.learnTest .rightLabel {
		vertical-align: middle;
		height: 30rpx;
		width: 30rpx;
		margin: 0;
	}

	.jinnnang,
	.studyTest {
		font-size: 32rpx;
		font-weight: 1000;
	}

	.affairBag .more {
		font-size: 28rpx;
		margin-right: 2rpx;
		color: #E2E2E2;
	}

	.learnTest .more {
		font-size: 28rpx;
		margin-right: 8rpx;
	}

	.learnTest .rightBox {
		border: 3rpx solid #ff8181;
		color: #ff8181;
		padding: 10rpx 20rpx 10rpx 30rpx;
		border-radius: 30rpx;
	}

	.rightBox {
		display: inline-block;
		float: right;
		line-height: 32rpx;
		/*与左侧字体同高*/
	}

	.affairBag .topTitle {
		border-bottom: 1rpx solid #eeeeee;
	}


	.studyTest .listMsg {
		margin: 20rpx;
	}

	.barText {
		font-size: 20rpx;
		color: #f3f3f3;
		border: 1rpx solid #2ea0fe;
		border-radius: 15rpx;
		background-color: #2ea0fe;
		padding: 7rpx 10rpx;
		margin-top: 20rpx;
		display: inline-block;
	}

	.processBar {
		margin: 10rpx 20rpx 20rpx 10rpx;
	}

	.affairBag .listMsg {
		margin: 10rpx 0rpx;
		display: flex;
	}

	.listMsg .image {
		margin: 10rpx 20rpx;
		width: 220rpx;
		height: 160rpx;
	}

	.listMsg .listTitle {
		font-size: 28rpx;
		font-weight: 800;
		line-height: 50rpx;
		overflow: hidden;
		display: -webkit-box;
		-webkit-line-clamp: 2;
		/* 指定显示的行数 */
		-webkit-box-orient: vertical;
	}

	.listMsg image {
		width: 100%;
		height: 100%;
		border-radius: 8rpx;
	}

	.listMsg .viewText {
		width: 360rpx;
		height: 100rpx;
		color: #6f6f6f;
		margin-top: 10rpx;
		padding: 10rpx;
		height: 160rpx;
		/* 或具体高度，根据行数和行高调整 */
		overflow: hidden;
		/* background-color: #2ea0fe; */
	}

	.listMsg .viewTime {
		font-size: 24rpx;
		color: #cbcbcb;
		position: relative;
		left: 230rpx;
		bottom: -20rpx;
	}
</style>