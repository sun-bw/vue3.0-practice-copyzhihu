<template>
  <div class="container">
    <global-header :user="currentUser"></global-header>
    <!-- <column-list :list="list"></column-list> -->
    <form action="">
      <div class="mb-3">
        <label class="form-label">邮箱地址</label>
        <validate-input :rules="emailRules"></validate-input>
      </div>
      <div class="mb-3">
        <label for="exampleInoutEmail1" class="form-label">邮箱地址</label>
        <input 
          type="email"  class="form-control" id="exampleInputEmail1"
          v-model="emailRef.val"
          @blur="validateEmail"
        >
        <div class="form-text" v-if="emailRef.error">{{emailRef.message}}</div>
      </div>
      <div class="mb-3">
        <label for="exampleInputPassword1" class="form-label">密码</label>
        <input type="password" class="form-control" id="exampleInputPassword">
      </div>
    </form>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive } from 'vue';
import 'bootstrap/dist/css/bootstrap.min.css'
// import ColumnList, { ColumnProps } from './components/ColumnList.vue'
import GlobalHeader, { UserProps } from './components/GloballHeader.vue'
import validateInput, { RulesProp } from './components/ValidateInput.vue'
const currentUser: UserProps = {
  isLogin: true,
  name: '温言'
}
// const testData: ColumnProps[] = [
//   {
//     id: 1,
//     title: 'test1的专栏',
//     description: '这是test1的专刊',
//     avatat: '',
//   },
//   {
//     id: 2,
//     title: 'test1的专栏',
//     description: '这是test1的专刊',
//     avatat: '',
//   }
// ]
const emailReg = /^[a-zA-Z0-9.!#$%&’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$/
export default defineComponent({
  name: 'App',
  components: {
    // ColumnList,
    GlobalHeader,
    validateInput
  },
  setup() {
    const emailRules: RulesProp = [
      { type: 'required', message: '电子邮箱地址不能为空'},
      { type: 'email', message: '请输入正确的电子邮箱格式'}
    ]
    const emailRef = reactive({
      val: '',
      error: false,
      message: '',
    })
    const validateEmail = () => {
      if(emailRef.val.trim() === '') {
        emailRef.error = true
        emailRef.message = 'can not be empty'
      } else if(!emailReg.test(emailRef.val)) {
        emailRef.error = true
        emailRef.message = 'should be valid email'
      }
    }
    return {
      // list: testData,
      currentUser,
      emailRef,
      validateEmail,
      emailRules
    }
  }
});
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
