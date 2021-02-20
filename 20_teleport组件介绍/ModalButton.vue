<!--  -->
<template>
  <button @click="modalOpen = true">
    打开一个对话框
  </button>

  <!-- 对话框代码 -->
  <Teleport to="body">
    <div v-if="modalOpen">
      <div>这是对话框
        <button @click="modalOpen = false">关闭对话框</button>
      </div>

    </div>
  </Teleport>

</template>

<script lang='ts'>
import { defineComponent, ref } from "vue";
export default defineComponent({
  name: "ModalButton",
  setup() {
    // 控制对话框显示或者隐藏的
    const modalOpen = ref(false);
    return {
      modalOpen
    };
  }
});
</script>
<style scoped>
</style>