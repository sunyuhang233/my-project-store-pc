<script setup lang="ts">
const props = withDefaults(defineProps<{
  noMore?: boolean
  immediate?: boolean
  delay?: number
}>(), {
  noMore: false,
  immediate: true,
  delay: 400,
});

const emit = defineEmits("load");

const loadMoreRef = ref();

let timer: any = 0;

onMounted(() => {
  if (props.immediate)
    emit("load");
});
onUnmounted(() => {
  clearInterval(timer);
});


const { stop } = useIntersectionObserver(
     // 如果target对应的DOM进入可视区，那么该回调函数就触发
      loadMoreRef,
      ([{ isIntersecting }]) => {
          if (isIntersecting) {
             // 如果target对应的DOM进入可视区，那么该回调函数就触发
              timer = setInterval(() => {
                  if (props.noMore)
                // 如果还有更多数据 ，那么就继续加载数据
                      timer && clearInterval(timer);
                  emit("load");
            }, props.delay);
          }
          else {
            // 如果target对应的DOM离开可视区，那么该回调函数就触发
            timer && clearInterval(timer);
          }
      },
    );

watch(() => props.noMore, (val) => {
    if (val)
        stop && stop();
});

defineExpose({
    loadMoreRef,
    stop,
});
</script>

<template>
  <slot name="default" />
  <div v-if="!noMore" ref="loadMoreRef" key="loadMoreRef">
    <slot name="load">
      <p h-2 w-full opacity-0 />
    </slot>
  </div>
</template>

<style scoped>

</style>
