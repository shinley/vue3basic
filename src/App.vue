<template>
  <div class="container">
    <global-header :user="currentUser"></global-header>
    <form action="">
      <div class="mb-3 text-start">
        <label class="form-label">Email</label>
        <validate-input :rules="emailRules"></validate-input>
      </div>
      <div class="mb-3 text-start">
        <label for="exampleInputEmail" class="form-lable">邮箱地址</label>
        <input
          type="email"
          class="form-control"
          id="exampleInputEmail"
          placeholder="name@example.com"
          v-model="emailRef.val"
          @blur="validateEmail"
        />
        <div class="form-text text-start" v-if="emailRef.error">
          {{ emailRef.message }}
        </div>
      </div>
      <div class="mb-3 text-start">
        <label for="exampleInputPassword">Password</label>
        <input
          type="password"
          class="form-control"
          id="exampleInputPassword"
          placeholder="Password"
        />
      </div>
    </form>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive } from 'vue'
import 'bootstrap/dist/css/bootstrap.min.css'
import GlobalHeader, { UserProps } from '@/components/GlobalHeader.vue'
import ValidateInput, { RulesProp } from '@/components/ValidateInput.vue'

const currentUser: UserProps = {
  id: 1,
  name: 'shinley',
  isLogin: true,
}
const emailReg =
  /^[a-zA-Z0-9.!#$%&’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$/
export default defineComponent({
  name: 'App',
  components: {
    GlobalHeader,
    ValidateInput,
  },
  setup() {
    const emailRules: RulesProp = [
      {
        type: 'required',
        message: '邮箱地址不能为空',
      },
      {
        type: 'email',
        message: '请输入正确的电子邮箱格式',
      },
    ]
    const emailRef = reactive({
      val: '',
      error: false,
      message: '',
    })
    const validateEmail = () => {
      emailRef.error = false
      if (emailRef.val.trim() === '') {
        emailRef.error = true
        emailRef.message = 'can not be empty'
      } else if (!emailReg.test(emailRef.val)) {
        emailRef.error = true
        emailRef.message = 'should be valid email'
      }
    }
    return {
      currentUser,
      emailRef,
      validateEmail,
      emailRules,
    }
  },
})
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
