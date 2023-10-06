<script setup lang="ts">
import { appName } from "./constants";

useHead({
   title: `${appName} - 开启你的极物之旅 ✨`,
  meta: [
    {
      name: "description",
      content: "极物圈-主页 开启你的极物之旅！",
    },
  ],
});

useSeoMeta({
  title: `${appName} - 开启你的极物之旅 ✨`,
  description: "极物圈-主页 开启你的极物之旅！",
  keywords: "社区,商城,极物之旅,主页,购物,home,index,shop",
  referrer: "no-referrer",
});

const showOtherLoading = ref<boolean>(true);

onMounted(() => {
  if (document && document.body)
    document.body.style.overflow = "hidden";
});

onNuxtReady(async () => showOtherLoading.value = false);
</script>

<template>
  <NuxtLayout name="default">
    <Transition name="fade">
      <OtherLoading v-show="showOtherLoading" />
    </Transition>
    123
  </NuxtLayout>
</template>

<style>
.page-enter-active,
.page-leave-active {
  transition: all 0.3s;
}
.page-enter-from,
.page-leave-to {
  opacity: 0;
  filter: blur(16px) contrast(6);
}
.dark .page-enter-from,
.dark .page-leave-to {
  filter: blur(0) grayscale(0) ;
}


.layout-enter-active,
.layout-leave-active {
  transition: all 0.3s;
}
.layout-enter-from,
.layout-leave-to {
  opacity: 0;
  filter: blur(16px) contrast(6);
}
.dark .layout-enter-from,
.dark .layout-leave-to {
  opacity: 0;
  filter: blur(0) grayscale(1) ;
}
</style>
