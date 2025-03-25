<template>
  <view>
    <view class="">
      <view class="underline-text">服务模块</view>
      <view class="flex-box">
        <view class="partyBox" @click="toYoung">
          <view class="text-container">
            <text class="flex-text">党员旗帜</text>
          </view>
          <image src="../../static/images/员工风采.png" mode=""></image>
        </view>
      </view>
    </view>

    <view class="">
      <view class="branchDeed margin padding">
        <navigator class="topTitle padding">
          <text class="title-text">支部堡垒</text>
          <view class="rightBox">
            <text class="more">查看更多</text>
            <image src="/static/images/zhe.png" alt="" class="rightLabel" />
          </view>
        </navigator>
        <view class="bagList">
          <view class="listMsg" v-for="(article, index) in articles" :key="index" @click="goToArticle(article.url)">
            <view class="image">
              <image :src="article.image" mode="aspectFill"></image>
            </view>
            <view class="viewText">
              <text class="listTitle">{{ article.title }}</text>
              <view class="viewTime">
                <text class="listTime">{{ article.date }}</text>
              </view>
            </view>
          </view>
        </view>
      </view>
    </view>
 <view class="">
      <view class="branchDeed margin padding">
        <navigator class="topTitle padding">
          <text class="title-text">时代前哨</text>
          <view class="rightBox">
            <text class="more">查看更多</text>
            <image src="/static/images/zhe.png" alt="" class="rightLabel" />
          </view>
        </navigator>
        <view class="bagList">
          <view class="listMsg" v-for="(article, index) in timeArticles" :key="index" @click="goToArticle(article.url)">
            <view class="image">
              <image :src="article.image" mode="aspectFill"></image>
            </view>
            <view class="viewText">
              <text class="listTitle">{{ article.title }}</text>
              <view class="viewTime">
                <text class="listTime">{{ article.date }}</text>
              </view>
            </view>
          </view>
        </view>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      // 文章列表数据 (支部堡垒)
      articles: [
        {
          title: '喜报 | 我院学子在第十七届中国研究生电子设计竞赛全国总决赛中荣获佳绩',
          image: '../../static/testimg/t1.jpg',
          url: 'https://mp.weixin.qq.com/s/otmWFuV1aI2xe98xAu4lRg',
          date: '2023-08-28'
        },
        {
          title: '我院举行2023年秋季学期家庭经济困难学生慰问座谈会',
          image: '../../static/testimg/t2.jpg',
          url: 'https://mp.weixin.qq.com/s/GVqRjDC-rOF7lxmDF7hHDw',
          date: '2023-09-15'
        },
        {
          title: '我院学子在2023年“TI杯”全国大学生电子设计竞赛中荣获佳绩',
          image: '../../static/testimg/t3.jpg',
          url: 'https://mp.weixin.qq.com/s/UJs68isjooL15A3fNyMp6g',
          date: '2023-09-05'
        },
        {
          title: '青春筑梦，扬帆起航 | 我院2023级研究生开学典礼暨入学教育顺利举行',
          image: '../../static/testimg/t4.jpg',
          url: 'https://mp.weixin.qq.com/s/W5DPZoklo-EJIMMG37EPDg',
          date: '2023-09-01'
        }
      ]
    ,
    timeArticles:[
        {
          title: '喜报 | 我院学子在第十七届中国研究生电子设计竞赛全国总决赛中荣获佳绩',
          image: '../../static/testimg/t1.jpg', // 替换为实际图片路径
          url: 'https://mp.weixin.qq.com/s/otmWFuV1aI2xe98xAu4lRg',
          date: '2023-08-28'
        },
        {
          title: '我院举行2023年秋季学期家庭经济困难学生慰问座谈会',
          image: '../../static/testimg/t2.jpg', // 替换为实际图片路径
          url: 'https://mp.weixin.qq.com/s/GVqRjDC-rOF7lxmDF7hHDw',
          date: '2023-09-15'
        },
        {
          title: '我院学子在2023年“TI杯”全国大学生电子设计竞赛中荣获佳绩',
          image: '../../static/testimg/t3.jpg', // 替换为实际图片路径
          url: 'https://mp.weixin.qq.com/s/UJs68isjooL15A3fNyMp6g',
          date: '2023-09-05'
        },
        {
          title: '青春筑梦，扬帆起航 | 我院2023级研究生开学典礼暨入学教育顺利举行',
          image: '../../static/testimg/t4.jpg', // 替换为实际图片路径
          url: 'https://mp.weixin.qq.com/s/W5DPZoklo-EJIMMG37EPDg',
          date: '2023-09-01'
        }
      ]
    };
  },
  methods: {
    toYoung() {
      uni.navigateTo({
        url: '/pages/memberCommunity/young', //党员旗帜页面
      });
    },
    goToArticle(url) {
      uni.navigateTo({
        url: `/pages/memberCommunity/webview?url=${encodeURIComponent(url)}`,
      });
    }
  }
};
</script>

<style scoped>
.underline-text {
  position: relative;
  line-height: 60rpx;
  margin: 20rpx 10rpx 10rpx 10rpx;
  display: inline-block;
}

/* 使用伪元素添加下划线 */
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

.rightBox {
  float: right;
}

.branchDeed .more {
  font-size: 26rpx;
}

.branchDeed .title-text {
  font-size: 32rpx;
  font-weight: 1000;
}

.branchDeed .rightLabel {
  vertical-align: middle;
  width: 26rpx;
  height: 26rpx;
  margin: 0;
}

.branchDeed .more {
  font-size: 28rpx;
  margin-right: 2rpx;
  color: #E2E2E2;
}

.margin {
  margin: 70rpx 30rpx;
}

.padding {
  padding: 15rpx 20rpx;
}

.branchDeed {
  background-color: white;
  border-radius: 15rpx;
}

.branchDeed .listMsg {
  line-height: 200rpx;
  border-bottom: 1rpx solid #f3f3f3;
}

.branchDeed .listMsg {
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
  overflow: hidden;
}

.listMsg .viewTime {
  font-size: 24rpx;
  color: #cbcbcb;
  position: relative;
  left: 220rpx;
  bottom: 70rpx;
}
</style>