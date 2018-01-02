<template>
  <div id="app">
    <Search v-show="isVerify"></Search>
    <Verify v-show="!isVerify" @verifyEvent="onVerify"></Verify>
  </div>
</template>

<script>
  import Search from './components/Search'
  import Verify from './components/Verify'

  export default {
    name: 'app',
    components: {
      Search, Verify
    },
    data: function () {
      return {
        isVerify: ''
      }
    },
    methods: {
      onVerify: function (v) {
        this.isVerify = v
      }
    }
  }
</script>

<style>
  *, *::after, *::before {
    margin: 0px;
    padding: 0px;
    -webkit-tap-highlight-color: transparent;
    -webkit-input-placeholder-color: transparent;
    -webkit-overflow-scrolling: touch;
  }

  body {
    -moz-user-select: none;
    -webkit-user-select: none;
    -ms-user-select: none;
    -khtml-user-select: none;
    user-select: none;
    -ms-touch-action: none;
    color: #676767;
    font-size: 14px;
  }

  /**
   * 不显示Scrollbar
   */
  ::-webkit-scrollbar {
    display: none;
    width: 0;
  }
</style>
