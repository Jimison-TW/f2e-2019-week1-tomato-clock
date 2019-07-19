<template>
  <div class="clock-player">
    <icon
      name="baseline-play_circle_outline-24px"
      :scale="500"
      id="play-icon"
    />
    <p>25:00</p>
    <p>The First Thing To Do</p>
  </div>
</template>

<script>
export default {
  name: "Clock"
};
</script>

<style scope>
.clock-player {
  margin-top: 160px;
  text-align: center;
}
</style>
