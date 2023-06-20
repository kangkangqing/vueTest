<template>
  <div id="app" style="background: #fff">
    <h1>ToDoList练习</h1>
    <div style="border:1px solid darkred;padding: 10px">
      <MyHeader @getData="addTodo"></MyHeader>
      <list :todos="todos"></list>
      <MyFooter :todos="todos" @checkAll="checkAll" @clearAll="clearAll"></MyFooter>
    </div>

    <h1>自定义事件</h1>
    <div style="border: 1px solid black">
      {{ msg }}
      <div/>
      <School></School>
      <Student></Student>
    </div>
  </div>
</template>
<script>
import School from "@/components/School";
import Student from "@/components/Student";
import MyHeader from "@/components/MyHeader";
import MyFooter from "@/components/MyFooter";
import List from "@/components/List";

export default {
  name: 'App',
  components: {MyFooter, List, MyHeader, Student, School},
  data() {
    return {
      todos: JSON.parse(sessionStorage.getItem("todos")) || [],
      msg: "你好啊"
    }
  },
  methods: {
    //添加一个todo
    addTodo(x) {
      this.todos.push(x)
    },

    //更新一个todo的checked
    updateCheck(id) {
      this.todos.forEach((todo) => {
        if (todo.id == id) {
          todo.done = !todo.done
        }
      })
    },

    //删除一个todo
    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => {
        return todo.id != id
      })
    },

    //控制全选与全不选
    checkAll(checked) {
      this.todos.forEach((todo) => {
        todo.done = checked
      })
    },

    //删除所有已完成
    clearAll() {
      // console.log("我被调用了")
      this.todos = this.todos.filter((todo) => {
        return todo.done == false
      })
    },

    //更新一个todo的name
    updateTodo(id,name) {
      this.todos.forEach((todo) => {
        if (todo.id == id) {
          todo.name = name
        }
      })
    },

    getSchoolName(name) {
      console.log(name)
    },
    demo(name, ...a) {
      console.log(name)
      console.log(a)
    },


  },
  watch: {
    todos: {
      deep: true,//这样才能监视到数组下一层的值
      handler(value) {
        sessionStorage.setItem("todos", JSON.stringify(value))
      }
    }
  },
  mounted() {
    this.$bus.$on('updateCheck',this.updateCheck)
    this.$bus.$on('deleteTodo',this.deleteTodo)
    this.$bus.$on('updateTodo',this.updateTodo)
  },
  beforeDestroy() {
    this.$bus.$off(['updateCheck','deleteTodo','updateTodo'])
  }

}
</script>

<style>
</style>
