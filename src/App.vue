<template>
  <main-screen
    v-if="showScreen === 'default'"
    @onStart="onChangeToInteract($event)"
    @onDarkMode="turnDarkMode"
  >
  </main-screen>
  <interact-screen
    v-if="showScreen === 'in_match'"
    :cardsContent="setting.cardsContent"
    @onSuccess="turnResultScreen($event)"
  ></interact-screen>
  <result-screen
    v-if="showScreen === 'result'"
    :result="result"
    @restart="onRestart"
  ></result-screen>
</template>

<script>
import { shuffed } from "@/helper/array";
import MainScreen from "@/components/MainScreen.vue";
import InteractScreen from "@/components/InteractScreen.vue";
import ResultScreen from "@/components/ResultScreen.vue";

export default {
  data() {
    return {
      setting: {
        totalBlock: 0,
        cardsContent: [],
        dark_mode: "black",
      },
      showScreen: "default",
      result: 0,
    };
  },
  components: {
    ResultScreen,
    MainScreen,
    InteractScreen,
  },
  methods: {
    turnResultScreen(result) {
      this.result = result;
      this.showScreen = "result";
    },
    onChangeToInteract(config) {
      this.setting.totalBlock = config.totalBlock;
      const inital_array = Array.from(
        { length: this.setting.totalBlock / 2 },
        (_, i) => i + 1
      );
      const cards_list = [...inital_array, ...inital_array];
      this.setting.cardsContent = shuffed(
        shuffed(shuffed(shuffed(cards_list)))
      );
      this.showScreen = "in_match";
    },
    onRestart() {
      this.showScreen = "default";
    },
    turnDarkMode() {
      this.dark_mode = true;
    },
  },
};
</script>

<style>
#app {
  display: flex;
  padding: 100px 400px;
  flex-direction: column;
  width: 100%;
  height: 100%;
  background-color: #212121;
}
</style>
