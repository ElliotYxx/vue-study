<template>
  <h2>reactive的使用</h2>
  <h3>name: {{user.name}}</h3>
  <h3>age: {{user.age}}</h3>
  <h3>gender: {{user.gender}}</h3>
  <h3>wife: {{user.wife}}</h3>
  <hr>
  <button @click="updateUser">更新用户</button>
</template>

<script lang="ts">
import { defineComponent, reactive } from "vue";

export default defineComponent({
  name: "App",
  // 显示用户的相关信息，点击按钮，可以更新用户的相关信息数据
  /**
   * reactive
   * 作用: 定义多个数据的响应式
   * const proxy = reactive(obj): 接收一个普通对象然后返回该普通对象的响应式代理器对象
   * 响应式转换是“深层的”： 会影响对象内部所有嵌套的属性
   * 内部基于 ES6 的 Proxy 实现，通过代理对象操作源对象内部数据都是响应式的
   */
  setup() {
    const obj = {
      name: "sheva",
      age: 20,
      wife: {
        name: "aaa",
        age: 18,
        cars: ["benz", "tesla", "bmw"]
      }
    };
    // 把复杂数据编程响应式的数据
    // 返回的是一个Proxy代理对象，被代理的目标对象就是reactive中传入的对象
    // user现在是代理对象，obj是目标对象
    const user = reactive<any>(obj);
    console.log(user);
    // 方法
    const updateUser = () => {
      // user.name += "a";
      // user.age += 1;
      // user.wife.name += "===";
      // user.wife.cars[0] = "byd";
      // user ---> 代理对象， obj ---> 目标对象
      // 如果操作代理对象，目标对象中的数据也会随之变化，同时想要在操作数据的时候，洁敏也跟着重新渲染，就要操作代理对象
      // user.gender = "男"; //这种方式界面可以更新渲染，而且这个数据最终也添加到了 obj 里面

      // 通过当前的代理对象找到该对象中的某个属性，更改该属性总的某个数组的数字
      // user.wife.cars[1] = "honda";

      // 通过当前的代理对象把目标对象中的某个数组属性添加一个新的属性
      user.wife.cars[3] = "toyota";
    };
    return {
      user,
      updateUser
    };
  }
});
</script>