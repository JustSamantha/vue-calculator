<script setup lang="ts">
  import { ref } from 'vue';

  const calculatorDisplay:object = ref('');
  let currentSymbol:string = '';
  let storedValue:string = '';
  let clearInput:boolean = false;


  function addInput(event:Event) {
    if (event.target && event.target.innerText) {
      const input:string = event.target.innerText;
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
    <div class="w-[200px]">
      <input class="border-1 w-full rounded text-right pr-[5px] pl-[5px]" type="text" :value="calculatorDisplay" disabled="true" />
      <div class="mt-[5px] grid grid-cols-4 grid-rows-5">
        <button class="bg-gray-100 hover:bg-green-500 border-1 rounded h-[30px]" @click="addInput">1</button>
        <button class="border-1 rounded h-[30px]" @click="addInput">2</button>
        <button class="border-1 rounded h-[30px]" @click="addInput">3</button>
        <button class="border-1 rounded h-[30px]" @click="addInput">+</button>
        <button class="border-1 rounded h-[30px]" @click="addInput">4</button>
        <button class="border-1 rounded h-[30px]" @click="addInput">5</button>
        <button class="border-1 rounded h-[30px]" @click="addInput">6</button>
        <button class="border-1 rounded h-[30px]" @click="addInput">-</button>
        <button class="border-1 rounded h-[30px]" @click="addInput">7</button>
        <button class="border-1 rounded h-[30px]" @click="addInput">8</button>
        <button class="border-1 rounded h-[30px]" @click="addInput">9</button>
        <button class="border-1 rounded h-[30px]" @click="addInput">/</button>
        <button class="border-1 rounded h-[30px]" @click="addInput">.</button>
        <button class="border-1 rounded h-[30px]" @click="addInput">0</button>
        <button class="border-1 rounded h-[30px]" @click="addInput">=</button>
        <button class="border-1 rounded h-[30px]" @click="addInput">*</button>
        <button class="border-1 rounded h-[30px]" @click="addInput">C</button>
      </div>
    </div>
  </main>
</template>

<style scoped>
@import "tailwindcss";

</style>
