<template>
  <div>
    <button @click="handleClick">child increment</button>
    <HelloWorld ref="child"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  methods: {
    handleClick() {
      // 可以访问子组件的increment方法，但是无法直接访问count，因为count未被导出
      this.$refs.child.increment()
    }
  }
}
</script>
