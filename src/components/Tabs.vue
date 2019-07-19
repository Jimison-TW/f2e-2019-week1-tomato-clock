<template>
  <div class="tabs-component">
    <ul role="tablist" class="tabs-component-tabs">
      <li
        v-for="(tab, index) in tabs"
        :key="index"
        :class="{ 'is-active': tab.name === value }"
        class="tabs-component-tab"
      >
        <!-- 產出頁籤，而tab.name是從調用端傳給tab，再取this.$children來取得裡面的props -->
        <a @click="selectTab(tab.name)" class="tabs-component-tab-a">{{
          tab.label
        }}</a>
      </li>
    </ul>
    <div class="tabs-component-panels">
      <!-- 產出內容區塊，如果這邊沒有slot的話，就無法取得children的值了 -->
      <slot />
    </div>
  </div>
</template>

<script>
export default {
  name: "tabs",
  props: ["value"],
  data() {
    return {
      tabs: []
    };
  },
  methods: {
    selectTab(tabName) {
      this.$emit("input", tabName);
    }
  },
  created() {
    // tabs是從子元件取得的，也就是tab的部份，可以取得子元件的vue內容
    this.tabs = this.$children;
  }
};
</script>

<style scoped>
.tabs-component {
  margin: 4em 0;
}

.tabs-component-tabs {
  border: solid 1px #ddd;
  border-radius: 6px;
  list-style: none;
  margin-bottom: 5px;
}

@media (min-width: 700px) {
  .tabs-component-tabs {
    border: 0;
    align-items: stretch;
    display: flex;
    justify-content: flex-start;
    margin-bottom: -1px;
  }
}

.tabs-component-tab {
  color: #999;
  font-size: 14px;
  font-weight: 600;
  margin-right: 0;
}

.tabs-component-tab:not(:last-child) {
  border-bottom: dotted 1px #ddd;
}

.tabs-component-tab:hover {
  color: #666;
}

.tabs-component-tab.is-active {
  color: #000;
}

@media (min-width: 700px) {
  .tabs-component-tab {
    background-color: #fff;
    border: solid 1px #ddd;
    border-radius: 3px 3px 0 0;
    margin-right: 0.5em;
    transform: translateY(2px);
    transition: transform 0.3s ease;
  }

  .tabs-component-tab.is-active {
    border-bottom: solid 1px #fff;
    z-index: 2;
    transform: translateY(0);
  }
}

.tabs-component-tab-a {
  align-items: center;
  color: inherit;
  display: flex;
  padding: 0.75em 1em;
  text-decoration: none;
  cursor: pointer;
}

.tabs-component-panels {
  padding: 4em 0;
}

@media (min-width: 700px) {
  .tabs-component-panels {
    border-top-left-radius: 0;
    background-color: #fff;
    border: solid 1px #ddd;
    border-radius: 0 6px 6px 6px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.05);
    padding: 4em 2em;
  }
}
</style>
