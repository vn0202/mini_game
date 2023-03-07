<template>
  <div class="screen-result">
    <div class="screen-content">
      <h1>✨ Congratulations ✨</h1>
      <p>
        Your result is :
        <span class="score">{{ Math.round(result / 1000) }}s</span>
      </p>
      <button @click="restart">Restart</button>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    result: {
      type: [String, Number, Object],
      require: true,
    },
  },
  methods: {
    restart() {
      this.$emit("restart");
    },
  },
};
</script>
<style lang="css" scoped>
.screen-result {
  width: 100%;
  height: 100vh;
  margin: 0 auto;
  display: flex;
}
.screen-content {
  margin: auto;
  text-align: center;
}
.screen-content .score {
  color: green;
}
</style>
