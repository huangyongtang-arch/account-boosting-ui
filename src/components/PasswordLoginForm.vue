<script setup lang="ts">
import { ref } from 'vue'

const emit = defineEmits(['switchForm'])

const phoneNumber = ref('')
const password = ref('')
const agreedToTerms = ref(false)

const handleLogin = () => {
  console.log('Logging in with:', phoneNumber.value, password.value)
}
</script>

<template>
  <div class="login-container">
    <h1 class="title">账号密码登录</h1>
    
    <div class="form-container">
      <div class="input-group">
        <input 
          type="text" 
          v-model="phoneNumber" 
          placeholder="请输入手机号"
          class="input"
        >
      </div>
      
      <div class="input-group">
        <input 
          type="password" 
          v-model="password" 
          placeholder="请输入密码"
          class="input"
        >
      </div>

      <div class="links">
        <a href="#" class="link" @click.prevent="emit('switchForm', 'code-login')">验证码登录</a>
        <a href="#" class="link" @click.prevent="emit('switchForm', 'register')">账号密码注册</a>
      </div>

      <div class="terms">
        <label class="checkbox-container">
          <input 
            type="checkbox" 
            v-model="agreedToTerms"
          >
          <span>我已阅读并同意</span>
          <a href="#" class="terms-link">《猛花APP隐私保护指引》</a>
        </label>
      </div>

      <button 
        @click="handleLogin" 
        class="login-btn"
        :disabled="!phoneNumber || !password || !agreedToTerms"
      >
        登录
      </button>
    </div>
  </div>
</template>

<style scoped>
.login-container {
  width: 100%;
  max-width: 400px;
  padding: 2rem;
  text-align: center;
}

.title {
  font-size: 1.5rem;
  color: #333;
  margin-bottom: 2rem;
}

.form-container {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.input-group {
  position: relative;
  margin-bottom: 1rem;
}

.input {
  width: 100%;
  padding: 0.8rem 1rem;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  font-size: 1rem;
  background-color: #f8f8f8;
}

.links {
  display: flex;
  justify-content: space-between;
  margin: 1rem 0;
}

.link {
  color: #4CAF50;
  text-decoration: none;
  font-size: 0.9rem;
}

.terms {
  margin: 1rem 0;
  text-align: left;
}

.checkbox-container {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 0.9rem;
  color: #666;
}

.terms-link {
  color: #4CAF50;
  text-decoration: none;
}

.login-btn {
  width: 100%;
  padding: 1rem;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 25px;
  font-size: 1rem;
  cursor: pointer;
  transition: background-color 0.3s;
}

.login-btn:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}
</style>