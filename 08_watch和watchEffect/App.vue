<!--  -->
<template>
  <h2>计算属性和监视</h2>
  <fieldset>
    <legend>姓名操作</legend>
    姓氏：<input
      type="text"
      placeholder="请输入姓氏"
      v-model="user.firstName"
    /> <br>
    名字：<input
      type="text"
      placeholder="请输入名字"
      v-model="user.lastName"
    />
  </fieldset>
  <fieldset>
    <legend>计算属性和监视的演示</legend>
    姓名：<input
      type="text"
      placeholder="显示姓名"
      v-model="fullName1"
    /> <br>
    姓名：<input
      type="text"
      placeholder="显示姓名"
      v-model="fullName2"
    /> <br>
    姓名：<input
      type="text"
      placeholder="显示姓名"
      v-model="fullName3"
    />

  </fieldset>
</template>

<script lang='ts'>
import {
  computed,
  defineComponent,
  reactive,
  watch,
  ref,
  watchEffect
} from "vue";
export default defineComponent({
  name: "App",
  setup() {
    // 定义一个响应式的对象
    const user = reactive({
      // 姓氏
      firstName: "东方",
      // 名字
      lastName: "不败"
    });
    // 通过计算属性的方式，实现第一个姓名的显示
    // vue3 中的计算属性
    // 计算属性中的函数中如果只传入一个回调函数，表示的是get
    // 第一个姓名：
    // 返回的是一个ref类型的对象
    const fullName1 = computed(() => {
      return user.firstName + "_" + user.lastName;
    });
    // 第二个姓名
    const fullName2 = computed({
      get() {
        return user.firstName + "_" + user.lastName;
      },
      set(val: string) {
        //console.log("====", val);
        const names = val.split("_");
        user.firstName = names[0];
        user.lastName = names[1];
      }
    });

    // 第三个姓名:
    const fullName3 = ref("");
    // 监视-----监视指定的数据
    // immediate 默认会执行一次watch， deep深度监视
    watch(
      user,
      ({ firstName, lastName }) => {
        fullName3.value = firstName + "_" + lastName;
      },
      { immediate: true, deep: true }
    );

    // 监视，不需要配置immediate就会默认进行监视
    // watchEffect(() => {
    //   fullName3.value = user.firstName + "_" + user.lastName;
    // });

    // 监视fullName3的数据，改变firstName和lastName
    watchEffect(() => {
      const names = fullName3.value.split("_");
      user.firstName = names[0];
      user.lastName = names[1];
    });

    // watch ----> 可以监视多个数据
    // watch([user.firstName, user.lastName, fullName3], () => {
    //   // 这里的代码就没有执行
    //   // fullName3 是响应式的数据，而前两个不是响应式的数据
    //   console.log("===");
    // })

    // 当我们监视非响应式数据的时候，需要更改一下代码
    watch([() => user.firstName, () => user.lastName], () => {
      // 这里的代码就没有执行
      // fullName3 是响应式的数据，而前两个不是响应式的数据
      console.log("===");
    });
    return {
      user,
      fullName1,
      fullName2,
      fullName3
    };
  }
});
</script>
<style scoped>
</style>