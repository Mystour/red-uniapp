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
  margin: 30rpx 15rpx; /* 给容器加左右边距 */
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between; /* 让前两个元素靠两边 */
}

.partyBox {
  border-radius: 10rpx;
  width: calc(50% - 15rpx); /* 计算宽度，占满一半减去间距 */
  height: 180rpx;
  background-color: #fff;
  padding: 15rpx 10rpx;
  margin-bottom: 30rpx; /* 只保留下边距 */
  display: flex;
  align-items: center;
  box-sizing: border-box; /* 让 padding 和 border 包含在宽度内 */
}

/* 单独设置第三个元素的样式 */
.partyBox:nth-child(3) {
  width: 100%; /* 第三个元素占满整行 */
  margin-left: 0;
  margin-right: 0;
  /* 修改这里：让内部元素水平分布，而不是默认的居中 */
  justify-content: flex-start; /* 或者 space-around / space-between，根据想要的效果调整 */
   padding-left: 200rpx; /* 可以添加一些左内边距让它不那么靠左 */
   padding-right: 50rpx; /* 可以添加一些右内边距 */
}

.partyBox .text-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start; /* 默认文字左对齐 */
  margin-left: 20rpx;
  /* width: 150rpx; */ /* 不固定宽度，让其自适应 */
   flex: 1; /* 让文本容器占据更多空间 */
}

/* 单独设置第三个元素内部文本容器的样式 */
.partyBox:nth-child(3) .text-container {
   align-items: flex-start; /* 确保第三个的文字也是左对齐 */
   margin-left: 20rpx; /* 保持或调整左边距 */
   flex: none; /* 取消flex:1, 避免过度拉伸 */
   width: auto; /* 或者设置一个合适的宽度，例如 150rpx */
}


.partyBox image {
  width: 100rpx;
  height: 100rpx;
  /* position: relative; */ /* 移除相对定位 */
  margin-left: auto; /* 图片自动靠右 */
  margin-right: 30rpx;
  flex-shrink: 0; /* 防止图片被压缩 */
}

/* 单独设置第三个元素内部图片的样式 */
.partyBox:nth-child(3) image {
    margin-left: auto; /* 保持图片靠右 */
    margin-right: 30rpx; /* 保持右边距 */
}


.flex-text {
  font-size: 35rpx;
}

</style>