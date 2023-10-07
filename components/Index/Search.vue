<script lang="ts" setup>
import { useStorage } from "@vueuse/core";

// 搜索关键词
const searchWord = ref("");

// 搜索历史 本地存储
const searchHistoryList = useStorage<string[]>("jiwu_index_search", []);


// 正在加载
const isLoading = ref<boolean>(false);

// 搜索记录
const searchPageList = ref([]);

// 搜索
function onSearch() {
searchHistoryList.value.push(searchWord.value);
};

// 是否有结果
const isShowResult = ref<boolean>(true);

// 关闭搜索框
function closeSearch() {
    isShowResult.value = !isShowResult.value;
};

/**
 * 关闭历史记录
 */
function handleClose(item: string) {
    searchHistoryList.value = searchHistoryList.value.filter(v => v !== item);
}

/**
 * 点击历史记录
 */
function clickTag(item: string) {
    searchWord.value = item;
    closeSearch();
}

/**
 * 加载更多数据
 */
function onLoadMore() { }
</script>

<template>
  <div relative>
    <!-- 下拉框 -->
    <el-popover
      width="100%"
      popper-class="relative popover"
      :teleported="false"
      transition="popup"
      placement="bottom-end"
      :show-after="200"
      :hide-after="0"
      trigger="click"
      :visible="isShowResult"
      popper-style="box-shadow:rgba(50, 50, 105, 0.15) 0px 2px 5px 0px, rgba(0, 0, 0, 0.05) 0px 1px 1px 0px;border-radius:4px; height:395px; padding: 1.2em 1.2em;"
      tabindex="0"
    >
      <template #reference>
        <div
          class="content z-1"
          relative
        >
          <transition name="fade">
            <div
              v-show="isShowResult"
              class="#7d7d7d] bg-[ fixed left-0 top-0 h-100vh w-full overflow-hidden backdrop-blur-8px"
              @click="closeSearch"
            />
          </transition>
          <!-- 搜索 -->
          <div
            class="v-input"
            flex-row-c-c
            pb-2
          >
            <ElInput
              v-model.trim="searchWord"
              class="mr-2"
              type="text"
              size="large"
              clearable
              autocomplete="off"
              :prefix-icon="ElIconSearch"
              minlength="2"
              maxlength="30"
              :on-search="onSearch"
              placeholder="搜索商品"
              @focus="isShowResult = true"
              @keyup.esc="closeSearch"
              @keyup.enter="onSearch"
            />
            <ElButton
              type="primary"
              w-66px
              style="transition: 0.2s; position: relative"
              :loading="isLoading"
              @click="onSearch"
            >
              搜索
            </ElButton>
          </div>
          <!-- 搜索历史记录 -->
          <ClientOnly>
            <div
              v-show="!isShowResult"
              class="tags"
              absolute top-0 top-40px z-0 w-full flex flex-nowrap cursor-pointer items-center overflow-hidden py-1
            >
              <ElTag
                v-for="(p, i) in searchHistoryList"
                :key="p + i"
                size="large"
                closable
                class="mr-1 mt-2 transition-300"
                @close="handleClose(p)"
                @click="clickTag(p, i)"
              >
                <span pr-0.3em>{{ p }}</span>
              </ElTag>
            </div>
          </ClientOnly>
        </div>
      </template>
      <!-- 2、搜索结果（商品goods） -->
      <!-- 标题 -->
      <span
        v-show="searchPageList.length > 0"
        px-2
        py-4
        pb-8
      >
        {{ ` 搜索到 ${searchPageList.length} 条数据` }}
      </span>
      <ElIconCloseBold
        class="absolute right-1em top-1em cursor-pointer rounded-4px shadow shadow-inset transition-300 active:transform-scale-80" width="1.6em" style="color: var(--el-color-primary)"
        @click="closeSearch"
      />
      <ElScrollbar v-loading="isLoading" class="flex flex-col overflow-hidden pb-6 pr-2 pt-2" element-loading-background="transparent" @scroll="onLoadMore">
        <div v-if="searchPageList.length > 0">
          123
        </div>
        <ElEmpty v-show="searchPageList.length <= 0" class="mt-10" description="没有找到商品" :image-size="80" />
      </ElScrollbar>
    </el-popover>
  </div>
</template>

<!-- 样式scss -->
<style scoped lang="scss">
$height: 2.6rem;
.v-input {
  :deep(.el-button) {
    padding: 0 30px;
    letter-spacing: 0.2em;
    height: $height;
    margin-right: 0;
  }

  :deep(.el-input__wrapper) {
    height: $height;
    transition: $transition-delay;
    letter-spacing: 0.2em;

    &.is-focus {
      backdrop-filter: blur(20px);
    }
  }
}

// 弹出框
.popover {
  display: flex;
  flex-direction: column;
  align-items: center;

  &hover {
    width: 100%;
  }

  :deep(.el-popover__title) {
    width: 100%;
    text-align: center !important;
  }
}

.tags .el-tags .el-tag__content {
  :deep(.el-close) {
    opacity: 0;
  }

  :deep(.el-close):hover {
    opacity: 1;
  }
}
</style>
