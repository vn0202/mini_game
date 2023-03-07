<template>
  <div class="card" :style="{ width: `${Math.floor(98 / rate)}` + '%' }">
    <div class="card_inner" :class="{ 'is-flip': is_flip }" @click="onFlip">
      <div class="card_face card_face__front">
        <div class="card_content"></div>
      </div>
      <div class="card_face card_face__back">
        <div
          class="card_content"
          :style="{
            backgroundImage: `url(${require('@/assets/' + imgBack)})`,
          }"
        ></div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    imgBack: {
      type: String,
      require: true,
    },
    card: {
      type: [String, Number, Object],
    },
    rate: {
      type: [String, Number, Object],
      require: true,
    },
  },
  data() {
    return {
      is_flip: false,
      disabled: false,
    };
  },
  methods: {
    onFlip() {
      if (!this.disabled) {
        this.is_flip = !this.is_flip;
        if (this.is_flip) this.$emit("onFlip", this.card);
      }
    },
    onCloseFlip() {
      this.is_flip = false;
    },
  },
};
</script>
<style lang="css" scoped>
.card {
  margin-bottom: 1rem;
  aspect-ratio: 3/4;
  height: auto;
  border-radius: 1rem;
  box-shadow: 1px 3px 6px 3px rgba(0, 0, 0, 0.2);
}
.card_inner {
  width: 100%;
  height: 100%;
  position: relative;
  transition: transform 1s;
  transform-style: preserve-3d;
}
.card_inner.is-flip {
  transform: rotateY(-180deg);
}
.card_face {
  position: absolute;
  backface-visibility: hidden;
  overflow: hidden;
  width: 100%;
  height: 100%;
}
.card_face.card_face__back {
  width: 100%;
  height: 100%;
  transform: rotateY(-180deg);
}
.card_face__front .card_content {
  width: 100%;
  height: 100%;
  background: url("@/assets/images/icon_back.png") no-repeat center center;
  background-size: 40px 40px;
}
.card_content {
  width: 100%;
  height: 100%;
  border-radius: 10px;
  background-size: contain;
  background-position: center center;
  background-repeat: no-repeat;
  background-origin: border-box;
  background-clip: border-box;
}
</style>
