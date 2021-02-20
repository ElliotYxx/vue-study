<!--  -->
<template>
  <h2>shallow Reactive和shallowRef</h2>
  <h3>m1: {{m1}}</h3>
  <h3>m2: {{m2}}</h3>
  <h3>m3: {{m3}}</h3>
  <h3>m4: {{m4}}</h3>
  <hr>
  <button @click="update">更新数据</button>
</template>

<script lang='ts'>
import {
  defineComponent,
  reactive,
  ref,
  shallowReactive,
  shallowRef
} from "vue";
export default defineComponent({
  name: "App",
  setup() {
    // 深度劫持（深监视）—— 深度响应式
    const m1 = reactive({
      name: "xiaoming",
      age: 17,
      car: {
        name: "benz",
        color: "green"
      }
    });

    // 浅劫持（浅监视） —— 浅响应式
    const m2 = shallowReactive({
      name: "xiaohong",
      age: 18,
      car: {
        name: "bmw",
        color: "red"
      }
    });

    // 深度劫持（深监视）—— 深度响应式
    const m3 = ref({
      name: "xiaohua",
      age: 19,
      car: {
        name: "byd",
        color: "yellow"
      }
    });
    // 浅劫持（浅监视） —— 浅响应式
    const m4 = shallowRef({
      name: "xiaozhang",
      age: 20,
      car: {
        name: "honda",
        color: "black"
      }
    });
    const update = () => {
      // 更改m1的数据 ---> reactive的方式
      // m1.name += "=";
      // m1.car.name += "+";
      // 更改m2的数据 ----> shallowReactive的方式
      // m2.name += "==";
      // m2.car.name += "++";
      // 更改m3的数据 ----> ref的方式
      // m3.value.name += "===";
      // m3.value.car.name += "+++";
      // 更改m4的数据 ----> shallowRef的方式
      // m4.value.name += "====";
      // m4.value.car.name += "++++";
      console.log(m3, m4);
    };
    return {
      m1,
      m2,
      m3,
      m4,
      update
    };
  }
});
</script>
<style scoped>
</style>