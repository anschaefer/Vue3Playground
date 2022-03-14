<script setup>
import {ref, computed} from "vue";

const count = ref(0)
const text = ref('')
const awesome = ref(true);

let id = 0

const newTodo = ref('')
const hideCompleted = ref(false)
const todos = ref([
  { id: id++, text: 'Learn HTML', done: true },
  { id: id++, text: 'Learn JavaScript', done: true },
  { id: id++, text: 'Learn Vue', done: false }
])

const filteredTodos = computed(() => {
  return hideCompleted.value ? todos.value.filter((t) => !t.done) : todos.value
})

function increment() {
  count.value++
}
function onInput(input) {
  text.value = input.target.value
}
function toggle() {
  awesome.value = !awesome.value
}
function addTodo() {
  todos.value.push( {id: id++, text: newTodo.value} )
  newTodo.value = ''
}
function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t != todo)
}
</script>

<template>
  <div class="toggleText">
    <h1 v-if="awesome" v-on:click="toggle">Vue is awesome</h1>
    <h2 v-else v-on:click="toggle">Not so much</h2>
  </div>

  <div class="input">
    <h2>Inputs and Buttons</h2>
    <input v-bind:value="text" @input="onInput" placeholder="Edit button label here">
    <button @click="increment">{{ text }}: {{count}}</button>
  </div>

  <div class="TodoList">
    <h2>Todo List Example</h2>
    <input v-model="newTodo" @keyup.enter="addTodo" />
    <button @click="addTodo">Add Todo</button>
    <ul>
      <li v-for="todo in filteredTodos" :key="todo.id">
        <input type="checkbox" v-model="todo.done" />
        <span :class="{ done: todo.done}">{{ todo.text }}</span>
        <button @click="removeTodo(todo)">X</button>
      </li>
    </ul>
    <button @click="hideCompleted = !hideCompleted">
      {{ hideCompleted ? 'Show all' : 'Hide completed' }}
    </button>
  </div>
</template>

<style>
.done {
  text-decoration: line-through;
}
</style>