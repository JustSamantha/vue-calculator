<script setup lang="ts">
  let calculator = "";
  function addSymbol(event) {
    console.log(event.target.innerText);
    calculator = event.target.innerText;
  }
</script>

<template>
  <main>
    <input type="text" v-bind:src="calculator" disabled="true" />
    <button @click="addSymbol">0</button>
    <button @click="addSymbol">1</button>
    <button @click="addSymbol">2</button>
    <button @click="addSymbol">3</button>
    <button @click="addSymbol">4</button>
    <button @click="addSymbol">5</button>
    <button @click="addSymbol">6</button>
    <button @click="addSymbol">7</button>
    <button @click="addSymbol">8</button>
    <button @click="addSymbol">9</button>
    <button @click="addSymbol">+</button>
    <button @click="addSymbol">-</button>
    <button @click="addSymbol">/</button>
    <button @click="addSymbol">*</button>
  </main>
</template>

<style scoped>

</style>
