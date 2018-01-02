<template>
  <div>
    <mt-header title="应用授权"></mt-header>
    <div class="verify">
      <input type="text" placeholder="请输入授权码" v-model="isVerify">
      <button @click="verify"> 确认</button>
    </div>
  </div>
</template>

<script>
  import Vue from 'vue'
  // import axios from 'axios'
  import Mint from 'mint-ui'

  Vue.use(Mint)
  // http://pv.sohu.com/cityjson?ie=utf-8
  export default {
    name: 'verify',
    data: function () {
      return {
        isVerify: '',
        grandCode: ['n9116'],
        errorCount: 0
      }
    },
    methods: {
      verify: function () {
        if (sessionStorage.getItem('errorCount') >= 2) {
          Mint.MessageBox('您的设备已拉入黑名单')
          return
        }
        let verify = this.isVerify
        if (verify === null || verify === '' || verify === undefined) {
          Mint.MessageBox('请输入授权码')
          return
        }
        let isValid = this.grandCode.indexOf(verify)
        if (isValid === -1) {
          sessionStorage.setItem('errorCount', this.errorCount++)
          Mint.MessageBox('授权码错误')
          return
        }
        // 抛事件
        this.$emit('verifyEvent', true)
      }
    },
    counted () {
      // axios.get('http://pv.sohu.com/cityjson?ie=utf-8').then(response => {
      //   console.log('response-->', response)
      // }).catch(function (error) {
      //   Mint.MessageBox('温馨提示', error)
      // })
    }
  }
</script>

<style scoped>
  .verify {
    margin-top: 40px;
    text-align: center;
  }

  .verify input {
    height: 36px;
    width: 60%;
  }

  .verify button {
    border-radius: 5px;
    height: 42px;
    line-height: inherit;
    background-color: #26a2ff;
    width: 20%;
  }
</style>
