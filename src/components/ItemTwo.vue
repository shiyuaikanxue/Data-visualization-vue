<template>
  <div class="itemTwo">
    <h2>周销图</h2>
    <div class="chart" id="myChart"></div>
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
        url: "/two/data",
      });
    }
    onMounted(() => {
      getState().then(() => {
        console.log(data);
        const myChart = echarts.init(document.getElementById("myChart"));
        myChart.setOption({
          tooltip: {
            trigger: "axis",
            axisPointer: {
              type: "cross",
              label:{
                color:'#e6b600'
              }
            },
          },
          legend:{
            show:true,
            top:'1%'
          },
          grid:{
            left:'0%',
            right:'4%',
            bottom:'3%',
            containLabel:true
          },
          xAxis: {
            type: "category",
            boundaryGap: false,
            data: data.data.chartData.chartData.day,
            axisLine:{
              lineStyle:{
                color:'white'
              }
            }
          },
          yAxis: {
            type: "value",
            axisLine:{
              lineStyle:{
                color:'white'
              }
            }
          },
          series: [
            {
              name: "服饰",
              type: "line",
              data: data.data.chartData.chartData.num.Chemicals,
              smooth: true,
              showSymbol: false,
              stack: "total",
              lineStyle: {
                width: 0,
              },
              emphasis: {
                focus: "series",
              },
              areaStyle: {
                opacity: 0.8,
                color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
                  {
                    offset: 0,
                    color: "rgba(128,255,165)",
                  },
                  {
                    offset: 1,
                    color: "rgba(1,191,236)",
                  },
                ]),
              },
            },
            {
              name: "数码",
              type: "line",
              data: data.data.chartData.chartData.num.Clothes,
              smooth: true,
              showSymbol: false,
              stack: "total",
              lineStyle: {
                width: 0,
              },
              emphasis: {
                focus: "series",
              },
              areaStyle: {
                opacity: 0.8,
                color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
                  {
                    offset: 0,
                    color: "rgba(0,221,255)",
                  },
                  {
                    offset: 1,
                    color: "rgba(77,119,255)",
                  },
                ]),
              },
            },
            {
              name: "家电",
              type: "line",
              data: data.data.chartData.chartData.num.Electrical,
              smooth: true,
              showSymbol: false,
              stack: "total",
              lineStyle: {
                width: 0,
              },
              emphasis: {
                focus: "series",
              },
              areaStyle: {
                opacity: 0.8,
                color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
                  {
                    offset: 0,
                    color: "rgba(55,162,255)",
                  },
                  {
                    offset: 1,
                    color: "rgba(116,21,219)",
                  },
                ]),
              },
            },
            {
              name: "家具",
              type: "line",
              data: data.data.chartData.chartData.num.digit,
              smooth: true,
              showSymbol: false,
              stack: "total",
              lineStyle: {
                width: 0,
              },
              emphasis: {
                focus: "series",
              },
              areaStyle: {
                opacity: 0.8,
                color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
                  {
                    offset: 0,
                    color: "rgba(255,0,135)",
                  },
                  {
                    offset: 1,
                    color: "rgba(135,0,157)",
                  },
                ]),
              },
            },
            {
              name: "日化",
              type: "line",
              data: data.data.chartData.chartData.num.gear,
              smooth: true,
              showSymbol: false,
              stack: "total",
              lineStyle: {
                width: 0,
              },
              emphasis: {
                focus: "series",
              },
              areaStyle: {
                opacity: 0.8,
                color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
                  {
                    offset: 0,
                    color: "rgba(255,191,0)",
                  },
                  {
                    offset: 1,
                    color: "rgba(224,62,76)",
                  },
                ]),
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
