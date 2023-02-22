<template>
  <div class="screen">
    <h1>Congratulations</h1>
    <p>{{ Math.round(timer / 1000) }}milisecond</p>
    <button @click="startAgain">Start again</button>
  </div>
</template>

<script>
export default {
  props: {
    timer: {
      type: Number,
      required: true,
    },
  },
  methods: {
    startAgain() {
      this.$emit("startAgain");
    },
  },
}
</script>
