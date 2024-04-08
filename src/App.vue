<script setup>
import { ref, computed, onMounted, watch } from "vue"
const isLoading = ref(false)
const isUpdated = ref(false)
const isValid = ref(false)

const firstname = ref("")
const lastname = ref("")
const email = ref("")
const errors = ref({})

const fullname = computed(() => {
  return `${firstname.value} ${lastname.value}`
})

// simulate fetching data from API
onMounted(() => {
  firstname.value = "Fname"
  lastname.value = "Lname"
  email.value = "test@gmail.com"
})

// simulate fetching data from API with condition
const updateProfile = async () => {
  isLoading.value = true
  await new Promise((resolve) => setTimeout(resolve, 2000))
  isLoading.value = false
  isUpdated.value = true
}

// validate name
const validateName = (name) => {
  const re = /\d/
  return !re.test(name)
}

// validate email
const validateEmail = (email) => {
  return email.includes("@")
}

// watch for changes in value and validate with function
watch([firstname, lastname, email], () => {
  isValid.value = true
  isUpdated.value = false
  errors.value = {}

  if (!validateName(firstname.value)) {
    isValid.value = false
    errors.value.firstname = "Firstname not valid"
  }

  if (!validateName(lastname.value)) {
    isValid.value = false
    errors.value.lastname = "Lastname not valid"
  }

  if (!validateEmail(email.value)) {
    isValid.value = false
    errors.value.email = "Email not valid"
  }
})
</script>

<template>
  <div class="container">
    <div>
      <div>Fullname: {{ fullname }}</div>
      <div>Email: {{ email }}</div>
    </div>
    <div>
      <div>Firstname:</div>
      <input type="text" v-model="firstname" />
    </div>
    <div class="error">
      {{ errors.firstname }}
    </div>
    <div>
      <div>Lastname:</div>
      <input type="text" v-model="lastname" />
    </div>
    <div class="error">
      {{ errors.lastname }}
    </div>
    <div>
      <div>Email:</div>
      <input type="text" v-model="email" />
    </div>
    <div class="error">
      {{ errors.email }}
    </div>
    <div class="loading" v-if="isLoading">Loading...</div>
    <button :disabled="!isValid" class="button" @click="updateProfile()">
      Update profile
    </button>
    <div v-if="isUpdated">Profile updated</div>
  </div>
</template>

<style>
.container {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  max-width: 320px;
  margin: 0 auto;
}

.container > div {
  width: 100%;
}

.button {
  width: 100%;
  height: 24px;
  margin-top: 20px;
}

.loading {
  background-color: aliceblue;
  width: 100%;
  padding: 20px;
  box-sizing: border-box;
  margin: 10px 0;
}

input {
  width: 100%;
}

.error {
  color: red;
}
</style>
