<template>
  <div>
    <h1>姓名：{{ person.name }}</h1>
    <h1>年龄：{{ person.age }}</h1>
    <h1>性别：{{ person.sex }}</h1>
    <button @click="headleClick1">我是子组件，我要把数据传递给父组件(通过回调函数)</button>
    <button @click="headleClick2">我是子组件，我要把数据传递给父组件(通过 $emit)</button>
    <button @click="headleClick3">我是子组件，我要把数据传递给父组件(通过时间总线)</button>
  </div>
</template>

<script>
export default {
  props: {
    person: {
      type: Object,
      default() {
        return {}
      }
    },
    getSonData: {
      type: Function
    }
  },
  data() {
    return {
      message: '我是子组件的数据，我要把这个数据传递给父组件(通过回调函数)',
      msg: '我是子组件的数据，我要把这个数据传递给父组件(通过 $emit)',
      msg2: '我是子组件的数据，我要把这个数据传递给父组件(通过时间总线)',
    }
  },
  methods: {
    headleClick1() {
      this.getSonData(this.message)
    },
    headleClick2() {
      this.$emit('headleClick2', this.msg)
    },
    headleClick3() {
      this.$bus.$emit('bus', this.msg2)
    }
  },
}
</script>

<style>

</style>