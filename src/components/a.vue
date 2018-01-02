<template>
<div>
  {{ number }}
  {{ hello }}
  <button @click="emitMyEvent">emit</button>
  <slot>
    no slot
  </slot>
</div>
</template>

<script type="text/ecmascript-6">
  export default{
    props: ['number'],
    data () {
      return {
        hello: 'i am componentA'
      }
    },
    methods: {
      emitMyEvent () {
        this.$emit('my-event', this.hello)
      }
    }
  }
</script>
