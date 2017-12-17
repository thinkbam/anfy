<template>
  <div class="ayfy-home">
    <div class="ayfu-header">
      <!--<mt-header title="在线题库"></mt-header>-->
      <div tabindex="Department" v-on:click="itemClick($event)">科室列表</div>
      <div tabindex="Search" v-on:click="itemClick($event)">在线搜索</div>
      <div tabindex="OnlineExam" v-on:click="itemClick($event)">在线考试</div>
    </div>
    <div class="ayfy-container">
      <Department v-if="renderComponents == 'Department'"></Department>
      <Search v-else-if="renderComponents == 'Search'"></Search>
    </div>
    <!--<div class="ayfy-footer">-->
      <!--<div tabindex="Department" v-on:click="itemClick($event)">科室列表</div>-->
      <!--<div tabindex="Search" v-on:click="itemClick($event)">在线搜索</div>-->
      <!--<div tabindex="OnlineExam" v-on:click="itemClick($event)">在线考试</div>-->
    <!--</div>-->
  </div>
</template>

<script>
  import Vue from 'vue'
  import Mint from 'mint-ui'
  import Search from './Search'
  import Department from './Department'

  Vue.use(Mint)
  export default {
    name: 'home',
    components: {
      Search, Department
    },
    data: function () {
      return {
        renderComponents: {
          type: String,
          default: 'Department'
        }
      }
    },
    methods: {
      itemClick: function (e) {
        let tabindex = e.target.getAttribute('tabindex')
        switch (tabindex) {
          case 'Department':
            this.renderComponents = 'Department'
            break
          case 'Search':
            this.renderComponents = 'Search'
            break
          case 'OnlineExam':
            // this.renderComponents = 'OnlineExam'
            Mint.MessageBox('温馨提示', '未完待续...')
            break
          default:
            this.rendeComponents = 'Department'
        }
      }
    },
    created () {
      // 设置默认渲染组件（PS：设定默认值貌似不行？）
      this.renderComponents = 'Department'
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
  }

  .ayfy-container {
    -webkit-overflow-scrolling: touch;
    -webkit-box-flex: 1;
    -moz-box-flex: 1;
    box-flex: 1;
    overflow: scroll;
  }

  .ayfu-header {
    display: -webkit-box;
    display: -moz-box;
    display: box;
    height: 40px;
  }

  .ayfu-header div {
    -webkit-box-flex: 1;
    -moz-box-flex: 1;
    box-flex: 1;
    text-align: center;
    line-height: 40px;
    background-color: #26A2FF;
    color: #ffffff;
  }
</style>
