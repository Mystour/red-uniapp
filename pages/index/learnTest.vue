<template>
	<view>
		<!-- <h1>学习自测</h1> -->
		<view class="jifen">
			<view class="text"></view>
			<view class="text"></view>
			<view class="text"></view>
			<view class="text"></view>
		</view>
		<view class="u-demo-block__content">
			<view class="u-page__tag-item">
				<u-search v-model="value2" :show-action="false"></u-search>
			</view>
		</view>
		<view class="ul">
			<view class="li">
				<image src="../../static/images/星星.png" mode=""></image>
				<view class="">
					<text class="title" @click="toAnswerQuestion">党务测试 第一期</text>
				</view>
				<text class="time">2024-2-4</text>
			</view>
			<view class="li">
				<view class="">
					<text class="title">党务测试 第二期 党务测试 第一期 党务测试 第一期 党务测试 第一期 党务测试 第一期</text>
				</view>
				<text class="time">2024-2-4</text>
			</view>
			<view class="li">
				<view class="">
					<text class="title">党务测试 第三期</text>
				</view>
				<text class="time">2024-2-4</text>
			</view>
			<view class="li">
				<view class="">
					<text class="title">党务测试 第四期</text>
				</view>
				<text class="time">2024-2-4</text>
			</view>
			<view class="li">
				<view class="">
					<text class="title">党务测试 第五期</text>
				</view>
				<text class="time">2024-2-4</text>
			</view>
			<view class="li">
				<view class="">
					<text class="title">党务测试 第六期</text>
				</view>
				<text class="time">2024-2-4</text>
			</view>
			<view class="li">
				<view class="">
					<text class="title">党务测试1</text>
				</view>
				<text class="time">2024-2-4</text>
			</view>
			<view class="li">
				<view class="">
					<text class="title">党务测试1</text>
				</view>
				<text class="time">2024-2-4</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				value2: '第九期',
			}
		},
		methods: {
			toAnswerQuestion(){
				uni.navigateTo({
					url: '/pages/index/answerQuestion',
				});
			}
		}
	}
</script>

<style scoped>
	page {
		box-sizing: border-box;
	}

	.ul {
		/* background-color: antiquewhite; */
		margin: 50rpx 30rpx;
	}

	.ul .li {
		height: 150rpx;
		padding: 15rpx 30rpx;
		width: auto;
		margin: 20rpx 0rpx;
		background-color: white;
		border-radius: 10rpx;
	}
	
	.li image{
		width: 60rpx;
		height: 60rpx;
		float: right;
	}

	.title {
		line-height: 80rpx;
		font-size: 34rpx;
		font-weight: bold;
		width: 500rpx;
		overflow: hidden;
		display: -webkit-box;
		-webkit-line-clamp: 1;
		/* 指定显示的行数 */
		-webkit-box-orient: vertical;
	}

	.time {
		font-size: 25rpx;
		line-height: 30rpx;
		color: #cfcfcf;
	}

	/* 搜索框 */
	.u-demo-block__content {
		padding: 20rpx 10rpx;
		background-color: #fff;
	}

	.u-search {}

	.u-page__tag-item {
		/* @include flex(column); */
		display: flex;
		/* flex: 1 */
	}

	.m-t-10 {
		margin-top: 10px;
	}
</style>