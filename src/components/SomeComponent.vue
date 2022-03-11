<script setup>
import {ref} from "vue";

const count = ref(0)
const text = ref('Label')
const awesome = ref(true);

function increment() {
  count.value++
}
function onInput(input) {
  text.value = input.target.value
}
function toggle() {
  awesome.value = !awesome.value
}
</script>

<template>
  <h1 v-if="awesome" v-on:click="toggle">Vue is awesome</h1>
  <h2 v-else v-on:click="toggle">Not so much</h2>
  <div class="input">
    <input v-bind:value="text" @input="onInput" placeholder="Edit button label here">
  </div>
  <div class="counter">
    <button @click="increment">{{ text }}: {{count}}</button>
  </div>
</template>