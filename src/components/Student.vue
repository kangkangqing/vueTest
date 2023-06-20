<template>
<div style="border: 1px solid deepskyblue">
  <h2>{{name}}</h2>
  <h2>{{sex}}</h2>
  <button @click="sendStudentName">把学生名交给学校</button>
  <button>解绑黑马事件</button>
</div>
</template>

<script>
export default {
  name: "Student",
  data(){
    return{
      name:"张三",
      sex:"男"
    }
  },
methods:{
  sendStudentName(){
    this.$bus.$emit('hello',this.name)
  }
}
}
</script>

<style scoped>

</style>