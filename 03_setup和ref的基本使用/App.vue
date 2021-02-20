<template>
  <h2>setup和ref的基本使用</h2>
  <h3>{{ count }}</h3>
  <button @click="updateCount">更新数据</button>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";

export default defineComponent({
  name: "App",
  // 页面打开后可以直接看到一个数据，点击按钮后该数据可以发生变化
  // vue2 实现方式
  // data() {
  //   return {
  //     count: 0 // 属性
  //   };
  // },
  // methods: {
  //   updateCount() { // 方法
  //     this.count++;
  //   }
  // }
  // vue3 实现方式
  // setup是组合api的入口函数，只在初始化时执行一次
  setup() {
    // 变量
    // let count = 0; // 此时的数据并不是响应式的数据，数据变化页面不随着渲染变化
    // ref是一个函数，作用是定义一个响应式的数据，返回的是一个ref对象，对象中有一个value属性，如果要对数据进行操作，需要对value属性进行操作
    // html模板中是不需要.value属性的写法
    // 一般用于定义一个基本数据类型的响应式数据
    const count = ref(0);
    // 方法
    function updateCount() {
      // count是一个ref对象，对象是不能进行自增操作的
      // count++;
      count.value++;
    }
    // 返回的是一个对象
    return {
      // 属性
      count,
      updateCount
    };
  }
});
</script>