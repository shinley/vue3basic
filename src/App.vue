<template>
  <div class="container">
    <global-header :user="currentUser"></global-header>
    <router-view></router-view>
    <footer class="text-center py-4 text-secondary bg-light mt-6">
      <small>
        <ul class="list-inline mb-0">
          <li>@2020者也专栏</li>
          <li>课程</li>
          <li>文档</li>
          <li>联系</li>
          <li>更多</li>
        </ul>
      </small>
    </footer>
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
      console.log('校验结果', result)
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
