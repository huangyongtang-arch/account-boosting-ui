<script setup lang="ts">
import { ref, computed } from 'vue'

const emit = defineEmits(['switchForm'])

const username = ref('')
const password = ref('')
const confirmPassword = ref('')
const phoneNumber = ref('')
const verificationCode = ref('')
const agreedToTerms = ref(false)

const errors = ref({
  username: '',
  password: '',
  confirmPassword: '',
  phoneNumber: '',
  verificationCode: ''
})

const validateUsername = () => {
  if (username.value.length < 3) {
    errors.value.username = '用户名至少需要3个字符'
    return false
  }
  errors.value.username = ''
  return true
}

const validatePassword = () => {
  if (password.value.length < 6) {
    errors.value.password = '密码至少需要6个字符'
    return false
  }
  errors.value.password = ''
  return true
}

const validateConfirmPassword = () => {
  if (confirmPassword.value !== password.value) {
    errors.value.confirmPassword = '两次输入的密码不一致'
    return false
  }
  errors.value.confirmPassword = ''
  return true
}

const validatePhone = () => {
  const phoneRegex = /^1[3-9]\d{9}$/
  if (!phoneRegex.test(phoneNumber.value)) {
    errors.value.phoneNumber = '请输入有效的手机号码'
    return false
  }
  errors.value.phoneNumber = ''
  return true
}

const isFormValid = computed(() => {
  return username.value &&
    password.value &&
    confirmPassword.value &&
    phoneNumber.value &&
    verificationCode.value &&
    agreedToTerms.value &&
    !Object.values(errors.value).some(error => error !== '')
})

const sendCode = () => {
  if (validatePhone()) {
    console.log('Sending code to:', phoneNumber.value)
  }
}

const handleRegister = () => {
  const isValid = validateUsername() &&
    validatePassword() &&
    validateConfirmPassword() &&
    validatePhone()

  if (isValid) {
    console.log('Registering:', {
      username: username.value,
      password: password.value,
      phoneNumber: phoneNumber.value,
      verificationCode: verificationCode.value
    })
  }
}
</script>

<template>
  <div class="register-container">
    <h1 class="title">账号注册</h1>
    
    <div class="form-container">
      <div class="input-group">
        <input 
          type="text" 
          v-model="username" 
          @blur="validateUsername"
          placeholder="请输入用户名"
          class="input"
        >
        <span class="error-message" v-if="errors.username">{{ errors.username }}</span>
      </div>

      <div class="input-group">
        <input 
          type="password" 
          v-model="password" 
          @blur="validatePassword"
          placeholder="请输入密码"
          class="input"
        >
        <span class="error-message" v-if="errors.password">{{ errors.password }}</span>
      </div>

      <div class="input-group">
        <input 
          type="password" 
          v-model="confirmPassword" 
          @blur="validateConfirmPassword"
          placeholder="请确认密码"
          class="input"
        >
        <span class="error-message" v-if="errors.confirmPassword">{{ errors.confirmPassword }}</span>
      </div>

      <div class="input-group">
        <input 
          type="text" 
          v-model="phoneNumber" 
          @blur="validatePhone"
          placeholder="请输入手机号"
          class="input"
        >
        <span class="error-message" v-if="errors.phoneNumber">{{ errors.phoneNumber }}</span>
      </div>
      
      <div class="input-group verification">
        <input 
          type="text" 
          v-model="verificationCode" 
          placeholder="验证码"
          class="code-input"
        >
        <button 
          @click="sendCode" 
          class="send-code-btn"
          :disabled="!phoneNumber || errors.phoneNumber"
        >
          发送验证码
        </button>
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
        @click="handleRegister" 
        class="register-btn"
        :disabled="!isFormValid"
      >
        注册
      </button>

      <div class="login-link">
        已有账号？<a href="#" class="link" @click.prevent="emit('switchForm', 'code-login')">立即登录</a>
      </div>
    </div>
  </div>
</template>

<style scoped>
.register-container {
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

.input,
.code-input {
  width: 100%;
  padding: 0.8rem 1rem;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  font-size: 1rem;
  background-color: #f8f8f8;
}

.error-message {
  position: absolute;
  left: 0;
  bottom: -1.5rem;
  color: #ff4d4f;
  font-size: 0.8rem;
  text-align: left;
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

.send-code-btn:disabled {
  color: #ccc;
  cursor: not-allowed;
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

.register-btn {
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

.register-btn:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}

.login-link {
  margin-top: 1rem;
  font-size: 0.9rem;
  color: #666;
}

.link {
  color: #4CAF50;
  text-decoration: none;
  margin-left: 0.5rem;
}
</style>