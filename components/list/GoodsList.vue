
<script setup lang="ts">
const isNoMore = ref(false);

function loadGoodsPage() {}
</script>

<template>
  <ListAutoIncre :no-more="isNoMore" @load="loadGoodsPage">
    123
  </ListAutoIncre>
</template>
