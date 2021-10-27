<template>
  <div>
    <button @click="handleClick">child increment</button>
    <HelloWorld ref="child" />
    <button @click="testRef">test ref</button>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import { provide, ref, onMounted } from "vue";

export default {
  name: "App",
  components: {
    HelloWorld,
  },
  setup() {
    const name = ref("name");
    provide("name", name);
    // setTimeout(() => {
    //   name.value = 'new name'
    // }, 2000)
    const child = ref(null);
    const handleClick = () => {
      child.value.increment();
    };
    onMounted(() => {
      console.log(child.value);
    });
    return {
      name,
      handleClick,
      // 虚拟DOM补丁算法中VNode的ref属性值如果和render context中的ref对应，那么在虚拟DOM挂载/patch过程中会将该虚拟DOM赋给render context中对应的ref
      // 此处通过setup return将child暴露到render context中，因此挂载后template中的ref='child'节点会被赋给下面的child
      child,
    };
  },
  methods: {
    // handleClick() {
    // 可以访问子组件的increment方法，但是无法直接访问count，因为count未被导出
    // this.$refs.child.increment()
    // },
    testRef() {
      // setup中return出来的ref可以通过以下方式修改
      this.name = "1";
      console.log(this.name);
    },
  },
};
</script>
