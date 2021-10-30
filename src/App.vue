<template>
  <div class="container">
    <global-header :user="currentUser"></global-header>
    <validate-form @form-submit="onFormSubmit">
      <div class="mb-3 text-start">
        <label class="form-label">Email</label>
        <validate-input
          :rules="emailRules"
          placeholder="请输入邮箱"
          v-model="emailVal"
          ref="inputRef"
        ></validate-input>
        {{ emailVal }}
      </div>

      <div class="mb-3 text-start">
        <label for="exampleInputPassword">密码</label>
        <validate-input
          type="password"
          class="form-control"
          id="exampleInputPassword"
          placeholder="Password"
        />
      </div>
      <!-- 具名插槽可以缩写为 #submit-->
      <template v-slot:submit>
        <span class="btn btn-danger">Submit</span>
      </template>
    </validate-form>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref } from 'vue'
import 'bootstrap/dist/css/bootstrap.min.css'
import GlobalHeader, { UserProps } from '@/components/GlobalHeader.vue'
import ValidateInput, { RulesProp } from '@/components/ValidateInput.vue'
import ValidateForm from '@/components/ValidateForm.vue'

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
    ValidateForm,
  },
  setup() {
    const emailVal = ref('viking')
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

    const inputRef = ref<any>()
    const onFormSubmit = (result: boolean) => {
      // 可以调子组件的方法
      console.log(inputRef.value.validateInput())
    }
    return {
      currentUser,
      emailRef,
      validateEmail,
      emailRules,
      emailVal,
      onFormSubmit,
      inputRef,
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
