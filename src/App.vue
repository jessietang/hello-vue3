<template>
  <!-- <Comp1
    msg="toRefs API 用来提供解决此约束的办法——它将响应式对象的每个 property 都转成了相应的 ref"
  /> -->
  <Comp2 msg="setup执行时机 + setup注意点" />
  <Comp3 msg="reactive理解" />
  <Comp4 msg="ref理解" />
  <Comp5 msg="ref和reactive的区别" />
</template>

<script>
import Comp1 from './components/Comp1.vue'
import Comp2 from './components/Comp2.vue'
import Comp3 from './components/Comp3.vue'
import Comp4 from './components/Comp4.vue'
import Comp5 from './components/Comp5.vue'

export default {
  name: 'App',
  components: {
    Comp1,
    Comp2,
    Comp3,
    Comp4,
    Comp5
  }
}
</script>
