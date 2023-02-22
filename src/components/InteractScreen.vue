<template>
  <div class="screen">
    <h1>Interact Screen</h1>
    <div class="screen__inner" :style="{
      width: `${(((624 - 16 * 4) / Math.sqrt(cardArray.length) - 16) * 3 / 4 + 16) * Math.sqrt(cardArray.length)}px`
    }">
      <card-flipped v-for="(card, index) in cardArray" :key="index" :imgBackFaceUrl="`image/${card}.png`"
        :ref="`${index}`" :card="{ index: index, value: card }" @onFlip="checkRule($event)" :cardArray="cardArray" />
    </div>
  </div>
</template>

<script>
import Card from "./Card.vue"
export default {
  props: {
    cardArray: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  data () {
    return {
      rules: [],
    }
  },
  components: {
    CardFlipped: Card,
  },
  methods: {
    checkRule (card) {
      if (this.rules.length === 2) {
        return false;
      }
      this.rules.push(card);
      if (this.rules.length === 2 && this.rules[0].value === this.rules[1].value) {
        this.$refs[`${this.rules[0].index}`][0].onDisabled();
        this.$refs[`${this.rules[1].index}`][0].onDisabled();
        this.rules = [];

        const disabledElements = document.querySelectorAll(".card.is-disabled");
        if (disabledElements && disabledElements.length === this.cardArray.length - 2) {
          setTimeout(() => {
            this.$emit("isFinished");
          }, 1000);
        }
      } else if (this.rules.length === 2 && this.rules[0].value !== this.rules[1].value) {
        // console.log(this.rules[0].index)
        // console.log(this.$refs[`${this.rules[0].index}`]);
        setTimeout(() => {
          this.$refs[`${this.rules[0].index}`][0].onCloseCard();
          this.$refs[`${this.rules[1].index}`][0].onCloseCard();
          this.rules = [];
        }, 1000);
        const disabledElements = document.querySelectorAll(".card.is-disabled");
        console.log(disabledElements);
      }

    }
  },
}
</script>

<style lang="css" scoped>
.screen {
  position: absolute;
  width: 100%;
  height: 100vh;
  /* background-color: var(--dark); */
  background: url(../assets/image/icon_back_1.png) no-repeat center center;

  color: var(--light);
  top: 0;
  left: 0;
  z-index: 2;
}

.screen__inner {
  display: flex;
  flex-wrap: wrap;
  margin: 0 auto;

}
</style>
