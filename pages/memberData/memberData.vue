<template>
  <view class="container">
    <!-- 地图 -->
    <!-- <mapdemo></mapdemo> -->
    <view class="dataEntrance">
      <view>
        <u-grid :border="false" align="center" @click="click">
          <u-grid-item v-for="(listItem,listIndex) in list" :key="listIndex"
            customStyle="padding-top: 10px; padding-bottom: 10px">
            <image :src="listItem.url" mode=""></image>
            <text class="grid-text">{{listItem.title}}</text>
          </u-grid-item>
        </u-grid>
      </view>
    </view>
    <view class="adminShow">
      <text>递交入党申请书情况</text>
      <u-tabs :list="tablist" :is-scroll="false" :current="current" bar-width="50" swipeable
        active-color="#30B1B7" @change="change"></u-tabs>
      <view v-if="current == 0">
        <view class="charts-box">
          <qiun-data-charts type="rose" :opts="opts4" :chartData="chartData4" />
        </view>
      </view>
      <view v-if="current == 1">
        <qiun-data-charts type="column" :opts="opts5" :chartData="chartData5" :ontouch="true" />
      </view>
      <view v-if="current == 2">
        <qiun-data-charts type="mix" :opts="opts6" :chartData="chartData6" />
      </view>
      <view v-if="current == 3">
        <qiun-data-charts type="bubble" :opts="opts7" :chartData="chartData7" />
      </view>
      <view v-if="current == 4">
        <qiun-data-charts 
          type="arcbar"
          :opts="opts8"
          :chartData="chartData8"
        />
      </view>
    </view>
    <view class="underline-text">
      <text>发展党员培养教育</text>
    </view>
    <view class="dataEntrance">
      <text>活动参与率</text>
      <view class="charts-box">
        <qiun-data-charts type="line" :opts="opts1" :chartData="chartData1" />
      </view>
    </view>
    <view class="dataEntrance">
      <text>学业分析</text>
      <view class="charts-box">
        <qiun-data-charts type="column" :opts="opts2" :chartData="chartData2" />
      </view>
    </view>
    <view class="dataEntrance">
      <text>风采展示</text>
      <view class="charts-box">
        <qiun-data-charts 
          type="radar" 
          :opts="opts3" 
          :chartData="chartData3" 
          :width="chartWidth + 'px'" 
          :height="chartHeight + 'px'" 
        />
      </view>
    </view>
  </view>
</template>

