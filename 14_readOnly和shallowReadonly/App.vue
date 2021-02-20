<!--  -->
<template>
  <h2>readOnly和shallowReadonly</h2>
  <h3>state:{{state2}}</h3>
  <button @click="update">更新</button>
</template>

<script lang='ts'>
import { defineComponent, reactive, readonly, shallowReadonly } from "vue";
export default defineComponent({
  name: "App",
  setup() {
    const state = reactive({
      name: "xiaoming",
      age: 20,
      car: {
        name: "benz",
        color: "yellow"
      }
    });
    // 只读数据 —— 深度只读
    // const state2 = readonly(state);
    // 只读的数据 —— 浅只读
    const state2 = shallowReadonly(state);
    const update = () => {
      // console.log("测试");
      // state2.name += "=";
      state2.car.name += "+";
    };
    return {
      // state,
      state2,
      update
    };
  }
});
</script>
<style scoped>
</style>