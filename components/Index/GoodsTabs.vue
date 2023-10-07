<script setup lang="ts">
const activeTabs = ref("isHot");
</script>

<template>
  <el-tabs
    v-model="activeTabs" class="goods-tabs"
    tab-position="top"
  >
    <el-tab-pane
      name="isHot"
      label="热卖好物"
    >
      123
    </el-tab-pane>
    <el-tab-pane
      name="isNew"
      :lazy="true"
      label="新品上架"
    >
      456
    </el-tab-pane>
    <el-tab-pane
      name="isViews"
      :lazy="true"
      label="人气商品"
    >
      789
    </el-tab-pane>
  </el-tabs>
</template>

<style scoped lang="scss">
.goods-tabs {
  :deep(.el-tabs__item) {
    font-size: 1.2em;
    font-weight: 600;
    font-family: sans-serif;
    letter-spacing: 0.1em;
    padding: 1.4em 1.2em;
    margin-right: 1em;
    display: flex;
    justify-content: center;
  }
}
</style>