<script>
  import mapdemo from './mapdemo.vue'
  export default {
    data() {
      return {
        tablist: [
          { name: "按专业" },
          { name: "按年级" },
          { name: "按递交时间" },
          { name: "按性别" },
          { name: "按递交率区间" }
        ],
        current: 0,
        pages: [
          '/pages/memberData/finance',
          '/pages/memberData/thingInternet',
          '/pages/memberData/software',
          '/pages/memberData/telecommunication',
          '/pages/memberData/teachingStaff',
          '/pages/memberData/partyCommittee'
        ],
        list: [
          {
            url: '../../static/images/政府党委.png',
            title: '党委',
          },
          {
            url: '../../static/images/金融.png',
            title: '金融支部',
          },
          {
            url: '../../static/images/物联 网-物联网平台-面.png',
            title: '物联网支部',
          },
          {
            url: '../../static/images/007_软件开发.png',
            title: '软件支部',
          },
          {
            url: '../../static/images/电信.png',
            title: '电信支部',
          },
          {
            url: '../../static/images/部门教工信息.png',
            title: '教工支部',
          },
        ],
        chartData1: {},
        chartData: {},
        opts1: {
          color: ["#1890FF", "#91CB74", "#FAC858", "#EE6666", "#73C0DE", "#3CA272", "#FC8452", "#9A60B4",
            "#ea7ccc"
          ],
          padding: [15, 10, 0, 15],
          enableScroll: false,
          legend: {},
          xAxis: {
            disableGrid: true
          },
          yAxis: {
            gridType: "dash",
            dashLength: 2
          },
          extra: {
            line: {
              type: "curve",
              width: 2,
              activeType: "hollow"
            }
          }
        },
        chartData2: {},
        opts2: {
          color: ["#1890FF", "#91CB74", "#FAC858", "#EE6666", "#73C0DE", "#3CA272", "#FC8452", "#9A60B4",
            "#ea7ccc"
          ],
          padding: [15, 15, 0, 5],
          enableScroll: false,
          legend: {},
          xAxis: {
            disableGrid: true
          },
          yAxis: {
            data: [{
              min: 0
            }]
          },
          extra: {
            column: {
              type: "group",
              width: 30,
              activeBgColor: "#000000",
              activeBgOpacity: 0.08
            }
          }
        },
        chartData3: {},
        opts3: {
          color: ["#1890FF", "#91CB74", "#FAC858", "#EE6666", "#73C0DE", "#3CA272", "#FC8452", "#9A60B4",
            "#ea7ccc"
          ],
          padding: [5, 5, 5, 5],
          dataLabel: false,
          enableScroll: false,
          legend: {
            show: true,
            position: "right",
            lineHeight: 25
          },
          extra: {
            radar: {
              gridType: "circle",
              gridColor: "#CCCCCC",
              gridCount: 3,
              opacity: 0.2,
              max: 200,
              labelShow: true
            }
          }
        },
        chartData4: {},
        opts4: {
          color: ["#1890FF", "#91CB74", "#FAC858", "#EE6666", "#73C0DE", "#3CA272", "#FC8452", "#9A60B4",
            "#ea7ccc"
          ],
          padding: [5, 5, 5, 5],
          enableScroll: false,
          legend: {
            show: true,
            position: "left",
            lineHeight: 25
          },
          extra: {
            rose: {
              type: "radius",
              minRadius: 50,
              activeOpacity: 0.5,
              activeRadius: 10,
              offsetAngle: 0,
              labelWidth: 15,
              border: true,
              borderWidth: 2,
              borderColor: "#FFFFFF",
              linearType: "custom"
            }
          }
        },
        chartData5: {},
        opts5: {
          color: ["#1890FF", "#91CB74", "#FAC858", "#EE6666", "#73C0DE", "#3CA272", "#FC8452", "#9A60B4",
            "#ea7ccc"
          ],
          padding: [15, 15, 0, 5],
          touchMoveLimit: 24,
          enableScroll: true,
          legend: {},
          xAxis: {
            disableGrid: true,
            scrollShow: true,
            itemCount: 4
          },
          yAxis: {
            data: [{
              min: 0
            }]
          },
          extra: {
            column: {
              type: "group",
              width: 30,
              activeBgColor: "#000000",
              activeBgOpacity: 0.08
            }
          }
        },
        chartData6: {},
        opts6: {
          color: ["#1890FF", "#91CB74", "#FAC858", "#EE6666", "#73C0DE", "#3CA272", "#FC8452", "#9A60B4",
            "#ea7ccc"
          ],
          padding: [15, 15, 0, 15],
          enableScroll: false,
          legend: {},
          xAxis: {
            disableGrid: true,
            title: "单位：年"
          },
          yAxis: {
            disabled: false,
            disableGrid: false,
            splitNumber: 5,
            gridType: "dash",
            dashLength: 4,
            gridColor: "#CCCCCC",
            padding: 10,
            showTitle: true,
            data: [{
                position: "left",
                title: "折线"
              },
              {
                position: "right",
                min: 0,
                max: 200,
                title: "柱状图",
                textAlign: "left"
              },
              {
                position: "right",
                min: 0,
                max: 200,
                title: "点",
                textAlign: "left"
              }
            ]
          },
          extra: {
            mix: {
              column: {
                width: 20
              }
            }
          }
        },
        chartData7: {},
        opts7: {
          color: ["#1890FF", "#91CB74", "#FAC858", "#EE6666", "#73C0DE", "#3CA272", "#FC8452", "#9A60B4",
            "#ea7ccc"
          ],
          padding: [15, 15, 0, 15],
          enableScroll: false,
          legend: {},
          xAxis: {
            disableGrid: false,
            gridType: "dash",
            splitNumber: 5,
            boundaryGap: "justify",
            min: 0,
            max: 250
          },
          yAxis: {
            disableGrid: false,
            gridType: "dash",
            data: [{
              min: 0,
              max: 150
            }]
          },
          extra: {
            bubble: {
              border: 2,
              opacity: 0.5
            }
          }
        },
        chartData8: {},
        opts8: {
          color: ["#1890FF","#91CB74","#FAC858","#EE6666","#73C0DE","#3CA272","#FC8452","#9A60B4","#ea7ccc"],
          padding: undefined,
          title: {
            name: "递交率区间",
            fontSize: 35,
            color: "#1890ff"
          },
          subtitle: {
            name: "专业数量",
            fontSize: 15,
            color: "#666666"
          },
          extra: {
            arcbar: {
              type: "circle",
              width: 12,
              backgroundColor: "#E9E9E9",
              startAngle: 1.5,
              endAngle: 0.25,
              gap: 2
            }
          }
        },
        chartWidth: 0,
        chartHeight: 0
      };
    },
    onReady() {
      uni.getSystemInfo({
        success: (res) => {
          this.chartWidth = res.windowWidth - 60;
          this.chartHeight = 300;
        }
      });
      this.getServerData();
    },
    components: {
      mapdemo
    },
    methods: {
      click(count) {
        uni.navigateTo({
          url: `${this.pages[count]}`,
        });
      },
      change(index) {
        this.current = index.index;
      },
      getServerData() {
        setTimeout(() => {
          let res1 = {
            categories: ["第一次党课", "第二次党课", "第三次党课", "主题党日", "志愿活动"],
            series: [
              {
                name: "金融支部",
                data: [83, 90, 92, 88, 95]
              },
              {
                name: "物联网支部",
                data: [80, 82, 85, 83, 88]
              },
              {
                name: "软件支部",
                data: [78, 82, 85, 85, 84]
              },
              {
                name: "电信支部",
                data: [82, 82, 85, 80, 88]
              },
              {
                name: "教工支部",
                data: [80, 82, 87, 80, 88]
              }
            ]
          };
          this.chartData1 = JSON.parse(JSON.stringify(res1));

          let res2 = {
            categories: ["金融", "物联网", "软件工程", "电信"],
            series: [
              {
                name: "平均绩点",
                data: [3.6, 3.4, 3.7, 3.5]
              },
              {
                name: "优秀率",
                data: [0.4, 0.3, 0.45, 0.35]
              }
            ]
          };
          this.chartData2 = JSON.parse(JSON.stringify(res2));

          let res3 = {
            categories: ["理论学习", "组织生活", "志愿服务", "社会实践", "先锋模范作用", "专业技能"],
            series: [
              {
                name: "优秀党员平均水平",
                data: [110, 85, 120, 92, 88, 110]
              },
              {
                name: "积极分子平均水平",
                data: [80, 75, 85, 82, 60, 80]
              }
            ]
          };
          this.chartData3 = JSON.parse(JSON.stringify(res3));

          // Tab 0: 按专业分类（递交人数）
          let res4 = {
            series: [{
              data: [
                { name: "金融", value: 120 },
                { name: "物联网", value: 100 },
                { name: "软件工程", value: 110 },
                { name: "电信", value: 90 }
              ]
            }]
          };
          this.chartData4 = JSON.parse(JSON.stringify(res4));

          // Tab 1: 按年级分类（各年级内不同专业的递交人数）
          let res5 = {
            categories: ["2022级", "2023级", "2024级"],
            series: [
              {
                name: "金融",
                data: [50, 40, 30]
              },
              {
                name: "物联网",
                data: [45, 35, 20]
              },
              {
                name: "软件工程",
                data: [55, 45, 10]
              },
              {
                name: "电信",
                data: [40, 30, 20]
              }
            ]
          };
          this.chartData5 = JSON.parse(JSON.stringify(res5));

          // Tab 2: 按递交时间分类（每年递交人数和递交率）
          let res6 = {
            categories: ["2022", "2023", "2024"],
            series: [
              {
                name: "递交人数",
                type: "line",
                style: "curve",
                data: [150, 130, 100]
              },
              {
                name: "递交率",
                type: "column",
                data: [37.5, 32.5, 25] // 递交率 = 递交人数 / 400 * 100
              }
            ]
          };
          this.chartData6 = JSON.parse(JSON.stringify(res6));

          // Tab 3: 按性别分类（不同性别在各专业的递交人数）
          let res7 = {
            series: [
              {
                name: "男",
                data: [
                  [70, 70, 23, "金融"],
                  [60, 60, 20, "物联网"],
                  [65, 65, 25, "软件工程"],
                  [50, 50, 18, "电信"]
                ]
              },
              {
                name: "女",
                data: [
                  [50, 50, 15, "金融"],
                  [40, 40, 12, "物联网"],
                  [45, 45, 14, "软件工程"],
                  [40, 40, 10, "电信"]
                ]
              }
            ]
          };
          this.chartData7 = JSON.parse(JSON.stringify(res7));

          // Tab 4: 按递交率区间分类（各区间的专业数量）
          let res8 = {
            series: [
              {
                name: "0-30%",
                data: 0.75 // 3个专业，共4个专业，占比3/4
              },
              {
                name: "30-40%",
                data: 0.25 // 1个专业，占比1/4
              },
              {
                name: "40-50%",
                data: 0
              },
              {
                name: "50%以上",
                data: 0
              }
            ]
          };
          this.chartData8 = JSON.parse(JSON.stringify(res8));
        }, 500);
      }
    }
  }
</script>

<style scoped>
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
    margin-left: 30rpx;
    width: 150rpx;
    background-color: red;
  }

  .dataEntrance {
    background-color: white;
    margin: 30rpx 15rpx;
    padding: 20rpx;
    border-radius: 20rpx;
  }

  .dataEntrance image {
    height: 80rpx;
    width: 80rpx;
  }

  .grid-text {
    font-size: 14px;
    color: #909399;
    padding: 10rpx 0 20rpx 0rpx;
    box-sizing: border-box;
  }

  .u-tabs {
    color: black;
  }

  .adminShow {
    margin: 10rpx;
    padding: 20rpx;
    border: 1rpx solid #b8bcc3;
    border-radius: 20rpx;
  }
</style>