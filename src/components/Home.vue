<template>
  <div class="ayfy-home">
    <div class="ayfu-header">
      <mt-header title="在线题库"></mt-header>
    </div>
    <div class="ayfy-container">
      <ul v-for="item in 100">
        <li>{{item}}</li>
      </ul>
    </div>
    <div class="ayfy-footer">
      <div>科室列表</div>
      <div>在线搜索</div>
      <div>在线考试</div>
    </div>
  </div>
</template>

<script>
  import Vue from 'vue'
  import axios from 'axios'
  import Mint from 'mint-ui'

  Vue.use(Mint)
  export default {
    name: 'home',
    data: function () {
      return {
        selected: {
          type: Number,
          default: 1
        },
        departments: {
          type: Array,
          default: Array.of()
        }
      }
    },
    methods: {
      itemClick: function () {
        alert('1111')
      }
    },
    created () {
      axios.get('static/data/department.json').then(response => {
        console.log('home response->', response)
        this.departments = response.data.departments
      }).catch(error => {
        Mint.MessageBox('提示', error)
      })
    }
  }
</script>

<style scoped>

  .ayfy-home {
    display: -webkit-box;
    display: -moz-box;
    display: box;
    -webkit-box-orient: vertical;
    -moz-box-orient: vertical;
    box-orient: vertical;
    height: 100vh;
  }

  .ayfu-header {
    height: 40px;
    border: 1px solid red;
  }
  .ayfy-container {
    -webkit-overflow-scrolling: touch;
    -webkit-box-flex: 1;
    -moz-box-flex: 1;
    box-flex: 1;
    overflow: scroll;
    border: 1px solid darkgreen;
  }

  .ayfy-footer {
    display: -webkit-box;
    display: -moz-box;
    display: box;
    height: 40px;
    /*border: 1px solid blue;*/
  }
  .ayfy-footer div{
    -webkit-box-flex: 1;
    -moz-box-flex: 1;
    box-flex: 1;
    text-align: center;
    line-height: 40px;
    background-color: #26A2FF;
    color: #ffffff;
    /*border: 1px solid forestgreen;*/
  }
</style>
