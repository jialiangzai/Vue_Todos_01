<template>
  <div class="todoapp">
    <Head />
    <!-- 父传子 提升渲染性能 -->
    <List :list="list"/>
    <Foot />
  </div>
</template>

<script>
import Head from "./views/head.vue";
import List from "./views/list.vue";
import Foot from "./views/foot.vue";
import "../styles/base.css";
import "../styles/index.css";
export default {
  name: "App",
  components: {
    Head,
    List,
    Foot,
  },
  data() {
    return {
       list: [
        { id: 100, name: "吃饭", isDone: true },
        { id: 201, name: "睡觉", isDone: false },
        { id: 103, name: "打豆豆", isDone: true },
      ],
    }
  },
};
</script>

<style>
</style>
