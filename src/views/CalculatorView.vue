<!-- <template>
  <div class="about">
    <h1>This is an about page</h1>
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>


 -->

<script setup lang="ts">
import { ref } from 'vue'

const calculatorDisplay: { value: string } = ref('')
const buttons: Array<string> = [
  '1',
  '2',
  '3',
  '+',
  '4',
  '5',
  '6',
  '-',
  '7',
  '8',
  '9',
  '/',
  '.',
  '0',
  '=',
  '*',
  'C',
]
let currentSymbol: string = ''
let storedValue: string = ''
let clearInput: boolean = false

function addInput(input: string) {
  if (isMathSymbol(input)) {
    addSymbol(input)
  } else if (input === '=') {
    doMath()
    clearStatus()
  } else if (input === 'C') {
    clearStatus(true)
  } else {
    addNumber(input)
  }
}

function addNumber(number: string) {
  if (clearInput) {
    calculatorDisplay.value = ''
    clearInput = false
  }
  let tmpNumber: string = calculatorDisplay.value.toString()
  tmpNumber += number
  calculatorDisplay.value = tmpNumber
}

function doMath() {
  calculatorDisplay.value = eval(storedValue + currentSymbol + calculatorDisplay.value)
}

function addSymbol(symbol: string) {
  if (currentSymbol !== '') {
    doMath()
  }
  clearInput = true
  currentSymbol = symbol
  storedValue = calculatorDisplay.value
}

function isMathSymbol(char: string) {
  const symbols: Array<string> = ['+', '-', '/', '*']
  return !!symbols.find((symbol) => symbol === char)
}

function clearStatus(clearDisplay: boolean = false) {
  currentSymbol = ''
  storedValue = ''
  clearInput = true
  calculatorDisplay.value = clearDisplay ? '' : calculatorDisplay.value
}
</script>

<template>
  <div class="flex h-screen justify-center bg-pink-100">
    <div class="w-[200px] mt-10">
      <input
        class="border-1 w-full rounded text-right pr-[5px] pl-[5px] h-[50px]"
        type="text"
        :value="calculatorDisplay"
        disabled="true"
      />
      <div class="mt-[5px] grid grid-cols-4 grid-rows-5">
        <button
          v-for="x in buttons"
          :key="x"
          class="hover:bg-pink-200 border-1 rounded h-[30px]"
          @click="addInput(x)"
        >
          {{ x }}
        </button>
      </div>
    </div>
  </div>
</template>
