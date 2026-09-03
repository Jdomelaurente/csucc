<template>
  <div class="page">
    <div class="form-box">
      <div class="school-name">CSUCC</div>
      <h2>Create Account</h2>

      <form @submit.prevent="handleRegister">
        <div class="field">
          <label for="firstname">First Name</label>
          <input id="firstname" v-model="form.firstName" type="text" placeholder="Enter first name" required />
        </div>

        <div class="field">
          <label for="lastname">Last Name</label>
          <input id="lastname" v-model="form.lastName" type="text" placeholder="Enter last name" required />
        </div>

        <div class="field">
          <label for="email">Email</label>
          <input id="email" v-model="form.email" type="email" placeholder="Enter your email" required />
        </div>

        <div class="field">
          <label for="student-id">Student ID</label>
          <input id="student-id" v-model="form.studentId" type="text" placeholder="e.g. 2024-00001" required />
        </div>

        <div class="field">
          <label for="password">Password</label>
          <input id="password" v-model="form.password" type="password" placeholder="Enter password" required />
        </div>

        <div class="field">
          <label for="confirm">Confirm Password</label>
          <input id="confirm" v-model="form.confirm" type="password" placeholder="Re-enter password" required />
          <span class="error" v-if="form.confirm && form.confirm !== form.password">Passwords do not match.</span>
        </div>

        <button
          type="submit"
          class="btn-submit"
          :disabled="isLoading || form.password !== form.confirm"
        >
          {{ isLoading ? 'Registering...' : 'Register' }}
        </button>
      </form>

      <p class="switch-text">
        Already have an account? <router-link to="/login">Login here</router-link>
      </p>
      <p class="back-link"><router-link to="/">← Back to home</router-link></p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const isLoading = ref(false)
const form = ref({
  firstName: '',
  lastName: '',
  email: '',
  studentId: '',
  password: '',
  confirm: '',
})

async function handleRegister() {
  if (form.value.password !== form.value.confirm) return
  isLoading.value = true
  await new Promise(r => setTimeout(r, 800))
  isLoading.value = false
  alert('Register will connect to the backend.')
}
</script>

<style scoped>
* { box-sizing: border-box; margin: 0; padding: 0; }

.page {
  font-family: Arial, sans-serif;
  background: #f2f2f2;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
}

.form-box {
  background: #fff;
  border: 1px solid #ccc;
  border-radius: 6px;
  padding: 36px 32px;
  width: 100%;
  max-width: 400px;
}

.school-name {
  text-align: center;
  font-size: 22px;
  font-weight: bold;
  color: #1a4a8a;
  margin-bottom: 4px;
  letter-spacing: 1px;
}

h2 {
  text-align: center;
  font-size: 18px;
  font-weight: normal;
  color: #333;
  margin-bottom: 24px;
}

.field {
  margin-bottom: 14px;
}

.field label {
  display: block;
  font-size: 14px;
  margin-bottom: 5px;
  color: #444;
}

.field input {
  width: 100%;
  padding: 8px 10px;
  font-size: 14px;
  border: 1px solid #bbb;
  border-radius: 4px;
  outline: none;
  font-family: Arial, sans-serif;
}

.field input:focus {
  border-color: #1a4a8a;
}

.error {
  display: block;
  font-size: 12px;
  color: #c0392b;
  margin-top: 4px;
}

.btn-submit {
  width: 100%;
  padding: 10px;
  background: #1a4a8a;
  color: #fff;
  font-size: 15px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  margin-top: 6px;
  font-family: Arial, sans-serif;
}

.btn-submit:hover:not(:disabled) { background: #153d73; }
.btn-submit:disabled { opacity: 0.5; cursor: default; }

.switch-text {
  text-align: center;
  font-size: 13px;
  color: #555;
  margin-top: 18px;
}

.switch-text a, .back-link a {
  color: #1a4a8a;
  text-decoration: none;
}
.switch-text a:hover, .back-link a:hover { text-decoration: underline; }

.back-link {
  text-align: center;
  margin-top: 10px;
  font-size: 13px;
}
</style>
