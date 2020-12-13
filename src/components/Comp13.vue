<template>
  <div ref="box"></div>
</template>

<script>
import { ref, onMounted } from 'vue'
export default {
  name: 'Comp13',
  props: ['msg'],
  setup() {
    let box = ref(null)

    onMounted(() => {
      console.log('onMounted', box.value)
    })

    console.log(box.value) // null
    return {
      box
    }
  }
}
</script>
