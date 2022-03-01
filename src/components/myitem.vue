<template>
  <transition appear name="todo">
      <li>
        <label>
          <!-- 给标签增加checked属性 -->
          <input type="checkbox" :checked="todo.done" @change="handleTodo(todo.id)"/>
          <span v-show="!todo.isEdit">{{todo.name}}</span>
        <input 
          type="text" 
          v-show="todo.isEdit"
          @blur="blurHandler(todo,$event)"  
          :value="todo.name"
          ref="inputName"
          >
        </label>
      <button class="btn btn-danger" @click="handleDelete(todo.id)">删除</button>
      <button class="btn btn-edit" @click="handleEdit(todo)" v-show="!todo.isEdit">编辑</button>
    </li>
  </transition>
</template>

<script>
export default {
    name:'MyItem',
    //声明接收的对象
    props:['todo'],
    mounted() {
      //console.log(this.todo)
    },
    methods: {
      handleTodo(id){
        // console.log(id);
        // this.checkTodo(id) 这是最基本写法，一次次传递
        this.$bus.$emit('checkTodo',id)
      },
      handleDelete(id){
        
        if(confirm("确定删除吗？")){
          //console.log(id);
          // this.deleteTodo(id)
          this.$bus.$emit('deleteTodo',id)
        }
      },
      handleEdit(todo){
        // todo.isEdit=true//这种方式添加的不是响应式
        if (Object.prototype.hasOwnProperty.call(todo,'isEdit')) {
          todo.isEdit=true
        
        } else {
          this.$set(todo,'isEdit',true) //添加响应式属性
        }
        this.$nextTick(()=>(
          this.$refs.inputName.focus()
        ))
        //解决渲染执行前后顺序问题（方法全部执行完毕，最后进行渲染，存在标签没渲染进行调用，然后无效），有两种解决方式
        // setTimeout(()=>(
        //   this.$refs.inputName.focus()
        // ),200)
       
      },
      blurHandler(todo,e){
        todo.isEdit=false
        if(!e.target.value.trim()) return alert('输入不能为空')
        this.$bus.$emit('changeName',todo.id,e.target.value)
        console.log(e.target.value);
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