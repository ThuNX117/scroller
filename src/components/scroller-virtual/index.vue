<template>
  <div ref="containerRef" class="container" @scroll="handleScroll">
    <div class="phantom" :style="{ height: totalHeight + 'px' }"></div>
    <div class="content" :style="{ transform: `translateY(${offset}px)` }">
      <div v-for="item in visibleItems" :key="item.id" class="item">
        <Item @onTriggerTab="handleOnTab" :id="item.id" />
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
  import { computed, ref } from "vue";
  import Item from "./item.vue";
  const items = ref(
    Array.from({ length: 500 }, (_, i) => ({ id: i, text: `Item ${i}` }))
  );
  const itemHeight = ref(50);
  const visibleCount = ref(10);
  const startIndex = ref(0);
  const offset = ref(0);
  const containerRef = ref();
  const endIndex = computed(() => {
    return Math.min(startIndex.value + visibleCount.value, items.value.length);
  });
  const visibleItems = computed(() => {
    return items.value.slice(startIndex.value, endIndex.value);
  });
  const totalHeight = computed(() => {
    return items.value.length * itemHeight.value;
  });
  const handleOnTab = () => {
    console.log("onTab");
    if (containerRef.value.scrollTop) {
      containerRef.value.scrollTop = (containerRef.value?.scrollTop ?? 0) + 30;
      handleScroll();
    }
  };
  const handleScroll = () => {
    const scrollTop = containerRef.value?.scrollTop ?? 0;
    startIndex.value = Math.floor(scrollTop / itemHeight.value);
    offset.value = startIndex.value * itemHeight.value;
  };
</script>

<style scoped>
  .container {
    overflow: auto;
    position: relative;
    height: 500px;
  }
  .phantom {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
  }
  .content {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
  }
  .item {
    height: 50px;
    line-height: 50px;
    border-bottom: 1px solid #ccc;
  }
</style>
computed,
