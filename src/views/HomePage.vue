<template>
  <div>
    <header><h1>大数据可视化</h1></header>
    <section class="container">
      <section class="itemLeft">
        <ItemPage><ItemOne></ItemOne></ItemPage>
        <ItemPage>
          <ItemTwo></ItemTwo>
        </ItemPage>
      </section>
      <section class="itemCenter">
        <MapPage></MapPage>
      </section>
      <section class="itemRight">
        <ItemPage>
          <ItemThree></ItemThree>
        </ItemPage>
        <ItemPage>
          <ItemFour></ItemFour>
        </ItemPage>
      </section>
    </section>
  </div>
</template>

<script>
import ItemPage from "@/components/ItemPage.vue";
import ItemOne from "@/components/ItemOne.vue";
import ItemTwo from "@/components/ItemTwo.vue";
import ItemThree from "@/components/ItemThree.vue";
import ItemFour from "@/components/ItemFour.vue";
import { inject } from "vue";
import MapPage from '@/components/mapPage.vue';
export default {
  components: {
    ItemPage,
    ItemOne,
    ItemTwo,
    ItemThree,
    ItemFour,
    MapPage
  },
  setup() {
    const echarts = inject("echarts");
    const axios = inject("axios");
    console.log(echarts);
    console.log(axios);
  },
};
</script>

<style lang="less">
header {
  height: 1rem;
  width: 100%;
  background-color: rgba(0, 0, 255, 0.2);
  h1 {
    font-size: 0.375rem;
    color: white;
    text-align: center;
    line-height: 1rem;
  }
}
.container {
  min-width: 1200px;
  max-width: 2048px;
  margin: 0 auto;
  padding: 0.125rem 0.125rem 0;
  display: flex;
  .itemLeft,
  .itemRight {
    flex: 3.5 ;
  }
  .itemCenter {
    flex: 5;
    margin: 0.25rem;
    border: 1px solid blue;
    padding: .25rem;
  }
}
</style>
