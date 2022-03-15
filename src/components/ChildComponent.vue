<script setup>
import {ref} from "vue";

const newText = ref('')

// eslint-disable-next-line no-undef
defineProps({
  msg: String
})

// eslint-disable-next-line no-undef
const emit = defineEmits(['response'])

emit('response', 'hello from child')
</script>

<template>
  <h2>A Child Component!</h2>
  <h3>{{ msg || 'No props passed yet' }}</h3>
  <slot>Fallback slot content</slot>
  <textarea v-model="newText" />
  <p>{{newText}}</p>
</template>