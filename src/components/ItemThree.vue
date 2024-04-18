<template>
  <div class="itemThree">
    <h2>库存统计</h2>
    <div class="chart" id="charts"></div>
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
        url: "/three/data",
      });
    }
    onMounted(() => {
      getState().then(() => {
        console.log(data);
        const myChart = echarts.init(document.getElementById("charts"));
        myChart.setOption({
          legend: {
            top: "bottom",
          },
          tooltip: {
            show: true,
          },
          series: [
            {
              type: "pie",
              data: data.data.chartData.chartData,
              radius: [10, 100],
              center: ["50%", "45%"],
              roseType: "area",
              itemStyle: {
                borderRadius: 10,
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
