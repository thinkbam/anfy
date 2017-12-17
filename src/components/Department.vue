<template>
  <div class="ayfy-department">
      <ul>
        <li  v-for="department, index in departments">
          {{index+1}}. {{department.chinaName}}
        </li>
      </ul>
  </div>
</template>

<script>
  import Vue from 'vue'
  import axios from 'axios'
  import Mint from 'mint-ui'

  Vue.use(Mint)
  export default {
    name: 'department',
    data: function () {
      return {
        departments: {
          type: Array,
          default: Array.of()
        }
      }
    },
    methods: {
      /**
       * 获取部门列表
       */
      getDepartments: function () {
        axios.get('static/data/department.json').then(response => {
          this.departments = response.data.departments
        }).catch(error => {
          Mint.MessageBox('温馨提示', error)
        })
      }
    },
    created () {
      // 初始化部门列表
      this.getDepartments()
    }
  }
</script>

<style scoped>
  .ayfy-department ul li {
    height: 36px;
    line-height:36px;
    padding-left: 10px;
    border: 1px solid whitesmoke;
  }
</style>

