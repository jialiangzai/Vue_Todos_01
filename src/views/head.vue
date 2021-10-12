<template>
  <header class="header">
    <h1>todos</h1>
    <!-- 全选和取消全选 -->
    <input
      v-model="isAll"
      id="toggle-all"
      class="toggle-all"
      type="checkbox"      
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
  props: {
    list: {
      type: Array,
      default: ()=>[]
    },
  },
  computed: {
    // v-model功能数据双向绑定，在点击全选表单复选框后会修改计算属性的结果，我们要用使用计算属性的对象全写模式 get set  关于set的参数是改变的计算属性结果
    // isAlll() {
    //   // return this.list.every(item=>item.isDone == true)
    //   return this.list.every(item=>item.isDone)
    // }
    isAll:{
      get(){
         return this.list.every(item=>item.isDone)
      },
      set(valNew){
        return this.$emit('alls',valNew)
      //   this.list.forEach(item => {
      //   item.isDone=valNew
      // });
      }
    }
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