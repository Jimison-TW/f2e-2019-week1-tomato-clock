<template>
  <section v-show="isActive" class="tabs-component-panel">
    <!-- 放置內容區塊 -->
    <slot />
  </section>
</template>

<script>
export default {
  name: "tab",
  props: {
    name: { required: true },
    label: { required: true }
  },
  computed: {
    isActive() {
      // this.$parent.value取得tabs裡面value的值
      return this.name === this.$parent.value;
    }
  }
};
</script>
