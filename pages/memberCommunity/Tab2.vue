<template>
  <view class="container">
    <view class="category-title">创新创业类</view>
    <view class="card-container">
      <view class="card" v-for="(item, index) in innovationContests" :key="index">
        <text class="contest-name">{{ item.name }}</text>
        <text class="details">{{ item.details }}</text>
      </view>
    </view>

    <view class="category-title">学术研究类</view>
    <view class="card-container">
      <view class="card" v-for="(item, index) in academicResearch" :key="index">
        <text class="contest-name">{{ item.name }}</text>
        <text class="details">{{ item.details }}</text>
      </view>
    </view>

    <view class="category-title">应用技能类</view>
    <view class="card-container">
      <view class="card" v-for="(item, index) in applicationSkills" :key="index">
        <text class="contest-name">{{ item.name }}</text>
        <text class="details">{{ item.details }}</text>
      </view>
    </view>
    <!-- 重复以上结构，分别为应用技能类、教育普及类、综合能力类 -->

  </view>
</template>

<script>
export default {
  data() {
    return {
      innovationContests: [
        { name: "‘互联网+’大学生创新创业大赛", details: "2023年一等奖" },
        { name: "商业计划竞赛", details: "2022年二等奖" },
      ],
      academicResearch: [
        { name: "全国大学生课外学术科技作品竞赛", details: "多次获奖" },
        { name: "‘挑战杯’系列竞赛", details: "连续三年优秀奖" },
      ],
      applicationSkills: [
        { name: "CAD设计竞赛", details: "多次获奖" },
        { name: "软件开发竞赛", details: "连续三年优秀奖" },
      ],
      // 应用技能类、教育普及类、综合能力类数据结构类似，根据实际竞赛补充
    };
  },
};
</script>

<style>
.container {
  padding: 20rpx;
}

.category-title {
  font-size: 28rpx;
  font-weight: bold;
  margin-bottom: 20rpx;
}

.card-container {
  display: flex;
  flex-wrap: wrap;
  /* justify-content: space-between; */
}

.card {
  background-color: #ffffff;
  border-radius: 10rpx;
  box-shadow: 0 2rpx 4rpx rgba(0, 0, 0, 0.1);
  padding: 20rpx;
  margin-bottom: 20rpx;
  width: 90%; /* 调整宽度以适应不同屏幕和布局需求 */
}

.contest-name {
  font-size: 26rpx;
  margin-bottom: 10rpx;
}

.details {
  color: #d81919;
  display: block;
  position: relative;
  left: 400rpx;
  line-height: 50rpx;
}
</style>