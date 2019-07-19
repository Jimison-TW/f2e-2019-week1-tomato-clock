<template>
  <div class="tab">
    <icon :name="iconName" :scale="100" />
    <span>{{ tabText }}</span>
  </div>
</template>

<script>
export default {
  props: {
    iconName: String,
    tabText: String
  }
};
</script>
