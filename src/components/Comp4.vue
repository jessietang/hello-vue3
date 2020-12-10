<template>
  <h4>{{ msg }}</h4>
  <p>{{ age }}</p>
  <button @click="updateAge">updateAge</button>
</template>

<script>
/**
 * 1.什么是ref?
 *  - ref和reactive一样，也是用来实现响应式数据的方法
 *  - 由于reactive必须传递一个对象，所以导致在企业开发中，
 *    如果我们想让某个变量实现响应式的时候会非常麻烦
 *    所以vue3就给我们提供了ref方法，实现对简单值的判断
 *
 * 2.ref本质：
 *  - ref底层的本质其实还是reactive
 *    系统会自动根据我们给ref传入的值将他转换成
 *    ref(xx) -> reactive({value: xx})
 *
 * 3.ref注意点：
 *  - 在vue template中使用ref的值不用通过value获取
 *  - 在js中使用ref的值必须通过value获取
 */
import { ref } from 'vue'
export default {
  name: 'Comp4',
  props: ['msg'],
  setup() {
    let age = ref(18) // ref(18) -> reactive({value: 18})
    function updateAge() {
      age.value = 66
    }
    return {
      age,
      updateAge
    }
  }
}
</script>
