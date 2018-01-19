<template>
  <div class="sales-board">
    <div class="sales-board-intro">
      <h2>流量分析</h2>
      <p>是指在获得网站访问量基本数据的情况下对有关数据进行统计、分析，从中发现用户访问网站的规律，并将这些规律与网络营销策略等相结合，从而发现目前网络营销活动中可能存在的问题，并为进一步修正或重新制定网络营销策略提供依据。当然这样的定义是站在网络营销管理的角度来考虑的</p>
    </div>
    <div class="sales-board-form">
      <div class="sales-board-line">
        <div class="sales-board-line">
          <div class="sales-board-line-left">
            购买数量：
          </div>
          <div class="sales-board-line-right">
            <el-input-number size="small" v-model="buyNum" :min="1" :max="1000" label="购买数量"></el-input-number>
          </div>
        </div>
        <div class="sales-board-line">
          <div class="sales-board-line-left">
            产品类型：
          </div>
          <div class="sales-board-line-right">
            <el-select size="small" v-model="buyType" placeholder="请选择"  @change="change">
              <el-option
                v-for="item in buyTypes"
                :key="item.value"
                :label="item.label"
                :value="item.value">
              </el-option>
            </el-select>
          </div>
        </div>
        <div class="sales-board-line">
          <div class="sales-board-line-left">
            有效时间：
          </div>
          <div class="sales-board-line-right">
            <el-radio-group v-model="period" size="medium">
              <el-radio-button v-for="item in periodList"
                        :key="item.value"
                        :label="item.value"
                        >{{item.label}}
              </el-radio-button>
            </el-radio-group>

          </div>
        </div>
        <div class="sales-board-line">
          <div class="sales-board-line-left">
            产品版本：
          </div>
          <div class="sales-board-line-right">
            <el-checkbox-group v-model="versions">
              <el-checkbox-button v-for="item in versionList"
                                  :key="item.value"
                                  :label="item.label"
                                  :value="item.value">

              </el-checkbox-button>
            </el-checkbox-group>
          </div>
        </div>
        <div class="sales-board-line">
          <div class="sales-board-line-left">
            总价：
          </div>
          <div class="sales-board-line-right">
            <el-button type="primary" @click="getPrice">获取价格</el-button>
            &nbsp;&nbsp;{{ price }} 元
          </div>
        </div>
        <div class="sales-board-line">
          <div class="sales-board-line-left">&nbsp;</div>
          <div class="sales-board-line-right">
            <el-button type="success" round>立即购买</el-button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import Vue from 'vue'
  import { Select, Option, InputNumber, Radio, RadioGroup, RadioButton, Checkbox, CheckboxButton, CheckboxGroup, Button } from 'element-ui'
  import _ from 'lodash'

  Vue.use(Select)
  Vue.use(Option)
  Vue.use(InputNumber)
  Vue.use(Radio)
  Vue.use(RadioGroup)
  Vue.use(RadioButton)
  Vue.use(Checkbox)
  Vue.use(CheckboxButton)
  Vue.use(CheckboxGroup)
  Vue.use(Button)
  export default {
    data () {
      return {
        buyNum: 0,
        buyType: {},
        period: {},
        versions: [],
        price: 0,
        buyTypes: [
          {
            label: '入门版',
            value: 0
          },
          {
            label: '中级版',
            value: 1
          },
          {
            label: '高级版',
            value: 2
          }
        ],
        periodList: [
          {
            label: '半年',
            value: 0
          },
          {
            label: '一年',
            value: 1
          },
          {
            label: '三年',
            value: 2
          }
        ],
        versionList: [
          {
            label: '客户版',
            value: 0
          },
          {
            label: '代理商版',
            value: 1
          },
          {
            label: '专家版',
            value: 2
          }
        ]
      }
    },
    methods: {
      // select
      change (value) {
        let obj = {}
        obj = this.buyTypes.find((item) => {
          return item.value === value
        })
        console.log(obj.label)
      },
      getPrice () {
        let buyVersionsArray = _.map(this.versions, (item) => {
          return item.value
        })
        let reqParams = {
          buyNumber: this.buyNum,
          buyType: this.buyType.value,
          period: this.period.value,
          version: buyVersionsArray.join(',')
        }
        this.$http.get('/api/getPrice', reqParams)
          .then((res) => {
            this.price = res.data.amount
          })
      }
    }
  }
</script>

<style scoped>

</style>
