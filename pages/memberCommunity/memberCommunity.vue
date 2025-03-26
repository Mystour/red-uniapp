<template>
  <view>
    <!-- 服务模块区域现在为空，如果你不需要这个标题也可以删掉 -->
    <!-- <view class="">
      <view class="underline-text">服务模块</view>
      <view class="flex-box">
         这里原来是党员旗帜的入口，已移除
      </view>
    </view> -->

    <!-- 支部堡垒 Section -->
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
          <!-- 支部堡垒文章列表 -->
          <view class="listMsg" v-for="(article, index) in fortressArticles" :key="'fortress-'+index" @click="goToArticle(article.url)">
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

    <!-- 党员旗帜 Section (原 时代前哨) -->
    <view class="">
      <view class="branchDeed margin padding">
        <navigator class="topTitle padding">
          <!-- 标题已修改 -->
          <text class="title-text">党员旗帜</text>
          <view class="rightBox">
            <text class="more">查看更多</text>
            <image src="/static/images/zhe.png" alt="" class="rightLabel" />
          </view>
        </navigator>
        <view class="bagList">
          <!-- 党员旗帜文章列表 -->
          <view class="listMsg" v-for="(article, index) in flagArticles" :key="'flag-'+index" @click="goToArticle(article.url)">
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
      // 支部堡垒文章列表数据
      fortressArticles: [
        {
          title: '就业辅导|都柏林学院学生党支部开展“我为群众办实事”主题党日活动',
          image: '../../static/images/fortress1.png', // 请替换为实际图片
          url: 'https://mp.weixin.qq.com/s/HSVSKkHoUnJiLWe0kW_sZg',
          date: '2023-06-04' // 示例日期，请按需修改
        },
        {
          title: '北京-都柏林国际学院党委开展院级党课 助力师生党员跨文化交际能力提升',
          image: '../../static/images/fortress2.png', // 请替换为实际图片
          url: 'https://mp.weixin.qq.com/s/W5DPZoklo-EJIMMG37EPDg',
          date: '2023-06-26' // 示例日期，请按需修改
        },
        {
          title: '英文宣讲团|都柏林学院开展学习贯彻习近平新时代中国特色社会主义思想主题教育',
          image: '../../static/images/fortress3.png', // 请替换为实际图片
          url: 'https://mp.weixin.qq.com/s/vRi7xqe-uyo90e7FqG-4bw',
          date: '2023-04-22' // 示例日期，请按需修改
        },
         {
          title: '党课丨做信念坚定、作风过硬的新时代合格党员',
          image: '../../static/images/fortress4.png', // 请替换为实际图片
          url: 'https://mp.weixin.qq.com/s/WVgE79BWsBCKdPg2i2L0jw',
          date: '2023-06-01' // 示例日期，请按需修改
        }
      ],
      // 党员旗帜文章列表数据
      flagArticles:[
        {
          title: '青衿之志，履践致远——信息类专业国家奖学金获得者专访',
          image: '../../static/images/flag1.png', // 请替换为实际图片
          url: 'https://mp.weixin.qq.com/s/7JQpYfC4BtWReR47gSe1fw',
          date: '2025-01-16' // 示例日期，请按需修改
        },
        {
          title: '遇见更好的自己——金融学专业国家奖学金获得者专访',
          image: '../../static/images/flag2.png', // 请替换为实际图片
          url: 'https://mp.weixin.qq.com/s/ZnCixe3ptJFBwa5LOK9UTQ',
          date: '2025-01-17' // 示例日期，请按需修改
        },
        {
          title: 'BDIC体育之星谭亦菲：疾速坚持 梦想荣耀',
          image: '../../static/images/flag3.png', // 请替换为实际图片
          url: 'https://mp.weixin.qq.com/s/CRjdvmp5PCmKUIE19uBU4Q',
          date: '2024-05-27' // 示例日期，请按需修改
        }
      ]
    };
  },
  methods: {
    // toYoung 方法已移除
    goToArticle(url) {
      uni.navigateTo({
        url: `/pages/memberCommunity/webview?url=${encodeURIComponent(url)}`,
      });
    }
  }
};
</script>

<style scoped>
/* 样式部分保持不变 */
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