<template>
  <div class="todo-header">
    <input type="text" placeholder="请输入你的任务名称，按回车键确认" v-model="name"  @keyup.enter="add"/>
  </div>
</template>

<script>
import {nanoid} from 'nanoid'
export default {  
    name:'MyHeader',
    data() {
      return {
        name:''  //第二种通过v-model动态获取数据方式
      }
    },
    methods:{
      add(){
        if(!this.name.trim())
          return alert('输入不能为空')

        // console.log(event.target.value)  第二种获取输入数据方式
        const todo={'id':nanoid(),'name':this.name,'done':false}
        // console.log(todo)
        // this.addTodo(todo)
        this.$emit('addTodo',todo)  //第二步出发组件自定义事件
        this.name=''
      }
    },
    // props:['addTodo']
}
</script>

<style>
    /*header*/
    .todo-header input {
    width: 560px;
    height: 28px;
    font-size: 14px;
    border: 1px solid #ccc;
    border-radius: 4px;
    padding: 4px 7px;
    }
    .todo-header input:focus {
    outline: none;
    border-color: rgba(82, 168, 236, 0.8);
    box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 8px rgba(82, 168, 236, 0.6);
    }
</style>