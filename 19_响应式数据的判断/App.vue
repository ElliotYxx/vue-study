<!--  -->
<template>
  <h2>响应式数据的判断</h2>
</template>

<script lang='ts'>
import {
  defineComponent,
  isProxy,
  isReactive,
  isReadonly,
  isRef,
  reactive,
  readonly,
  ref
} from "vue";
export default defineComponent({
  name: "App",
  /**
   * isRef：检查一个值是否为一个 ref 对象
   * isReactive：检查一个对象是否是由 reactive 创建的响应式代理
   * isReadOnly：检查一个对象是否是由readonly创建的只读对象
   * isProxy：检查一个对象是否是由 reactive 或者 readonly 方法创建的代理
   */

  setup() {
    // isRef：检查一个值是否为一个 ref 对象
    console.log(isRef(ref({})));
    // isReactive：检查一个对象是否是由 reactive 创建的响应式代理
    console.log(isReactive(reactive({})));
    // isReadOnly：检查一个对象是否是由readonly创建的只读对象
    console.log(isReadonly(readonly({})));
    // isProxy：检查一个对象是否是由 reactive 或者 readonly 方法创建的代理
    console.log(isProxy(reactive({})));
    console.log(isProxy(readonly({})));

    return {};
  }
});
</script>
<style scoped>
</style>