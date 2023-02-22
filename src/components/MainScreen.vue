<template>
  <div class="screen">

    <h1>POKE MEMORIES</h1>
    <h3>Select mode to start game</h3>
    <div class="container">
      <button @click="onStart(16)">
        <p>4x4</p>
        <p>easy</p>
      </button>
      <button @click="onStart(36)">
        <p>6x6</p>
        <p>normal</p>
      </button>

    </div>
  </div>
</template>

<script>
export default {
  methods: {
    onStart (numberOfBlocks) {
      this.$emit('onStart', numberOfBlocks)
    }
  }
}
</script>

<style lang="css" scoped>
.screen {
  background-color: var(--dark);
  /* background: url(../assets/image/icon_back_1.png) no-repeat center center; */
  color: var(--light);
  display: flex;
  margin: auto;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

h1 {
  font-size: 3.5rem;
}

h3 {
  font-size: 2rem;
}

button {
  background-color: var(--dark);
  color: var(--light);
  width: 80px;
  height: 80px;
  border: 1px solid var(--light);
  margin: 1rem 1.5rem;
  padding: 1rem;
  border-radius: 1rem;
  font-size: 1.5rem;
  font: var(--font);
  cursor: pointer;
  display: inline-block;
  justify-content: center;
}

button:hover {
  background-color: #a8a6a6;
}

button p {
  font-size: 1.2rem;
}
</style>
