<script setup lang="ts">
  import { ref } from 'vue';

  const calculatorDisplay = ref('');
  let currentSymbol = '';
  let storedValue = '';
  let clearInput = false;

  function addInput(event:Event) {
    if (event.target && event.target.innerText) {
      const input = event.target.innerText;
      if (isSymbol(input)) {
        addSymbol(input);
      } else if (input === '=') {
        doMath();
        currentSymbol = '';
        storedValue = '';
      } else if (input === 'C') {
        currentSymbol = '';
        storedValue = '';
        clearInput = true;
        calculatorDisplay.value = '';
      } else {
        addNumber(event.target.innerText);
      }
    }
  }

  function addNumber(number:string) {
    if (clearInput) {
      calculatorDisplay.value = '';
      clearInput = false;
    }
    let tmpNumber:string = calculatorDisplay.value.toString();
    tmpNumber += number;
    console.log(tmpNumber);
    calculatorDisplay.value = tmpNumber;
  }

  function doMath() {
    calculatorDisplay.value = eval(storedValue + currentSymbol + calculatorDisplay.value);
  }

  function addSymbol(symbol:string) {
    clearInput = true;
    if (currentSymbol !== '') {
      doMath();
    }
    currentSymbol = symbol;
    storedValue = calculatorDisplay.value;
  }

  function isSymbol(char:string) {
    const symbols:Array<string> = [ '+', '-', '/', '*'];
    return !!symbols.find((symbol) => symbol === char);
  }
</script>

<template>
  <main>
    <input type="text" :value="calculatorDisplay" disabled="true" />
    <button @click="addInput">1</button>
    <button @click="addInput">2</button>
    <button @click="addInput">3</button>
    <button @click="addInput">4</button>
    <button @click="addInput">5</button>
    <button @click="addInput">6</button>
    <button @click="addInput">7</button>
    <button @click="addInput">8</button>
    <button @click="addInput">9</button>
    <button @click="addInput">0</button>
    <button @click="addInput">.</button>
    <button @click="addInput">+</button>
    <button @click="addInput">-</button>
    <button @click="addInput">/</button>
    <button @click="addInput">*</button>
    <button @click="addInput">=</button>
    <button @click="addInput">C</button>
  </main>
</template>

<style scoped>

</style>
