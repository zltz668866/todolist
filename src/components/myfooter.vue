<template>
  <div class="todo-footer" v-show="all">
    <label>
      <!-- <input type="checkbox" :checked='isAll' @click="checkedAllClick"/> -->
      <input type="checkbox" v-model="isAll">
    </label>
    <span>
      <span>已完成{{doneTotal}}</span> / 全部{{all}}
    </span>
    <button @click="clear">清除已完成任务</button>
  </div>
</template>

<script>
export default {
    name:'MyFooter',
    props:['tudos'],
    computed:{
      doneTotal(){
        const x=this.tudos.reduce((pre,todo)=>{
          return pre+(todo.done ? 1:0)},0)
          return x
      },
      all(){
        return this.tudos.length
      },
      isAll:{
        get(){
          return this.doneTotal===this.all && this.all>0
        },
        set(value){
          // this.checkedAll(value)
          this.$emit('checkedAll',value)
        }
        
      }
      
    },
    methods:{
      //一键选择和取消、通过e获取checkbox的bool值
      // checkedAllClick(e){
      //   this.checkedAll(e.target.checked)
      // }
      clear(){
        // this.clearDone()
        this.$emit('clearDone')
      }
    }
}
</script>

<style scoped>
    .todo-footer {
    height: 40px;
    line-height: 40px;
    padding-left: 6px;
    margin-top: 5px;
    }
    .todo-footer label {
    display: inline-block;
    margin-right: 20px;
    cursor: pointer;
    }
    .todo-footer label input {
    position: relative;
    top: -1px;
    vertical-align: middle;
    margin-right: 5px;
    }
    .todo-footer button {
    float: right;
    margin-top: 5px;}
</style>