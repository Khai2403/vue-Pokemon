<template>
  <MainScreen v-if="statusMatch === 'default'" @onStart="renderInteractScreen($event)" />
  <InteractScreen v-if="statusMatch === 'interact'" :cardArray="setting.cardArray" @isFinished="renderResultScreen" />
  <ResultScreen v-if="statusMatch === 'result'" :timer="timer" @startAgain="startAgain" />
  <CopyRightScreen />
</template>

<script>
import MainScreen from './components/MainScreen.vue';
import CopyRightScreen from './components/CopyRightScreen.vue';
import InteractScreen from './components/InteractScreen.vue';
import ResultScreen from './components/ResultScreen.vue';
import { shuffled } from "./utils/Array.js"
export default {
  name: 'App',
  components: {
    MainScreen,
    InteractScreen,
    ResultScreen,
    CopyRightScreen,
  },
  data () {
    return {
      setting: {
        numberOfBlocks: 0,
        cardArray: [],
        startAt: null,
      },
      statusMatch: "default",
      timer: 0,
    }
  },
  methods: {
    renderInteractScreen (config) {
      this.setting.numberOfBlocks = config;
      const firstArray = Array.from({ length: this.setting.numberOfBlocks / 2 }, (_, i) => i + 1);
      const secondArray = [...firstArray]; /* copy mảng firstArray */
      const cards = [...firstArray, ...secondArray];
      this.setting.cardArray = shuffled(shuffled(shuffled(cards))); // đảo lộn xộn các phần tử trong cards
      //sort((a,b) => Math.random() - 0.5) random được 1 số < 0 thì a đứng trước b và ngược lại
      this.setting.startAt = new Date().getTime(); // tạo được mảng thì bắt đầu tính thời gian
      this.statusMatch = "interact";
    },
    renderResultScreen () {
      this.timer = new Date().getTime() - this.setting.startAt;

      this.statusMatch = "result";
    },
    startAgain () {
      this.statusMatch = "default";
    },
  }
}
</script>
