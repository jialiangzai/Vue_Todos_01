<template>
  <header class="header">
    <h1>todos</h1>
    <!-- 全选和取消全选 -->
    <input
     
      id="toggle-all"
      class="toggle-all"
      type="checkbox"
      placeholder="输入任务名称-回车确认"
    />
    <label for="toggle-all"></label>
    <!-- 输入新增的任务名 -->

    <input  v-model="name" @keyup.enter="addTodo" class="new-todo" placeholder="输入任务名称-回车确认" autofocus />
  </header>
</template>

<script>
export default {
  data() {
    return {
      name: "",
    };
  },
  methods: {
      addTodo() {
        // 校验非空  添加数据 子传父 this.$emit
        if (!this.name) {
            return alert('任务名不能为空！')
        }
        this.$emit('change-list',this.name)
        this.name=''
      }
  },
};
</script>