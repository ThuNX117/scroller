<template>
  <div class="item-row">
    <span>{{ id }}</span>
    <input class="w-52 h-10" />
    <input class="w-52 h-10" />
    <input class="w-52 h-10" />
    <input class="w-52 h-10" />
    <input class="w-52 h-10 bg-red" @keydown.tab="handleTab" />
  </div>
</template>
<script setup lang="ts">
  type Props = {
    id: number;
  };
  const emits = defineEmits<{
    onTriggerTab: [];
  }>();
  defineProps<Props>();
  const handleTab = () => {
    emits("onTriggerTab");
  };
</script>
<style>
  .item-row {
    display: flex;
    flex-direction: row;
    gap: 1rem;
    position: relative;
  }
  .item-row > .text {
    position: sticky;
    left: 0;
  }
  .item-row > input:last-child {
    background: red;
  }
</style>
