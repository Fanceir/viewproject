<template>
  <div class="dashboard-container">
    <h1>Dashboard</h1>
    <div class="chart" ref="chart1"></div>
    <div class="chart" ref="chart2"></div>
  </div>

</template>

<script>
// 引入 Echarts 库
import * as echarts from "echarts";

export default {
  name: 'Dashboard',
  data() {
    return {
      // 存储图表实例
      charts: [],
      // 自定义数据
      customData: {
        chart1: [30, 40, 50, 60, 70],
        chart2: [70, 60, 90, 40, 45],
        // 其他图表数据...
      }
    };
  },
  mounted() {
    // 在组件挂载完成后渲染图表
    this.renderCharts();
  },
  methods: {
    renderCharts() {
      // 获取图表容器元素
      const chart1 = this.$refs.chart1;
      const chart2 = this.$refs.chart2;
      // 其他图表容器...

      // 使用 Echarts 初始化图表实例
      const myChart1 = echarts.init(chart1);
      const myChart2 = echarts.init(chart2);
      // 其他图表实例...

      // 配置图表数据
      myChart1.setOption({
        title: {
          text: '注册人数'
        },
        xAxis: {
          type: 'category',
          data: ['大一', '大二', '大三', '大四', '教师']
        },
        yAxis: {
          type: 'value'
        },
        series: [{
          data: this.customData.chart1,
          type: 'bar'
        }]
      });

      myChart2.setOption({
        title: {
          text: '任务完成数量'
        },
        xAxis: {
          type: 'category',
          data: ['任务1', '任务2', '任务3', '任务4', '任务5']
        },
        yAxis: {
          type: 'value'
        },
        series: [{
          data: this.customData.chart2,
          type: 'line'
        }]
      });

      // 存储图表实例
      this.charts.push(myChart1, myChart2);
      // 其他图表实例...
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
  width: 50%;
  height: 400px;
}
</style>
