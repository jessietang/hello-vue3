<template>
  <h4>{{ msg }}</h4>
  <p>{{ msg1 }}</p>
</template>

<script>
import { reactive, ref } from 'vue'
export default {
  props: ['msg'],
  name: 'comp2',
  data() {
    return {
      m1: 'hhhhh'
    }
  },
  // async setup() { // 不能是异步的
  setup() {
    /**
     * 1.setup执行时机：
     * beforeCreate: 表示组件刚刚被创建出来，组件的data和methods还没有初始化好
     * setup： 在beforeCreate和created之间
     * created: 表示组件刚刚被创建好，并且组件的data和methods已经初始化好
     *
     *
     * 2.setup注意点：
     * - 由于在执行setup函数的时候，还没有执行created生命周期方法，
     *   所以在setup函数中，是无法使用data和methods的
     * - 由于我们不能在setup函数中使用data和methods,
     *   所以Vue为了避免我们错误的使用，他直接将setup函数中的this修改成了undefined
     * - setup函数只能是同步的，不能是异步的
     */

    // const msg1 = ref(this.m1)
    const msg1 = ref('123')
    console.log(this) // undefined
    return {
      msg1
    }
  }
}
</script>
