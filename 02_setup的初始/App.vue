<template>
  <div>第一节课</div>
  <!-- <h1>{{number}}</h1> -->
</template>

<script lang="ts">
// defineComponent函数，目的是定义一个组件，内部可以传入一个配置对象
import { defineComponent } from "vue";

// 暴露出去一个定义好的组件
export default defineComponent({
  name: "App",
  // 组合api中第一个要使用的函数
  // setup(){
  //   //console.log('这里是setup函数')
  //   const number = 10
  //   return {
  //     number
  //   }
  // }
});
</script>