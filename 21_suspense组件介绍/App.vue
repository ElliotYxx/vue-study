<!--  -->
<template>
  <h2>App父级组件：Suspense组件的使用</h2>
  <Suspense>

    <template #default>
      <!-- 异步组件 -->
      <!-- <AsyncComponent /> -->
      <AsyncAddress />
    </template>
    <template v-slot:fallback>
      <!-- 准备的内容 -->
      <h2>Loading</h2>
    </template>
  </Suspense>
</template>

<script lang='ts'>
import { defineAsyncComponent, defineComponent } from "vue";

// 引入组件：静态引入与动态引入
// Vue2中动态引入组件的写法 在Vue3中这种写法不行
// const AsyncComponent = () => import("./AsyncComopnent.vue");
// Vue3中动态引入组件的写法
// const AsyncComponent = defineAsyncComponent(() =>
//   import("./AsyncComopnent.vue")
// );
// 静态引入组件
// import AsyncComponent from "./AsyncComopnent.vue";
import AsyncAddress from "./AsyncAddress.vue";
export default defineComponent({
  name: "App",
  components: {
    // AsyncComponent
    AsyncAddress
  }
});
</script>
<style scoped>
</style>