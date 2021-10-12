<template>
  <footer class="footer">
    <span class="todo-count">剩余<strong>{{list.length}}</strong></span>
    <ul class="filters">
      <li>
        <a @click="changeType('all')"  :class='{ selected : flag === "all"}' href="javascript:;" >全部</a>
      </li>
      <li>
        <a @click="changeType('unok')" :class='{ selected : flag === "unok"}' href="javascript:;">未完成</a>
      </li>
      <li>
        <a @click="changeType('ok')" :class='{ selected : flag === "ok"}' href="javascript:;" >已完成</a>
      </li>
    </ul>
    <button @click="delFt" class="clear-completed" >清除已完成</button>
  </footer>
</template>

<script>
// 1. 父组件中定义切换状态数据=》全部 未完成 已完成
// 2. 当前状态传递给子组件foot，根据切换状态高亮显示按钮
// 3. 显示对应状态的任务列表数据


export default {
    props: {
        list: {
            type: Array,
            // 返回一个数组 如果是对象 ()=>({})  数组[] 如果是()=>[]函数更加规范推荐
            default: ()=>[]
        },
        flag:{
          type:String,
          default:''
        }
    },
    methods: {
      changeType(flag) {
        this.$emit('change-flag', flag )
      },
      delFt(){
        this.$emit('del-ok')
      }
    },
}
</script>