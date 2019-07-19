<template>
  <div id="app">
    <div id="sidebar">
      <Clock />
    </div>
    <div id="container">
      <div id="content">
        <router-link to="/">
          <TabButton iconName="baseline-list-24px" tabText="TO DO LIST" />
        </router-link>
        <router-link to="/about">
          <TabButton iconName="baseline-adjust-24px" tabText="ANALYTICS" />
        </router-link>
        <router-link to="/home">
          <TabButton iconName="baseline-settings-20px" tabText="SETTING" />
        </router-link>
      </div>
      <div>
        <input type="text" />
        <input type="button" value="新增" />
      </div>
      <router-view />
    </div>
    <!-- <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view /> -->
  </div>
</template>

<script>
import Clock from "@/views/Clock.vue";
import TabButton from "@/components/TabButton.vue";

export default {
  name: "app",
  components: {
    Clock,
    TabButton
  }
};
</script>

<style>
#app {
  display: table;
  width: 100%;
  height: 100%;
}

#sidebar {
  display: table-cell;
  width: 40%;
  position: fixed;
  vertical-align: top;
}

#container {
  display: table-cell;
  width: 60%;
  vertical-align: top;
}

#content {
  display: flex;
  text-align: center;
}

.center-inline {
  margin: 0px auto;
}

.center-inline div {
  display: inline-block;
  vertical-align: top;
  width: 300px;
}

.list-title {
  padding-left: 20px;
  text-align: left;
}

.list-item {
  text-align: left;
}
</style>
