<script setup lang="ts">
import { appName } from "@/constants";

// 定义页面元数据
definePageMeta({
  key: route => route.path,
  layout: false,
});
useHead({
  title: `${appName} - 开启你的极物之旅 ✨`,
  meta: [
    {
      name: "description",
      content: "极物圈-主页 开启你的极物之旅！",
    },
  ],
});
</script>

<template>
  <div>
    <NuxtLayout name="main">
      main
    </NuxtLayout>
  </div>
</template>

<style scoped>

</style>
