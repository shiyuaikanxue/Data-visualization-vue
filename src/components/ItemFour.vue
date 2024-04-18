<template>
  <div class="itemFour">
    <h2>产品类别</h2>
    <div class="chart" id="fourChart"></div>
  </div>
</template>

<script>
import { inject, onMounted, reactive } from "vue";
export default {
  setup() {
    const echarts = inject("echarts");
    const axios = inject("axios");
    let data = reactive({});
    async function getState() {
      data = await axios({
        url: "/four/data",
      });
    }
    onMounted(() => {
      getState().then(() => {
        console.log(data);
        const myChart = echarts.init(document.getElementById("fourChart"));
        myChart.setOption({
          tooltip: {
            trigger: "axis",
            axisPointer: {
              type: "shadow",
            },
          },
          legend: {},
          xAxis: {
            type: "category",
            data: data.data.chartData.chartData.day,
            axisLine: {
              lineStyle: {
                color: "white",
              },
            },
          },
          yAxis: {
            type: "value",
            axisLine: {
              lineStyle: {
                color: "white",
              },
            },
          },
          grid:{
            left:'3%',
            right:'4%',
            bottom:'3%',
            containLabel:true
          },
          series: [
            {
              name: "服饰",
              type: "bar",
              data: data.data.chartData.chartData.num.Chemicals,
              stack: "total",
              label: {
                show: true,
              },
              emphasis: {
                fucus: "series",
              },
            },
            {
              name: "数码",
              type: "bar",
              data: data.data.chartData.chartData.num.Clothes,
              stack: "total",
              label: {
                show: true,
              },
              emphasis: {
                fucus: "series",
              },
            },
            {
              name: "家电",
              type: "bar",
              data: data.data.chartData.chartData.num.Electrical,
              stack: "total",
              label: {
                show: true,
              },
              emphasis: {
                fucus: "series",
              },
            },
            {
              name: "家具",
              type: "bar",
              data: data.data.chartData.chartData.num.digit,
              stack: "total",
              label: {
                show: true,
              },
              emphasis: {
                fucus: "series",
              },
            },
            {
              name: "日化",
              type: "bar",
              data: data.data.chartData.chartData.num.gear,
              stack: "total",
              label: {
                show: true,
              },
              emphasis: {
                fucus: "series",
              },
            },
          ],
        });
      });
    });
    return {
      getState,
      data,
    };
  },
};
</script>

<style>
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
