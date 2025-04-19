<script setup lang="ts">
  import { ref } from 'vue';

  const calculatorDisplay:{ value:string } = ref('');
  let currentSymbol:string = '';
  let storedValue:string = '';
  let clearInput:boolean = false;


  function addInput(event:MouseEvent<HTMLElement>) {
    const input:string = event.target.innerText;
    if (isMathSymbol(input)) {
      addSymbol(input);
    } else if (input === '=') {
      doMath();
      clearStatus();
    } else if (input === 'C') {
      clearStatus(true);
    } else {
      addNumber(input);
    }
  }

  function addNumber(number:string) {
    if (clearInput) {
      calculatorDisplay.value = '';
      clearInput = false;
    }
    let tmpNumber:string = calculatorDisplay.value.toString();
    tmpNumber += number;
    calculatorDisplay.value = tmpNumber;
  }

  function doMath() {
    calculatorDisplay.value = eval(storedValue + currentSymbol + calculatorDisplay.value);
  }

  function addSymbol(symbol:string) {
    if (currentSymbol !== '') {
      doMath();
    }
    clearInput = true;
    currentSymbol = symbol;
    storedValue = calculatorDisplay.value;
  }

  function isMathSymbol(char:string) {
    const symbols:Array<string> = [ '+', '-', '/', '*'];
    return !!symbols.find((symbol) => symbol === char);
  }

  function clearStatus(clearDisplay:boolean = false) {
    currentSymbol = '';
    storedValue = '';
    clearInput = true;
    calculatorDisplay.value = clearDisplay ?  '' : calculatorDisplay.value;
  }
</script>

<template>
  <main class="flex h-screen justify-center bg-pink-100">
    <div class="w-[200px] mt-10">
      <input class="border-1 w-full rounded text-right pr-[5px] pl-[5px] h-[50px]" type="text" :value="calculatorDisplay" disabled="true" />
      <div class="mt-[5px] grid grid-cols-4 grid-rows-5">
        <button class="hover:bg-gray-200 border-1 rounded h-[30px]" @click="addInput">1</button>
        <button class="hover:bg-gray-200 border-1 rounded h-[30px]" @click="addInput">2</button>
        <button class="hover:bg-gray-200 border-1 rounded h-[30px]" @click="addInput">3</button>
        <button class="hover:bg-gray-200 border-1 rounded h-[30px]" @click="addInput">+</button>
        <button class="hover:bg-gray-200 border-1 rounded h-[30px]" @click="addInput">4</button>
        <button class="hover:bg-gray-200 border-1 rounded h-[30px]" @click="addInput">5</button>
        <button class="hover:bg-gray-200 border-1 rounded h-[30px]" @click="addInput">6</button>
        <button class="hover:bg-gray-200 border-1 rounded h-[30px]" @click="addInput">-</button>
        <button class="hover:bg-gray-200 border-1 rounded h-[30px]" @click="addInput">7</button>
        <button class="hover:bg-gray-200 border-1 rounded h-[30px]" @click="addInput">8</button>
        <button class="hover:bg-gray-200 border-1 rounded h-[30px]" @click="addInput">9</button>
        <button class="hover:bg-gray-200 border-1 rounded h-[30px]" @click="addInput">/</button>
        <button class="hover:bg-gray-200 border-1 rounded h-[30px]" @click="addInput">.</button>
        <button class="hover:bg-gray-200 border-1 rounded h-[30px]" @click="addInput">0</button>
        <button class="hover:bg-gray-200 border-1 rounded h-[30px]" @click="addInput">=</button>
        <button class="hover:bg-gray-200 border-1 rounded h-[30px]" @click="addInput">*</button>
        <button class="hover:bg-gray-200 border-1 rounded h-[30px]" @click="addInput">C</button>
      </div>
    </div>
  </main>
</template>

<style scoped>

</style>
