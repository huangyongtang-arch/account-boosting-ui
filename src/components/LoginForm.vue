<script setup lang="ts">
import { ref } from 'vue'

const emit = defineEmits(['switchForm'])

const phoneNumber = ref('')
const verificationCode = ref('')
const agreedToTerms = ref(false)

const sendCode = () => {
  console.log('Sending code to:', phoneNumber.value)
}

const handleLogin = () => {
  console.log('Logging in with:', phoneNumber.value, verificationCode.value)
}
</script>

<template>
  <div class="login-container">
    <h1 class="title">验证码登录</h1>
    
    <div class="form-container">
      <div class="input-group">
        <input 
          type="text" 
          v-model="phoneNumber" 
          placeholder="请输入手机号"
          class="phone-input"
        >
      </div>
      
      <div class="input-group verification">
        <input 
          type="text" 
          v-model="verificationCode" 
          placeholder="校验码"
          class="code-input"
        >
        <button @click="sendCode" class="send-code-btn">发送验证码</button>
      </div>

      <div class="links">
        <a href="#" class="link" @click.prevent="emit('switchForm', 'password-login')">账号密码登录</a>
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
        :disabled="!phoneNumber || !verificationCode || !agreedToTerms"
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

.phone-input,
.code-input {
  width: 100%;
  padding: 0.8rem 1rem;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  font-size: 1rem;
  background-color: #f8f8f8;
}

.verification {
  display: flex;
  gap: 0.5rem;
}

.code-input {
  flex: 1;
}

.send-code-btn {
  white-space: nowrap;
  padding: 0 1rem;
  color: #4CAF50;
  background: none;
  border: none;
  font-size: 0.9rem;
  cursor: pointer;
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