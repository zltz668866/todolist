<template>
   <li>
    <label>
      <!-- 给标签增加checked属性 -->
      <input type="checkbox" :checked="this.todo.done"/>
      <span >{{this.todo.name}}</span>
     
    </label>
    <button class="btn btn-danger" >删除</button>
    <button class="btn btn-edit" >编辑</button>
  </li>
</template>

<script>
export default {
    name:'MyItem',
    //声明接收的对象
    props:['todo'],
    mounted() {
      console.log(this.todo)
    }
}
</script>

<style>
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