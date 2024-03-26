<template>
	<div class="dashboard-container">
		<h1>Dashboard</h1>
		<div ref="chart1" class="chart" />
		<div ref="chart2" class="chart" />
		<div ref="chart3" class="chart" />
		<div ref="chart4" class="chart" />
	</div>
</template>

<script>
import * as echarts from 'echarts'
export default {
	/*eslint-disable*/
	// eslint-disable-next-line
	name: "Dashboard",
	data() {
		return {
			// 存储图表实例
			charts: [],
			// 自定义数据
			customData: {
				chart1: [30, 40, 50, 60, 70],
				chart2: [70, 60, 90, 40, 45],
				chart3: [
					{ value: 23, name: "大一" },
					{ value: 24, name: "大二" },
					{ value: 18, name: "大三" },
					{ value: 25, name: "大四" }
				],
				chart4: [23, 24, 18, 25, 27, 28, 25]
				// 其他图表数据...
			}
		};
	},
	mounted() {
		//颜色选项
		let colors = ['#5470c6', '#91cc75', '#fac858', '#ee6666', '#73c0de', '#3ba272']
		// 在组件挂载完成后渲染图表
		this.renderCharts();
		// 监听窗口大小变化，重新渲染图表
		window.addEventListener("resize", this.handleResize);
		// 设置定时器，每隔两秒更新数据
		setInterval(() => {
			this.updateChartData();
		}, 2000);
	},
	beforeDestroy() {
		// 在组件销毁前移除窗口大小变化监听器
		window.removeEventListener("resize", this.handleResize);
	},
	methods: {
		renderCharts() {
			// 获取图表容器元素
			const chart1 = this.$refs.chart1;
			const chart2 = this.$refs.chart2;
			const chart3 = this.$refs.chart3;
			const chart4 = this.$refs.chart4;
			// 使用 Echarts 初始化图表实例
			const myChart1 = echarts.init(chart1);
			const myChart2 = echarts.init(chart2);
			const myChart3 = echarts.init(chart3);
			const myChart4 = echarts.init(chart4);
			// 配置图表数据...
			myChart1.setOption({
				// 表名
				title: { text: "注册人数" },
				// 横轴
				xAxis: {
					type: "category",
					data: ["大一", "大二", "大三", "大四", "教师"],
				},
				// 纵轴
				yAxis: {
					type: "value",
				},
				// 数据来源、图表类型
				series: [
					{
						data: this.customData.chart1,
						type: "bar",
					},]
			});
			// 其他图表配置
			//折线图
			myChart2.setOption({
				title: {
					text: '任务完成数量',
				},
				xAxis: {
					type: 'category',
					data: ['任务1', '任务2', '任务3', '任务4', '任务5'],
				},
				yAxis: {
					type: 'value',
				},
				series: [{
					data: this.customData.chart2,
					type: 'line',
					//颜色设置
					color: ['#00aa00', '#F44042']
					//itemStyle : {normal : {color:'#409EFF'}, //改变折线点的颜色
					//lineStyle:{color:'#00aa00'}}//改变折线颜色
				}],
			});
			//饼图
			myChart3.setOption({
				//图例位置属性设置
				legend: {
					right: "10%",
					top: "30%",
					orient: "vertical"
				},
				title: {
					text: '各年级占比',
					top: "0%",
					//设置标题居中
					left: "center"
				},
				series: [{
					//自己设定的数据
					data: this.customData.chart3,
					//随机生成数据
					//data:makeRandomData(),
					type: 'pie',
					//图例
					label: {
						show: true,
						//设置图例的表示形式
						formatter: "{b}:{c}({d}%)"
					},
					//饼图的大小
					radius: "80%",
				}]
			});
			//散点图
			myChart4.setOption({
				title: {
					text: '各天在线人数(周次)'
				},
				xAxis: {
					type: 'category',
					data: ['周一', '周二', '周三', '周四', '周五', '周六', '周日']
				},
				yAxis: {
					type: 'value'
				},
				series: [{
					data: this.customData.chart4,
					type: 'scatter',
					color: '#409EFF'
				}]
			});
			//添加数据缩放和工具栏功能
			myChart1.setOption({
				dataZoom: [
					{
						type: 'slider', // 缩放类型为滑动条
						start: 0, // 起始位置百分比
						end: 100 // 结束位置百分比
					},
					{
						type: 'inside' // 内部缩放
					}
				],
				toolbox: {
					feature: {
						dataView: { readOnly: false }, // 数据视图，用户可以查看数据
						saveAsImage: {} // 导出图片
					}
				},
				tooltip: {
					trigger: 'axis' // 鼠标悬停提示
				}
			});

			myChart2.setOption({
				dataZoom: [
					{
						type: 'slider', // 缩放类型为滑动条
						start: 0, // 起始位置百分比
						end: 100 // 结束位置百分比
					},
					{
						type: 'inside' // 内部缩放
					}
				],
				toolbox: {
					feature: {
						dataView: { readOnly: false }, // 数据视图，用户可以查看数据
						saveAsImage: {} // 导出图片
					}
				},
				tooltip: {
					trigger: 'axis' // 鼠标悬停提示
				}
			});

			myChart4.setOption({
				dataZoom: [
					{
						type: 'slider', // 缩放类型为滑动条
						start: 0, // 起始位置百分比
						end: 100 // 结束位置百分比
					},
					{
						type: 'inside' // 内部缩放
					}
				],
				toolbox: {
					feature: {
						dataView: { readOnly: false }, // 数据视图，用户可以查看数据
						saveAsImage: {} // 导出图片
					}
				},
				tooltip: {
					trigger: 'axis' // 鼠标悬停提示
				}
			});
			// 存储图表实例
			this.charts.push(myChart1, myChart2);
			this.charts.push(myChart3, myChart4);
			// 其他图表实例...
		},
		updateChartData() {
			// 随机生成不同类型的新数据并更新图表
			this.charts.forEach((chart, index) => {
				let newData;
				switch (index) {
					case 0:
						newData = this.makeRandomData('myChart1');
						break;
					case 1:
						newData = this.makeRandomData('myChart2');
						break;
					case 2:
						newData = this.makeRandomData('myChart3');
						break;
					case 3:
						newData = this.makeRandomData('myChart4');
						break;
					default:
						newData = this.makeRandomData('default');
				}
				chart.setOption({
					series: [{ data: newData }]
				});
			});
		},
		makeRandomData(chartType) {
			switch (chartType) {
				case 'myChart1':
					return [
						{ value: Math.floor(Math.random() * 10000) },
						{ value: Math.floor(Math.random() * 10000) },
						{ value: Math.floor(Math.random() * 10000) },
						{ value: Math.floor(Math.random() * 10000) },
						{ value: Math.floor(Math.random() * 10000) }
					];
				case 'myChart2':
					return [
						{ value: Math.floor(Math.random() * 10000) },
						{ value: Math.floor(Math.random() * 10000) },
						{ value: Math.floor(Math.random() * 10000) },
						{ value: Math.floor(Math.random() * 10000) },
						{ value: Math.floor(Math.random() * 10000) }
					];
				case 'myChart3':
					return [
						{ value: Math.floor(Math.random() * 10000), name: "大一" },
						{ value: Math.floor(Math.random() * 10000), name: "大二" },
						{ value: Math.floor(Math.random() * 10000), name: "大三" },
						{ value: Math.floor(Math.random() * 10000), name: "大四" }
					];
				case 'myChart4':
					return [
						{ value: Math.floor(Math.random() * 10000) },
						{ value: Math.floor(Math.random() * 10000) },
						{ value: Math.floor(Math.random() * 10000) },
						{ value: Math.floor(Math.random() * 10000) },
						{ value: Math.floor(Math.random() * 10000) },
						{ value: Math.floor(Math.random() * 10000) },
						{ value: Math.floor(Math.random() * 10000) }
					];
				default:
					return [];
			}
		},
		handleResize() {
			// 窗口大小变化时重新渲染图表
			this.charts.forEach(chart => {
				chart.resize();
			});
		}
	}
};
</script>

<style scoped>
.dashboard {
	display: flex;
	flex-wrap: wrap;
}

.chart {
	float: left;
	width: 100%;
	height: 400px;
}
</style>
