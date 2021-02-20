<!--  -->
<template>
  <h2>toRefs的使用</h2>
  <!-- <h3>name:{{state.name}}</h3>
  <h3>age:{{state.age}}</h3> -->

  <h3>name:{{name}}</h3>
  <h3>age:{{age}}</h3>

  <h3>name2:{{name2}}</h3>
  <h3>age2:{{age2}}</h3>
</template>

<script lang='ts'>
import { defineComponent, reactive, toRefs } from "vue";

function useFeatureX() {
  const state = reactive({
    name2: "xiaoming",
    age2: 17
  });
  return {
    ...toRefs(state)
  };
}
export default defineComponent({
  name: "App",

  setup() {
    const state = reactive({
      name: "xiaoming",
      age: 17
    });
    // toRefs可以把一个响应式对象转换成普通对象，该普通对象的每个property都是一个ref
    // const state2 = toRefs(state);
    const { name, age } = toRefs(state);
    // console.log(state2);
    // 定时器 更新数据 如果数据变化，界面也会随之变化，那么肯定是响应式的数据
    setInterval(() => {
      //state.name += "=";
      name.value += "=";
    }, 1000);

    const { name2, age2 } = useFeatureX();
    return {
      //...state // 不是响应式的数据了 ---> {name: 'xiaoming', age: 17}
      // toRefs返回的对象
      //...state2
      name,
      age,
      name2,
      age2
    };
  }
});
</script>
<style scoped>
</style>