<template>
<div style="border: 1px solid red">
  <h2>{{name}}</h2>
  <h2>{{address}}</h2>
  <button>将学校名交给app</button>
</div>
</template>

<script>
export default {
  name: "School",
  data(){
    return{
      name:"大工程",
      address:'江津'
    }
  },
  methods:{
    getStudentName(name){
      console.log("学校收到了学生名"+name)
    },

  },
  mounted() {
    this.$bus.$on('hello',this.getStudentName)
  },
  beforeDestroy() {
    this.$bus.$off(['hello'])
  }
}
</script>

<style scoped>

</style>