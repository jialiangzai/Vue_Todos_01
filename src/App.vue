<template>
  <div class="todoapp">
    <Head :list="list" @change-list="addTodo" @alls="isAlls" />
    <!-- 父传子 提升渲染性能 计算属性-->
    <List @del-todo="delTodo" :list="newList" />
    <Foot @del-ok="delOk" @change-flag="changeType" :flag="flag" :list="list" />
  </div>
</template>

<script>
import Head from "./views/head.vue";
import List from "./views/list.vue";
import Foot from "./views/foot.vue";
import "./styles/base.css";
import "./styles/index.css";
export default {
  name: "App",
  components: {
    Head,
    List,
    Foot,
  },
  data() {
    return {
      //  列表数据状态值:全部（all） 完成（ok） 未完成（unOk）
      //  * 数据切换
      //  * 需求：点击对应按钮（全部、完成、未完成）显示不同的列表数据
      //  * 1. 点击按钮(菜单)的高亮
      //  * 思路：
      //  * 1. 定义一个当前的标识flag（index、string、id等）（代表当前高亮的元素）
      //  * 2. 根据flag对比所有需要高亮的元素
      //  *
      //  * 2. 对应高亮的按钮=》切换数据
      //  * 思路：
      //  * 根据flag条件，使用计算属性动态计算对应状态的列表数据

      flag: "all",
      // list: [
      //   { id: 100, name: "吃饭", isDone: true },
      //   { id: 201, name: "睡觉", isDone: false },
      //   { id: 103, name: "打豆豆", isDone: true },
      // ],
      list: JSON.parse(localStorage.getItem("todoLists")) || [],
    };
  },
  // 渲染页面 用计算属性 结果传递给foot

  
  computed: {
    newList() {
      if (this.flag === "ok") {
        return this.list.filter((item) => item.isDone === true);
      } else if (this.flag === "unok") {
        return this.list.filter((item) => item.isDone === false);
      } else {
        return this.list;
      }
    },
  },
  watch: {
    // 过滤作用 计算属性必须要加return  生成新的数组
    list: {
      deep: true,
      // immediate:true,
      handler(listAry) {
        localStorage.setItem("todoLists", JSON.stringify(listAry));
      },
    },
  },
  //  watch: {
  //   // list (newValue) {
  //   //   console.log('列表变化了：', newValue)
  //   // }
  //   list: {
  //     deep: true,
  //     // immediate:true,
  //     handler (newValue) {
  //       // console.log('列表变化了：', newValue)
  //       localStorage.setItem('todoLists', JSON.stringify(newValue))
  //     },
  //   }
  // },
  methods: {
    addTodo(name) {
      // console.log('go');
      this.list.unshift({ id: Date.now(), name, isDone: false });
    },
    delTodo(id) {
      this.list = this.list.filter((item) => item.id !== id);
    },
    changeType(type) {
      this.flag = type;
    },
    delOk() {
      // 过滤器做到删除效果
      // this.list.filter(item=>item.isDone === false)
      this.list = this.list.filter((item) => !item.isDone);
    },
    isAlls(newsAll) {
      this.list.forEach((item) => {
        item.isDone = newsAll;
      });
    },
  },
};
</script>

<style>
</style>
