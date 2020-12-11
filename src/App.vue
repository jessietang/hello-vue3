<template>
  <!-- <Comp1
    msg="1.toRefs API 用来提供解决此约束的办法——它将响应式对象的每个 property 都转成了相应的 ref"
  /> -->
  <Comp2 msg="2.setup执行时机 + setup注意点" />
  <Comp3 msg="3.reactive理解" />
  <Comp4 msg="4.ref理解" />
  <Comp5 msg="5.ref和reactive的区别" />
  <Comp6 msg="6.递归监听（每一层都可以监听）和非递归监听" />
  <Comp7 msg="7.toRaw方法拿到原始数据" />
  <Comp8 msg="8.markRaw使数据永远不被追踪" />
</template>

<script>
import Comp1 from './components/Comp1.vue'
import Comp2 from './components/Comp2.vue'
import Comp3 from './components/Comp3.vue'
import Comp4 from './components/Comp4.vue'
import Comp5 from './components/Comp5.vue'
import Comp6 from './components/Comp6.vue'
import Comp7 from './components/Comp7.vue'
import Comp8 from './components/Comp8.vue'

export default {
  name: 'App',
  components: {
    Comp1,
    Comp2,
    Comp3,
    Comp4,
    Comp5,
    Comp6,
    Comp7,
    Comp8
  }
}
</script>
