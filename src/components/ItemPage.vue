<template>
  <div class="itemPage">
    <slot></slot>
  </div>
</template>

<script>
export default {
}
</script>

<style scoped lang="less">
.itemPage{
  height: 5rem;
  border: 1px solid blue;
  margin: .25rem;
  background-color: rgba(12, 130, rgb(113, 207, 250),255 .45);
}
</style>
