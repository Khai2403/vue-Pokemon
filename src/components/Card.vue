<template>
  <div class="card" :class="{ 'is-disabled': isDisabled }" :style="{
    height: `${(624 - 16 * 4) / Math.sqrt(cardArray.length) - 16}px`,
    width: `${((624 - 16 * 4) / Math.sqrt(cardArray.length) - 16) * 3 / 4}px`,
    perspective: `${((624 - 16 * 4) / Math.sqrt(cardArray.length) - 16) * 3 / 4 * 2}px`
  }">
    <div class="card_inner" :class="{ 'is-flipped': isFlipped }" @click="ontoggle">
      <div class="card_face card_front">
        <div class="card_content">
        </div>
      </div>
      <div class="card_face card_backside">
        <div class="card_content" :style="{ backgroundImage: `url(${require('@/assets/' + imgBackFaceUrl)}` }">
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  props: {
    imgBackFaceUrl: {
      type: String,
      required: true,
    },
    card: {
      type: Object,
      required: true,
    },
    cardArray: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  data () {
    return {
      isFlipped: false,
      isDisabled: false,
    }
  },
  methods: {
    ontoggle () {
      if (this.isDisabled) return false;
      this.isFlipped = !this.isFlipped
      if (this.isFlipped) this.$emit("onFlip", this.card);
    },
    onCloseCard () {
      this.isFlipped = false;
    },
    onDisabled () {
      this.isDisabled = true;
    },
  }
}
</script>

<style lang="css" scoped>
.card {
  display: inline-block;
  margin-right: 1rem;
  margin-bottom: 1rem;
  cursor: pointer;
}

.card.is-disabled {
  cursor: default;
}

.card_inner {
  position: relative;
  border-radius: 1rem;
  box-shadow: 0 3px 10px 3px rgba(0, 0, 0, 0.3);
  width: 100%;
  height: 100%;
  transition: transform 1s;
  /*thời gian quay là 1s*/
  transform-style: preserve-3d;
  /*quay 3d */
}

.card_inner.is-flipped {
  transform: rotateY(-180deg);
}

.card_face {
  position: absolute;
  backface-visibility: hidden;
  width: 100%;
  height: 100%;
  padding: 1rem;
  overflow: hidden;
}

.card_front .card_content {
  background: url(../assets/image/icon_back_1.png) no-repeat center center;
  background-size: contain;
  height: 100%;
  width: 100%;
}

.card_backside {
  background-color: var(--light);
  transform: rotateY(-180deg);
  border-radius: 1rem;
}

.card_backside .card_content {
  background-size: contain;
  background-position: center center;
  background-repeat: no-repeat;
  height: 100%;
  width: 100%;
}
</style>
