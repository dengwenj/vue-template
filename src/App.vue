<template>
  <div>
    <!-- 
      1 父传子（无疑世界上最简单的方式 props 传递），就在这个组件里面写上属性就行，然后动态的获取 data 的值，
      模版里面可以直接取 data 里面的值不用加 this，这样这个 person 属性就被传入自组件里面去了
      在子组件里面写个 props 配置项就可以拿到父组件传递过来的值

      2 子传父，在父组件里面写个方法，然后传递给子组件，在子组件里面调用，把数据传递过来，
        这样父组件里面写的方法就可以接受到数据

      3 子传父, 通过自定义事件传值，在 vue 里面有个 $emit, 事件名要和 this.$emit('这里一样')

      4 通过 ref 获取子组件的值 this.$refs.demo.msg， this.$refs.demo 这样拿到了子组件这个实例，就可以操作子组件

      5 通过 事件总线 $bus 就是在原型添加个 $bus 值为 Vue 的实例对象，这个原理就是通过 $emit 和 $on，任何组件都可以传递
        当前这种方法在 Vue3 里面已经不能用了

      ....还有组件传值的方式 Vuex 等等
     -->
    <Demo1 ref="demo" :person="person" :getSonData="getSonData" @headleClick2="headleClick2"/>
    <button @click="headleRef">通过ref</button>
  </div>
</template>

<script>
import Demo1 from './components/Demo1'
export default {
  data() {
    return {
      person: {
        name: 'dengwj',
        age: 21,
        sex: '男'
      }
    }
  },
  components: {
    Demo1
  },
  mounted() {
    this.$bus.$on('bus', (msg) => {
      console.log(msg);
    })
  },
  methods: {
    getSonData(msg) {
      console.log(msg); // 子组见传递过来的
    },
    headleClick2(msg) {
      console.log(msg); // 我是子组件的数据，我要把这个数据传递给父组件(通过 $emit)
    },
    headleRef() { 
      console.log(this.$refs.demo.msg); // 这样也能拿到子组件的数据
    }
  }
}
</script>

<style>

</style>