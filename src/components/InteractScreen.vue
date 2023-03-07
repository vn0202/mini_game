<template>
  <div class="interact-screen">
    <card-item
      v-for="(card, index) in cardsContent"
      :key="index"
      :ref="`card-${index}`"
      :img-back="`images/${card}.png`"
      :card="{ index: index, value: card }"
      :rate="rate"
      @onFlip="checkRule($event)"
    ></card-item>
  </div>
</template>
<script>
import CardItem from "@/components/CardItem.vue";

export default {
  props: {
    cardsContent: {
      type: Array,
      default: () => [],
    },
  },
  components: {
    CardItem,
  },
  data() {
    return {
      rule: [],
      machine_cacular: 0,
      time: new Date().getTime(),
      rate: Math.sqrt(this.cardsContent.length),
    };
  },
  methods: {
    checkRule(card) {
      if (this.rule.length == 2) return false;
      this.rule.push(card);
      if (this.rule.length == 2 && this.rule[0].value == this.rule[1].value) {
        this.$refs[`card-${this.rule[0].index}`][0].disabled = true;
        this.$refs[`card-${this.rule[1].index}`][0].disabled = true;
        this.rule = [];
        this.machine_cacular++;
        if (this.machine_cacular == 8) {
          setTimeout(() => {
            let result = new Date().getTime() - this.time;
            this.$emit("onSuccess", result);
          }, 800);
        }
      } else if (
        this.rule.length == 2 &&
        this.rule[0].value != this.rule[1].value
      ) {
        setTimeout(() => {
          this.$refs[`card-${this.rule[0].index}`][0].onCloseFlip();
          this.$refs[`card-${this.rule[1].index}`][0].onCloseFlip();
          this.rule = [];
        }, 800);
      } else {
        return false;
      }
    },
  },
};
</script>
<style lang="css" scoped>
.interact-screen {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  align-content: baseline;
}
</style>
