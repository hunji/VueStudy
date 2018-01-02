<template>
  <div>
    <ComA number="666" @my-event="getMyEvent">
      <a>這是一個子組件</a>
    </ComA>
    <p is="com-a"></p>
    <p :is="comToRender"></p>
    <com-a></com-a>
    <div>
      {{myVal}}
    </div>
    <input type="text" v-model.number="myVal"/>
  </div>
</template>

<script>
  import ComA from './components/a'
  export default {
    components: { ComA },
    data () {
      return {
        myVal: '父组件内容',
        comToRender: 'ComA'
      }
    },
    methods: {
      getMyEvent (hello) {
        console.log('触发了父组件事件' + hello)
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
