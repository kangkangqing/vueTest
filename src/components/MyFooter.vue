<template>
<div style="display: flex;justify-content: space-between" v-show="todos.length!==0">
  <div>
    <input type="checkbox" :checked="isAll" v-model="isAll"> 已完成{{finishTotal}}/全部{{todos.length}}
  </div>
   <button style="background: coral" @click="clear">清除已完成任务</button>
</div>

</template>

<script>
export default {
  name: "MyFooter",
  props:['todos'],
  computed:{
    finishTotal(){
     const  res=this.todos.reduce((pre,current)=>{
        return pre+( current.done==true?1:0 );
      },0)
      return res

    },
    isAll:{
      get(){
        if(this.finishTotal==this.todos.length&&this.finishTotal>0){
          return true
        }
        return  false
      },
      set(v){
        this.$emit('checkAll',v)
      }

    }
  },
  methods:{
    // checkAlll(e){
    //   // console.log(e.target.checked)
    //   this.checkAll(e.target.checked)
    // }
    clear(){
        this.$emit('clearAll')
    }
  }
}
</script>

<style scoped>

</style>