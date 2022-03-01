<template>
   <li>
    <label>
      <!-- 给标签增加checked属性 -->
      <input type="checkbox" :checked="todo.done" @change="handleTodo(todo.id)"/>
      <span >{{todo.name}}</span>
     
    </label>
    <button class="btn btn-danger" @click="handleDelete(todo.id)">删除</button>
    <button class="btn btn-edit" >编辑</button>
  </li>
</template>

<script>
export default {
    name:'MyItem',
    //声明接收的对象
    props:['todo','checkTodo','deleteTodo'],
    mounted() {
      //console.log(this.todo)
    },
    methods: {
      handleTodo(id){
        console.log(id);
        this.checkTodo(id)
      },
      handleDelete(id){
        
        if(confirm("确定删除吗？")){
          //console.log(id);
          this.deleteTodo(id)
        }
      }
    },
}
</script>

<style scoped>
/*item*/
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}
li label {
  float: left;
  cursor: pointer;
}
li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}
li button {
  float: right;
  display: none;
  margin-top: 3px;
}
li:before {
  content: initial;
}
li:last-child {
  border-bottom: none;
}
li:hover{
  background-color: #ddd;
}
li:hover button{
  display: block;
}
.todo-enter-active{
  animation: todo 0.5s linear;
}
.todo-leave-active{
  animation: todo 0.5s linear reverse;
}
@keyframes todo {
  from{
    transform: translateX(100%);
  }
  to{
    transform: translateX(0px);
  }
}
</style>