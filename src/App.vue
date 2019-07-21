<template>
  <div id="app">
    <div id="sidebar">
      <Clock
        :iconName="iconName"
        :thingName="doingThing"
        :remainTime="prettyTime"
        @start="start"
        @stop="stop"
      />
    </div>
    <div id="container">
      <div id="content">
        <router-link to="/">
          <TabButton iconName="baseline-list-24px" tabText="TO DO LIST" />
        </router-link>
        <router-link to="/home">
          <TabButton iconName="baseline-adjust-24px" tabText="ANALYTICS" />
        </router-link>
        <router-link to="/about">
          <TabButton iconName="baseline-settings-20px" tabText="SETTING" />
        </router-link>
      </div>
      <router-view @onItemClicked="onClickedItem" />
    </div>
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
  },
  data: () => ({
    iconName: "baseline-play_circle_outline-24px",
    doingThing: "",
    minutes: 0,
    secondes: 0,
    time: 0,
    timer: null
  }),
  methods: {
    onClickedItem: function(itemName, remainTime) {
      console.log(itemName, remainTime);
      this.doingThing = itemName;
      this.time = remainTime * 60;
    },
    start() {
      if (!this.timer) {
        this.iconName = "baseline-pause_circle_outline-24px";
        this.timer = setInterval(() => {
          if (this.time > 0) {
            this.time--;
          } else {
            this.iconName = "baseline-play_circle_outline-24px";
            clearInterval(this.timer);
            this.reset();
          }
        }, 1000);
      }
    },
    stop() {
      console.log("stop");
      this.iconName = "baseline-play_circle_outline-24px";
      clearInterval(this.timer);
      this.timer = null;
    },
    reset() {
      this.stop();
      this.time = 0;
      this.secondes = 0;
      this.minutes = 0;
    },
    setTime(payload) {
      this.time = payload.minutes * 60 + payload.secondes;
    }
  },
  computed: {
    prettyTime() {
      let time = this.time / 60;
      let minutes = parseInt(time);
      let secondes = Math.round((time - minutes) * 60);
      return minutes + ":" + secondes;
    }
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
