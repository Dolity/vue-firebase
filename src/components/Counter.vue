<script setup>
import { ref, defineProps, onMounted } from "vue"

const counter = ref(0)
const message = "Dolity"

const increaseCounter = () => {
  counter.value += 1
}

defineProps({
  messageText: String,
  changeMessage: Function,
})

onMounted(() => {
  console.log("Counter mounted")
})
</script>

<template>
  <div>Hello {{ messageText }}</div>
  <div>
    <input type="text" v-model="message" />
    <button @click="changeMessage(message)">Change message from counter</button>
  </div>
  <button @click="increaseCounter">Click {{ counter }}</button>
</template>
