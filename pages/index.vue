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
      <div py-0 layout-default>
        <div class="flex flex-col">
          <IndexTopMenu w-full />
          <!-- 热门商品分类 -->
          <IndexCategoryLine class="mt-6 md:my-8" />
          <!-- 商品Tabs -->
          <div class="mv-10vh mt-4 min-h-100vh">
            <IndexGoodsTabs />
          </div>
        </div>
      </div>
    </NuxtLayout>
  </div>
</template>

<style scoped>

</style>
