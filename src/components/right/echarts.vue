<template>
  <div class="m-">
    <div id="myChart" ref="myEchart" :style="{width: '500px', height: '400px', background:'#eee'}"></div>
  </div>
</template>
<script>
import echarts from "../../../node_modules/echarts/dist/echarts";

export default {
  data() {
    return {
      data: [
        {
          _id: "2020-05-17",
          date: "2020-05-17",
          cpu_used_avg: 49,
          cpu_used_max: 100,
          memory_used_avg: 24
        },
        {
          _id: "2020-05-13",
          date: "2020-05-13",
          cpu_used_avg: 49,
          cpu_used_max: 100,
          memory_used_avg: 24
        },
        {
          _id: "2020-05-14",
          date: "2020-05-14",
          cpu_used_avg: 49,
          cpu_used_max: 100,
          memory_used_avg: 24
        },
        {
          _id: "2020-05-15",
          date: "2020-05-15",
          cpu_used_avg: 49,
          cpu_used_max: 100,
          memory_used_avg: 24
        },
        {
          _id: "2020-05-18",
          date: "2020-05-18",
          cpu_used_avg: 49,
          cpu_used_max: 100,
          memory_used_avg: 24
        }
      ]
    };
  },
  mounted() {
    this.drawLine(this.data);
  },
  methods: {
    drawLine(data) {
      const lArr = [];
      let tArr = [];
      const bArr = [];
      let cpuArr = [];
      let memavgArr = [];
      let memmaxArr = [];
      tArr = data;
      const dateToTime = str => new Date(str).getTime();
      data.forEach((item, i) => {
        tArr[i].publishTimeNew = dateToTime(data[i].publishTime);
      });
      data.sort((a, b) => (b.publishTimeNew > a.publishTimeNew ? 1 : -1));
      data.forEach(item => {
        lArr.push(item.cpu_used_avg);
        cpuArr.push(item.cpu_used_max);
        bArr.push(item.date);
      });
      this.leftList = lArr;
      this.cpuLift = cpuArr;
      this.bottomList = bArr;
      this.setInit(this.leftList, this.bottomList, this.cpuLift);
    },
    setInit(l, b, c) {
      this.chart = echarts.init(this.$refs.myEchart);
      var colors = ["#2D8CF0", "#FBA900"];
      const option = {
        color: colors,
        title: {
          text: "echarts"
          //   left: "center"
        },
        formatter:
          "{b0}<br/>" +
          '<span style="display:inline-block;margin-right:5px;border-radius:10px;width:9px;height:9px;background-color:#FBA900"></span>{a1}:{c1}%<br/>' +
          '<span style="display:inline-block;margin-right:5px;border-radius:10px;width:9px;height:9px;background-color:#2D8CF0"></span>{a0}:{c0}%<br/>',
        tooltip: {
          trigger: "axis",
          textStyle: {
            align: "left"
          }
        },
        legend: {
          data: ["邮件营销", "联盟广告", "视频广告", "直接访问", "搜索引擎"]
        },
        // tooltip: {
        //   trigger: "axis",
        //   axisPointer: {
        //     // 坐标轴指示器，坐标轴触发有效
        //     type: "line" // 默认为直线，可选为：'line' | 'shadow'
        //   }
        // },
        grid: {
          left: "-1%",
          right: "0%",
          bottom: "3%",
          containLabel: true,
          borderWidth: 0 // 去除白色边框
        },
        xAxis: [
          {
            type: "category",
            data: b,
            axisTick: {
              show: false
            },
            axisLine: {
              show: false
            },
            splitLine: {
              show: false
            }, // 去除网格线
            splitArea: {
              show: false
            } // 去除网格背景颜色
          }
        ],
        yAxis: [
          {
            type: "value",
            splitLine: {
              show: true // 去除网格线
            },
            splitArea: {
              show: false // 去除网格背景颜色
            }
          }
        ],
        series: [
          {
            name: "平均值",
            type: "line",
            barWidth: "100%",
            data: l
          },
          {
            name: "峰值",
            type: "line",
            barWidth: "100%",
            data: c,
            itemStyle: {
              normal: {
                lineStyle: {
                  color: "#FBA900"
                }
              }
            }
          }
        ]
      };
      this.chart.setOption(option);
    }
  }
};
</script>
<style scoped>
.m- {
}
</style>