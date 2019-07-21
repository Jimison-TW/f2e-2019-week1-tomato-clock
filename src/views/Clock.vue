<template>
  <div class="clock-player">
    <icon
      :name="iconName"
      :scale="500"
      id="play-icon"
      @click.native="callStart"
    />
    <p>{{ remainTime | prettify }}</p>
    <p>{{ thingName }}</p>
  </div>
</template>

<script>
export default {
  props: {
    iconName: String,
    thingName: String,
    remainTime: String
  },
  name: "Clock",
  data: () => ({
    isRunning: false
  }),
  filters: {
    prettify: function(value) {
      let data = value.split(":");
      let minutes = data[0];
      let secondes = data[1];
      if (minutes < 10) {
        minutes = "0" + minutes;
      }
      if (secondes < 10) {
        secondes = "0" + secondes;
      }
      return minutes + ":" + secondes;
    }
  },
  methods: {
    callStart() {
      if (this.isRunning) {
        this.$emit("stop");
        this.isRunning = false;
        return;
      }
      console.log("callStart");
      this.$emit("start");
      this.isRunning = true;
    }
  }
};
</script>

<style scope>
.clock-player {
  margin-top: 160px;
  text-align: center;
}
</style>
