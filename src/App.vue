<template>
  <div id="app">
    <div class="todo-container">
      <div class="todo-wrap">
        
        <MyHeader @addTodo="addTodo"></MyHeader>

        <!-- <MyList :tudos="tudos" :checkTodo='checkTodo' :deleteTodo='deleteTodo'/> -->
        <MyList :tudos='tudos'></MyList>
        
        <MyFooter :tudos='tudos' @checkedAll='checkedAll' @clearDone='clearDone'></MyFooter>
      </div>
    </div>
  </div>
</template>

<script>
import MyHeader from './components/myheader'
import MyList from './components/mylist'
import MyFooter from './components/myfooter.vue'

export default {
  name: 'App',
  components: {
    MyHeader,MyList,MyFooter
  },
  data() {
        return { 

          
            tudos:JSON.parse(localStorage.getItem('todos'))||[]
        }
    },
  methods:{
    addTodo(todoObj){
      this.tudos.unshift(todoObj)
    },
    checkTodo(id){
      this.tudos.forEach(obj => {
        if(obj.id===id){obj.done=!obj.done}
      });
    },
    deleteTodo(id){
      this.tudos=this.tudos.filter(obj =>{return obj.id!==id})
    },
    checkedAll(done){
      this.tudos.forEach((todo)=>{
        todo.done=done
      })
    },
    clearDone(){
      this.tudos=this.tudos.filter((obj)=>{return !obj.done===true})
    },
    changeName(id,newName){
      this.tudos.forEach(obj=>{
        if(obj.id===id){obj.name=newName}
      })
    }
    },
    watch:{
        tudos:{
          deep:true,
          handler(value){
            console.log(value);
            window.localStorage.setItem('todos',JSON.stringify(value))
          }
        }
      // tudos(value){
      //   window.localStorage.setItem('todos',JSON.stringify(value))
      // }
    },
    mounted(){
      this.$bus.$on('checkTodo',this.checkTodo)
      this.$bus.$on('deleteTodo',this.deleteTodo)
      this.$bus.$on('changeName',this.changeName)
    },
    beforeDestroy(){
      this.$bus.$off('checkTodo')
      this.$bus.$off('deleteTodo')
      this.$bus.$off('changeName')
    }
}
</script>

<style>
  /*base*/
  body {
    background: #fff;
  }
  .btn {
    display: inline-block;
    padding: 4px 12px;
    margin-bottom: 0;
    font-size: 14px;
    line-height: 20px;
    text-align: center;
    vertical-align: middle;
    cursor: pointer;
    box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
    border-radius: 4px;
  }
  .btn-danger {
    color: #fff;
    background-color: #da4f49;
    border: 1px solid #bd362f;
  }
  .btn-edit {
    color: #fff;
    background-color: lightgreen;
    border: 1px solid green;
    margin-right: 5px;
  }
  .btn-danger:hover {
    color: #fff;
    background-color: #bd362f;
  }
  .btn-edit:hover {
    color: #fff;
    background-color: green;
  }
  .btn:focus {
    outline: none;
  }
  .todo-container {
    width: 600px;
    margin: 0 auto;
  }
  .todo-container .todo-wrap {
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
  }
</style>
