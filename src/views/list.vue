<template>
  <ul class="todo-list">
    <!-- completed: 完成的类名 -->
    <li v-for="tm in list" :key="tm.id" :class="{completed:tm.isDone}" >
      <div class="view">
        <input class="toggle" type="checkbox" v-model="tm.isDone" />
        <label>{{tm.name}}</label>
        <button @click="delTodo(tm.id)" class="destroy"></button>
      </div>
    </li>
  </ul>
  
</template>

<script>
export default {
    // 接收
    props: {
        list: {
            type: Array,
            // 默认数组
            default: ()=>[]
        },
    },
    methods: {
        delTodo(id) {
            this.$emit('del-todo',id)
        }
    },
}
</script>