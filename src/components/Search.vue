<template>
  <div>
    <div class="anfy-online-search">
      <mt-header title="在线题库"></mt-header>
      <mt-search v-model="search" cancel-text="取消" placeholder="请输入关键字"></mt-search>
    </div>
    <div class="clear"></div>
    <div class="result" v-for="result,index in searchResults">
      <div v-show="result.options == ''">
        <div class="question">{{index+1}}.{{result.question}}</div>
      </div>
      <div v-show="result.options != ''">
        <div class="question">
          {{index+1}}.{{result.question}}（<span>{{result.answer}}</span>）
        </div>
        <div class="options">{{result.options}}</div>
      </div>
    </div>
  </div>
</template>

<script>
  import Vue from 'vue'
  import axios from 'axios'
  import Mint from 'mint-ui'

  Vue.use(Mint)
  export default {
    name: 'search',
    data: function () {
      return {
        search: '',
        searchLibrary: Array.of()
      }
    },
    computed: {
      searchResults: function () {
        var search = this.search
        if (search) {
          return this.searchLibrary.filter(function (content) {
            return Object.keys(content).some(function (key) {
              let isMatch = String(content[key]).toLowerCase().indexOf(search.toLowerCase()) > -1
              return isMatch
            })
          })
        }
        // return this.searchLibrary
      }
    },
    created () {
      let _this = this
      axios.get('static/data/data.json').then(function (response) {
        // 肾脏内科试题
        let nephrology = response.data.nephrology
        // 皮肤科试题
        let dermatology = response.data.dermatology
        // 血液科试题
        let hematology = response.data.hematology
        // 内分泌科试题
        let endocrinology = response.data.endocrinology
        // 儿科试题
        let pediatric = response.data.pediatric
        // 感染科试题
        let Infectious = response.data.Infectious
        // 呼吸内科试题
        let respiratory = response.data.respiratory
        // 普外科试题
        let generalSurgery = response.data.generalSurgery
        // 乳腺外科试题
        let breastSurgery = response.data.breastSurgery
        // 烧伤科试题
        let burns = response.data.burns
        // 手术室试题
        let operatingRoom = response.data.operatingRoom
        // 神经内科试题
        let neurology = response.data.neurology
        // 肝胆胰外科试题
        let hepatopancreatobiliarySurgery = response.data.hepatopancreatobiliarySurgery
        // 骨科试题
        let orthopedics = response.data.orthopedics
        // 麻醉科试题
        let anesthesiology = response.data.anesthesiology
        // 泌尿外科
        let urinarySurgery = response.data.urinarySurgery
        // 胃肠外科试题
        let gastrointestinalSurgery = response.data.gastrointestinalSurgery
        // 心外科试题
        let cardiacSurgery = response.data.cardiacSurgery
        // 胸外科试题
        let thoracicSurgery = response.data.thoracicSurgery
        // 甲状腺外科试题
        let thyroidSurgery = response.data.thyroidSurgery
        // 脑外科试题
        let brainSurgery = response.data.brainSurgery
        /* 公共试题 */
        // 急诊科试题
        let emergency = response.data.emergency
        // 压疮试题
        let pressureSores = response.data.pressureSores
        // 静脉试题
        let tendons = response.data.tendons
        // 重症监护室试题
        let icu = response.data.icu
        // 风湿科
        let rheumatism = response.data.rheumatism
        // 消化科
        let digestive = response.data.digestive
        // 循环系统疾病
        let circulatoryDisease = response.data.circulatoryDisease
        // 肿瘤科
        let oncology = response.data.oncology
        _this.searchLibrary = _this.searchLibrary.concat(nephrology, dermatology,
          hematology, endocrinology, pediatric, Infectious, respiratory, generalSurgery,
          breastSurgery, burns, operatingRoom, neurology, hepatopancreatobiliarySurgery,
          orthopedics, anesthesiology, urinarySurgery, gastrointestinalSurgery, cardiacSurgery,
          thoracicSurgery, thyroidSurgery, brainSurgery, emergency, pressureSores, tendons, icu,
          rheumatism, digestive, circulatoryDisease, oncology)
      }).catch(function (error) {
        Mint.MessageBox('温馨提示', error)
      })
    }
  }
</script>

<style scoped>

  .anfy-online-search {
    position: fixed;
    width: 100%;
  }

  .clear {
    height: 100px;
  }

  .mint-search {
    height: auto;
  }

  /* 搜索结果 */
  .result {
    padding: 0.8rem;
    text-align: left;
  }

  .question {
    font-weight: 600;
  }

  .result span {
    color: red;
  }
</style>
