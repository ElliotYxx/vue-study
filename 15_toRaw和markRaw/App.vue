<!--  -->
<template>
  <h2>toRaw和markRaw</h2>
  <h3>state:{{state}}</h3>
  <hr>
  <button @click="testToRaw">测试toRaw</button>
  <button @click="testMarkRaw">测试markRaw</button>
</template>

<script lang='ts'>
import { defineComponent, reactive, toRaw, markRaw } from "vue";
interface UserInfo {
  name: string;
  age: number;
  likes?: string[];
}
export default defineComponent({
  name: "App",
  setup() {
    const state = reactive<UserInfo>({
      name: "小明",
      age: 20
    });
    const testToRaw = () => {
      // 把代理对象编程了普通对象，如果数据变化界面则不会变化
      const user = toRaw(state);
      user.name += "+";
      console.log("testToRaw");
    };

    const testMarkRaw = () => {
      // state.likes = ["eat", "drink"];
      // state.likes[0] += "+";
      const likes = ["吃", "喝"];
      // markRaw标记的对象数据源从此以后都不能再成为代理对象
      state.likes = markRaw(likes);
      setInterval(() => {
        if (state.likes) {
          state.likes[0] += "+";
          console.log("定时器");
        }
      }, 1000);
      console.log("testMarkRaw");
      console.log(state);
    };
    return {
      state,
      testToRaw,
      testMarkRaw
    };
  }
});
</script>
<style scoped>
</style>