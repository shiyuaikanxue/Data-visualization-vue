<template>
  <div class="map" id="map"></div>
</template>

<script>
import axios from "axios";
import { inject, onMounted, reactive } from "vue";
export default {
  setup() {
    let mapData = reactive({});
    const echarts = inject("echarts");
    async function getState() {
      mapData = await axios.get("/map/data");
      console.log(mapData)
    }
    onMounted(() => {
      getState().then(() => {
        echarts.registerMap("china", mapData.data.chartData);
        const map = echarts.init(document.getElementById("map"));
        map.setOption({
          geo: {
            map: "china",
            itemStyle: {
              areaColor: "#0099ff",
              borderColor: "#00ffff",
              shadowColor: "rgba(230,130,70,.5)",
              shadowBlur: 30,
              emphasis: {
                focus: "self",
              },
            },
          },
          title: {
            text: "城市销量",
            left: "45%",
            textStyle: {
              color: "#fff",
              fontSize: 20,
              textShadowBlur: 10,
              textShadowColor: "#33ffff",
            },
          },
          tooltip: {
            trigger: "item",
          },
          visualMap: {
            type: "continuous",
            min: 100,
            max: 5000,
            calculable: true,
            inRange: { color: ["#50a3ba", "#eac736", "#d94e5d"] },
            textStyle: {
              color: "white",
            },
          },
          series: [
            {
              type: "scatter",
              itemStyle: {
                color: "red",
              },
              coordinateSystem: "geo",
              data: [
                { name: "北京", value: [116.46, 39.92, 4367] },
                { name: "上海", value: [121.48, 31.22, 8657] },
                { name: "深圳", value: [114.07, 22.62, 2461] },
                { name: "广州", value: [113.23, 23.16, 187] },
                { name: "西安", value: [108.45, 34, 3421] },
              ],
            },
          ],
        });
        console.log(mapData);
      });
    });
    return {
      getState,
      mapData,
    };
  },
};
</script>

<style>
.map {
  width: 100%;
  height: 100%;
}
</style>
