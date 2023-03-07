<template>
  <div class="main-screen">
    <h1 :style="{ color: 'red' }">POKEMON MEMORIES</h1>
    <h3>Select mode to start game</h3>
    <div class="actions">
      <button @click="onStart(16)">
        <span>4x4</span>
        <span>Easy</span>
      </button>
      <button @click="onStart(36)">
        <span>6x6</span>
        <span>Medium</span>
      </button>
      <button @click="onStart(64)">
        <span>8x8</span>
        <span>Hard</span>
      </button>
      <button @click="onStart(100)">
        <span>10x10</span>
        <span>very hard</span>
      </button>
    </div>
  </div>
</template>
<script>
export default {
  methods: {
    onStart(totalBlock) {
      this.$emit("onStart", { totalBlock: totalBlock });
    },
    onDarkMode() {
      this.$emit("onDarkMode");
    },
  },
};
</script>
<style scoped>
.mode {
  text-align: right;
}
.main-screen {
  margin: 0 auto;
  min-width: 500px;
  display: flex;
  flex-direction: column;
  align-content: center;
  justify-content: center;
  align-items: center;
}

h1 {
  text-align: center;
  font-size: 50px;
  font-weight: bolder;
}
h3 {
  margin: 20px 0;
}
.actions {
  width: 100%;
  display: flex;
  justify-content: space-around;
}
button {
  font-size: 20px;
  flex-basis: 20%;
  aspect-ratio: 1/1;
  height: auto;
  font-weight: bold;
}
button span {
  display: block;
}
</style>
