<template>
  <div>
    <tabs v-model="name">
      <tab name="First tab" label="First tab">
        This is the content of the first tab
      </tab>
      <tab name="Second tab" label="Second tab">
        This is the content of the second tab
      </tab>
      <tab name="Custom fragment" label="Custom fragment">
        The fragment that is appended to the url can be customized
      </tab>
    </tabs>
  </div>
</template>

<script>
import tabs from "@/components/Tabs.vue";
import tab from "@/components/Tab.vue";

export default {
  name: "TabArea",
  components: {
    tabs,
    tab
  },
  data: () => ({
    name: "First tab"
  })
};
</script>
