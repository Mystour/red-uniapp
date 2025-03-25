<template>
  <view>
    <view class="underline-text">服务模块</view>
    <view class="flex-box">
      <view class="partyBox" @click="toWall">
        <view class="text-container">
          <text class="flex-text">红色云墙</text>
        </view>
        <image src="../../static/images/医院风采.png" mode=""></image>
      </view>
      <view class="partyBox" @click="toHelp">
        <view class="text-container">
          <text class="flex-text">有求必应</text>
        </view>
        <image src="../../static/images/帮助中心.png" mode=""></image>
      </view>
      <view class="partyBox" @click="toSuggestion">
        <view class="text-container">
          <text class="flex-text">发展共治</text>
        </view>
        <image src="../../static/images/投诉建议.png" mode=""></image>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  methods: {
    toHelp() {
      uni.navigateTo({
        url: '/pages/memberCommunity/help',
      });
    },
    toSuggestion() {
      uni.navigateTo({
        url: '/pages/memberCommunity/suggestion',
      });
    },
    toWall() {
      uni.navigateTo({
        url: '/pages/memberCommunity/memberWall',
      });
    },
  }
};
</script>

<style scoped>
/* 样式与 memberCommunity.vue 中的 flex-box 和 partyBox 相同 */
.underline-text {
  position: relative;
  line-height: 60rpx;
  margin: 20rpx 10rpx 10rpx 10rpx;
  display: inline-block;
}

.underline-text::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 13rpx;
  opacity: 25%;
  padding: 10rpx 0rpx 5rpx 0rpx;
  margin-left: 20rpx;
  width: 150rpx;
  background-color: red;
}

.flex-box {
  margin: 30rpx 0rpx;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.partyBox {
  border-radius: 10rpx;
  width: 330rpx;
  height: 180rpx;
  background-color: #fff;
  padding: 15rpx 10rpx;
  margin: 10rpx;
  display: flex;
  align-items: center;
}

.partyBox .text-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
  margin-left: 20rpx;
  width: 150rpx;
}

.partyBox image {
  width: 100rpx;
  height: 100rpx;
  position: relative;
  margin-left: auto;
  margin-right: 30rpx;
}

.flex-text {
  font-size: 26rpx;
}
</style>