<template>
  <div>{{count}}</div>
</template>

<script>
import {ref} from 'vue'
export default {
  name: "HelloWorld",
  // expose: ['increment'],
  setup(props, {expose}) {
    const count = ref(0)
    const increment = () => {
      count.value ++
    }
    // 向外暴露的属性，外部通过$refs/$parent/$root调用当前组件时只有被暴露的属性才能被访问到
    // 可以保持组件的封装性，避免外部随意访问/修改当前组件的属性
    expose({
      increment
    })
    return {
      count,
      increment
    }
  }
};
</script>

<style></style>
