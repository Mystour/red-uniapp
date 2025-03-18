<template>
	<view class="container">
		<view class="charts-box">
			<text class="">年度收支分析</text>
			<qiun-data-charts type="area" :opts="opts" :chartData="chartData" />
		</view>
		<view class="charts-box">
			<text class="">学生贷款发放与还款情况</text>
		<qiun-data-charts 
		      type="radar"
		      :opts="opts"
		      :chartData="chartData"
		    />
		</view>
		<view class="charts-box">
			<text class="">奖学金发放统计</text>
			<qiun-data-charts 
			      type="column"
			      :opts="opts"
			      :chartData="chartData"
			      :ontouch="true"
			    />
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				chartData: {},
				//您可以通过修改 config-ucharts.js 文件中下标为 ['area'] 的节点来配置全局默认参数，如都是默认参数，此处可以不传 opts 。实际应用过程中 opts 只需传入与全局默认参数中不一致的【某一个属性】即可实现同类型的图表显示不同的样式，达到页面简洁的需求。
				opts: {
					color: ["#1890FF", "#91CB74", "#FAC858", "#EE6666", "#73C0DE", "#3CA272", "#FC8452", "#9A60B4",
						"#ea7ccc"
					],
					padding: [15, 15, 0, 15],
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
						area: {
							type: "curve",
							opacity: 0.2,
							addLine: true,
							width: 2,
							gradient: true,
							activeType: "hollow"
						}
					}
				}
			};
		},
		onReady() {
			this.getServerData();
		},
		methods: {
			getServerData() {
				//模拟从服务器获取数据时的延时
				setTimeout(() => {
					//模拟服务器返回数据，如果数据格式和标准格式不同，需自行按下面的格式拼接
					let res = {
						categories: ["2018", "2019", "2020", "2021", "2022", "2023"],
						series: [{
								name: "成交量A",
								data: [35, 8, 25, 37, 4, 20]
							},
							{
								name: "成交量B",
								data: [70, 40, 65, 100, 44, 68]
							},
							{
								name: "成交量C",
								data: [100, 80, 95, 150, 112, 132]
							}
						]
					};
					this.chartData = JSON.parse(JSON.stringify(res));
				}, 500);
			},
		}
	};
</script>

<style scoped>
	page {
		box-sizing: border-box;
	}

	.container {
		display: flex;
		justify-content: center;
		align-items: center;
		flex-wrap: wrap;
	}

	/* 请根据实际需求修改父元素尺寸，组件自动识别宽高 */
	.charts-box {
		width: 700rpx;
		/* height: 200px; */
		border-radius: 10rpx;
		padding: 10rpx 30rpx;
		margin: 30rpx 20rpx;
		background-color: white;
	}

	.charts-box text {
		font-weight: 700;
		line-height: 80rpx;
		border-bottom: 4rpx solid #eaea00;
	}
</style>