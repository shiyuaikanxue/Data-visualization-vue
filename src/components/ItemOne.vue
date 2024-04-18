<template>
  <div class="itemOne">
    <h2>图表1</h2>
    <div class="chart" id="oneChart"></div>
  </div>
</template>

<script>
import { inject, onMounted, reactive } from "vue";
export default {
  setup() {
    const echarts = inject("echarts");
    const axios = inject("axios");
    let xdata = reactive([]);
    let ydata = reactive([]);
    async function getData() {
      const res = await axios({ url: "/one/data" });
      xdata = res.data.chartData.chartData.map((item) => {
        return item.title;
      });
      ydata = res.data.chartData.chartData.map((item) => item.num);
      console.log(xdata);
      console.log(ydata);
    }
    onMounted(() => {
      const myChart = echarts.init(document.getElementById("oneChart"));
      getData().then(() => {
        myChart.setOption({
          xAxis: {
            type: "value",
            axisLine: {
              lineStyle: {
                color: "white",
              },
            },
            axisLabel: {
              color: "white",
            },
          },
          yAxis: {
            type: "category",
            data: xdata,
            axisLabel: {
              color: "white",
            },
            axisLine: {
              lineStyle: {
                color: "white",
              },
            },
          },
          grid: {
            top: "3%",
            left: "1%",
            right: "6%",
            bottom: "3%",
            containLabel: true,
          },
          series: [
            {
              type: "bar",
              data: ydata,
              itemStyle: {
                normal: {
                  barBorderRadius: [0, 20, 20, 0],
                  color: new echarts.graphic.LinearGradient(0, 0, 1, 0, [
                    {
                      offset: 0,
                      color: "#534587",
                    },
                    {
                      offset: 0.5,
                      color: "#978654",
                    },
                    {
                      offset: 1,
                      color: "#5a46ed",
                    },
                  ]),
                },
              },
            },
          ],
        });
      });
    });
    return {
      getData,
      xdata,
      ydata,
    };
  },
};
</script>

<style scoped>
.chart {
  height: 4.5rem;
}
h2 {
  height: 0.4rem;
  color: white;
  line-height: 0.4rem;
  font-size: 0.25rem;
  text-align: center;
}
</style>
