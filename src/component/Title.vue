<template>
  <div class="contents_header">
    <span class="title">{{ title }}</span>
    <div>
      <slot></slot>
    </div>
  </div>
</template>
<script setup>
const props = defineProps({
  title: {
    type: String,
    default: undefined,
  },
});
</script>
<style lang="scss" scoped>
.contents_header {
  margin: 50px 0px;
  .title {
    font-family: "Life Savers", sans-serif;
    font-size: 40px;
    color: var(--text-color);
  }
}
</style>
