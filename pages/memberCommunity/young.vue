<template>
	<view class="container">
		<view class="tab-bar">
			<view v-for="(item, index) in tabs" :key="index" :class="{ 'active': currentTabIndex === index }"
				@tap="switchTab(index)">{{ item.title }}</view>
		</view>

		<view class="content">
			<Tab1 v-if="currentTabIndex === 0" />
			<Tab2 v-else-if="currentTabIndex === 1" />
			<!-- 添加更多Tab内容组件 -->
		</view>
		<view class="addImg" @click="boxShow = true">
			<image src="../../static/images/添加.png" mode=""></image>
		</view>
		<view>
			<u-popup :safeAreaInsetBottom="true" :safeAreaInsetTop="true" :mode="popupData.mode" :show="boxShow"
				:round="popupData.round" :overlay="popupData.overlay" :borderRadius="popupData.borderRadius"
				:closeable="popupData.closeable" :closeOnClickOverlay="popupData.closeOnClickOverlay" @close="close"
				@open="open">
				<view class="u-popup-slot">
					<text class="text">添加活动：</text>
					<u-button class="btn" text="志愿服务活动" size="normal" type="success" @click="toAddaction" plain hairline></u-button>
					<u-button class="btn" text="竞赛获奖情况" size="normal" type="warning" @click="toHonor" plain hairline></u-button>
					<u-button type="error" text="取消" customStyle="width: 200rpx" class="cancelAdd btn"
						@click="boxShow = !boxShow"></u-button>

				</view>
			</u-popup>
		</view>
	</view>
</template>
<script>
	import Tab1 from './Tab1.vue';
	import Tab2 from './Tab2.vue'; // 导入你的Tab内容组件

	export default {
		components: {
			Tab1,
			Tab2,
			// ...其他Tab组件
		},
		data() {
			return {
				boxShow: false,
				popupData: {
					overlay: true,
					mode: 'center',
					round: 10,
					closeOnClickOverlay: true
				},
				tabs: [{
						title: '志愿服务活动',
						component: 'Tab1'
					},
					{
						title: '科技竞赛获奖',
						component: 'Tab2'
					},
					// 可以继续添加更多Tab
				],
				currentTabIndex: 0, // 初始激活的Tab索引
			};
		},
		methods: {
			switchTab(index) {
				this.currentTabIndex = index;
			},
			toAddaction() {
				this.boxShow = false;
				uni.navigateTo({
					url: '/pages/memberCommunity/addAction',
				});
			},
			toHonor() {
				this.boxShow = false;
				uni.navigateTo({
					url: '/pages/memberCommunity/competitionHonor',
				});
			},
			open() {
				// console.log('open');
			},
			close() {
				this.boxShow = false
				// console.log('close');
			}
		},
	};
</script>
<style lang="scss" scoped>
	.container {
		flex: 1;
	}

	.tab-bar {
		display: flex;
		justify-content: space-around;
		height: 100rpx;
		line-height: 40px;
		background-color: #f0f0f0;
	}

	.tab-bar view {
		padding: 0 20px;
		color: #666;
		line-height: 100rpx;
	}

	.tab-bar .active {
		color: #000;
		font-size: 40rpx;
		font-weight: 1000;
		position: relative;
		line-height: 80rpx;
		margin: 10rpx 10rpx 20rpx 10rpx;
		display: inline-block;
		/* 确保块级元素也能应用下划线 */
	}

	.tab-bar .active::after {
		content: '';
		/* 伪元素必须有内容 */
		position: absolute;
		bottom: 0;
		/* 下划线位于文字底部 */
		left: 0;
		/* 横跨整个文本 */
		height: 12rpx;
		/* 下划线厚度 */
		opacity: 20%;
		padding: 10rpx 0rpx 5rpx 0rpx;
		margin-left: 100rpx;
		width: 200rpx;
		background-color: red;
		/* 下划线颜色 */
	}

	.content {
		flex: 1;
	}

	.addImg {
		position: fixed;
		bottom: 150rpx;
		right: 130rpx;
	}

	.addImg image {
		width: 150rpx;
		height: 150rpx;
	}

	.underline-text {
		position: relative;
		line-height: 60rpx;
		margin: 20rpx 10rpx 10rpx 10rpx;
		display: inline-block;
		/* 确保块级元素也能应用下划线 */
	}

	/* 弹出框 */
	.u-popup-slot {
		width: 220px;
		height: 180px;
		@include flex;
		justify-content: center;
		align-items: center;
		flex-wrap: wrap;
	}

	.u-popup-slot .btn {
		margin: 22rpx;
		width: 300rpx;
		line-height: 80rpx;
	}
	
	.u-popup-slot .text{
		font-size: 30rpx;
		font-weight: 800;
		line-height: 90rpx;
	}
	.cancelAdd{
		border-radius: 0rpx 0rpx 100rpx 100rpx;
	}
</style>