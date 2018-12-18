<template>
  <div id="app" class="hello">
      <h1>{{ msg }}</h1>
      <h2>登录</h2>
      <el-row>
      <el-form :label-position="labelPosition" label-width="80px" :model="formLabelAlign">
        <el-row :gutter="20">
          <el-col :span="12" :offset="6">
            <div class="grid-content bg-purple">
              <el-form-item label="账号：">
                <el-input v-model="formLabelAlign.userName"></el-input>
              </el-form-item>
            </div>
          </el-col>
        </el-row>
        <el-row :gutter="20">
          <el-col :span="12" :offset="6">
            <div class="grid-content bg-purple">
              <el-form-item label="密码：">
                <el-input type="password" v-model="formLabelAlign.userPassword"></el-input>
              </el-form-item>
            </div>
          </el-col>
        </el-row>
      </el-form>
      </el-row>
      <el-button v-on:click="getTest">登录</el-button>
    </div>
</template>

<script>
import axios from 'axios'
// import qs from 'qs'
// 方法命名不规范，仅做Demo
export default {
  name: 'App',
  data () {
    return {
      msg: 'sharing books',
      labelPosition: 'right',
      formLabelAlign: {
        userName: '',
        userPassword: ''
      }
    }
  },
  methods: {
    getTest () {
      console.log(this.formLabelAlign)
      let userName = this.formLabelAlign.userName
      let userPassword = this.formLabelAlign.userPassword
      if (userName !== '' && userPassword !== '') {
        axios({
          method: 'POST',
          url: 'sysUser/login',
          data: {
            'userName': this.formLabelAlign.userName,
            'userPassword': this.formLabelAlign.userPassword
          }})
          // data: qs.stringify({
          //   'userName': this.formLabelAlign.userName,
          //   'userPassword': this.formLabelAlign.userPassword
          // })})
          .then(function (response) {
            console.log(1)
            console.log(response)
          })
          .catch(function (error) {
            console.log(error)
          })
      }
    }

  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
