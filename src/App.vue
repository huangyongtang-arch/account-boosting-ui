<script setup lang="ts">
import { ref } from 'vue'
import LoginForm from './components/LoginForm.vue'
import RegisterForm from './components/RegisterForm.vue'
import PasswordLoginForm from './components/PasswordLoginForm.vue'

const currentForm = ref('code-login') // 'code-login' | 'password-login' | 'register'

const switchForm = (formName: string) => {
  currentForm.value = formName
}
</script>

<template>
  <div class="app-container">
    <component 
      :is="currentForm === 'register' 
        ? RegisterForm 
        : currentForm === 'password-login'
        ? PasswordLoginForm
        : LoginForm" 
      @switch-form="switchForm" 
    />
  </div>
</template>

<style>
.app-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background-color: #fff;
}
</style>