<template>
	<view class="content">
		<view class="action">
			<view class="author">
				<view class="avatar-container">
					<image :src="avatarUrl" mode="aspectFill" class="avatar"></image>
					<!-- 如果有需要，可以在这里添加更多交互元素，比如编辑头像的按钮 -->
				</view>
				<view class="authorName">
					党建中心
				</view>
				<view class="action-time">
					2023-2-18
				</view>
			</view>
			<view class="action-content">
				<view class="content-image">
					<image src="../../static/testimg/志愿.jpg" mode="aspectFill"></image>
				</view>
			</view>
			<view class="content-text">
				<text >
					“百姓志愿”——天津和平志愿服务的鲜活实践
				</text>
			</view>
		</view>
		<view class="action">
			<view class="author">
				<view class="avatar-container">
					<image :src="avatarUrl" mode="aspectFill" class="avatar"></image>
					<!-- 如果有需要，可以在这里添加更多交互元素，比如编辑头像的按钮 -->
				</view>
				<view class="authorName">
					党建中心
				</view>
				<view class="action-time">
					2023-2-18
				</view>
			</view>
			<view class="action-content">
				<view class="content-image">
					<image src="../../static/testimg/志愿.jpg" mode="aspectFill"></image>
				</view>
			</view>
			<view class="content-text">
				<text >
					“百姓志愿”——天津和平志愿服务的鲜活实践
				</text>
			</view>
		</view>
		<view class="action">
			<view class="author">
				<view class="avatar-container">
					<image :src="avatarUrl" mode="aspectFill" class="avatar"></image>
					<!-- 如果有需要，可以在这里添加更多交互元素，比如编辑头像的按钮 -->
				</view>
				<view class="authorName">
					党建中心
				</view>
				<view class="action-time">
					2023-2-18
				</view>
			</view>
			<view class="action-content">
				<view class="content-image">
					<image src="../../static/testimg/志愿.jpg" mode="aspectFill"></image>
				</view>
			</view>
			<view class="content-text">
				<text >
					“百姓志愿”——天津和平志愿服务的鲜活实践
				</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				avatarUrl: '../../static/testimg/4231643-图片-1.jpg', // 头像的URL
			};
		},
		methods: {

		},
	};
</script>

<style scoped>
	.content{
		background-color: #F0F0F8;
	}
	.action {
		margin: 30rpx 20rpx;
		border-radius: 20rpx;
		/* height: 1000rpx; */
		background-color: #ffffff;
	}
	.action-time{
		margin: 20rpx 30rpx;
		font-size: 24rpx;
		color: #cbcbcb;
		float: right;
	}
	.author {
		padding: 20rpx 30rpx;
		border-bottom: 1rpx solid #f1f1f1;
	}

	.avatar-container {
		display: inline-block;
	}

	.avatar {
		width: 80rpx;
		height: 80rpx;
		border-radius: 50%;
		vertical-align: middle;
	}

	.authorName {
		display: inline-block;
		margin-left: 20rpx;
		font-size: 28rpx;
		font-weight: bold;
	}

	.content-image {
		width: 100%;
	}

	.content-image image {
		width: 100%;
		height: 350rpx;
	}
	.content-text{
		font-size: 30rpx;
		font-weight: 600;
		height: 80rpx;
		margin: 20rpx 20rpx;
	}
	.action-content{
		margin: 0rpx 0rpx 30rpx 0rpx;
	}
</style>