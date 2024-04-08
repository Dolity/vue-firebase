<script setup>
import { computed, reactive, ref, watch, watchEffect } from "vue"

const formData = reactive({
  firstname: "",
  lastname: "",
})

const fullname = ref("")

watchEffect(() => {
  fullname.value = `${formData.firstname} ${formData.lastname}`
  console.log("formData watchEffect fullname changed", formData)
})

watch(
  fullname,
  (newVal, oldVal) => {
    console.log("formData watch fullname changed", formData)
  },
  { immediate: true }
)
</script>

<template>
  <div>
    <div>Fullname: {{ fullname }}</div>
    <input type="text" v-model="formData.firstname" />
    <input type="text" v-model="formData.lastname" />
  </div>
</template>
